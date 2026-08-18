# APPROACHES.md — Feasibility and Technical Approaches

## Summary verdict

UX Reviewer is **technically viable as a Bob skill** using infrastructure that
already exists in the Bob environment today. The core Figma-side analysis
(Carbon compliance, token validation, spacing, typography) requires no new
APIs, no procurement, and no external dependencies.

Design-to-implementation comparison is viable at a useful level using AI
vision. Pixel-precise comparison at CI scale requires additional tooling
(Playwright scripts or Applitools) but can be layered in as a Phase 2.

---

## Infrastructure already available

| Infrastructure | Status | How used |
|---|---|---|
| **Carbon MCP** | Live, public preview. IBM employees can use immediately. | Provides live queryable Carbon docs, usage guidelines, code examples, accessibility guidance |
| **Figma MCP** | Connected in Bob. | Reads Figma frame structure, tokens, component mappings, screenshots |
| **Claude vision** | Available in Claude models used by Bob. | Compares two images; identifies visual drift |
| **IBM Figma Enterprise org** | IBM employees auto-added via SSO. | Provides access to Carbon Figma libraries; Figma Library Analytics; Enterprise API scopes |
| **IBM Equal Access Checker** | Free browser extension, IBM-published. | Handles mechanical WCAG checking (not UX Reviewer's responsibility) |

---

## Capability-by-capability feasibility

### 1. Carbon compliance (Figma)
**Verdict: ✅ Viable today**

**Approach:**
1. `mcp__figma-mcp__get_design_context` — reads component structure, Code
   Connect mappings, and reference code for a Figma node
2. `mcp__figma-mcp__get_code_connect_map` — identifies which Figma nodes are
   mapped to Carbon components vs. custom/detached components
3. `mcp__carbon-mcp__docs_search` — queries Carbon's authoritative usage
   guidelines for each identified component pattern
4. LLM reasons: is this component being used correctly per Carbon guidance?
   Is the variant appropriate for this context? Is there a Carbon component
   that should have been used instead of a custom one?

**Constraint:** LLM reasoning against documentation will produce qualitative
findings, not deterministic pass/fail. Outputs are signals for human review,
not automated enforcement. This is appropriate and intentional — Carbon usage
guidelines contain contextual nuance that deterministic rules cannot capture.

---

### 2. Token and variable validation
**Verdict: ✅ Viable today**

**Approach:**
1. `mcp__figma-mcp__get_variable_defs` — returns all variable/token
   assignments for a node (e.g., `background: $layer-01`, or a hardcoded
   `#f4f4f4`)
2. Cross-reference against Carbon token documentation via
   `mcp__carbon-mcp__docs_search`
3. Flag any hardcoded values that correspond to a Carbon token, and any
   token usages that don't match the semantic intent of the context

**What it catches:** Hardcoded hex values where tokens exist; wrong semantic
token for context (e.g., using `$layer-02` where `$layer-01` is correct);
custom color values with no Carbon equivalent.

---

### 3. Layout and spacing analysis
**Verdict: ✅ Viable today**

**Approach:**
1. `mcp__figma-mcp__get_metadata` — returns exact positions and sizes
   (bounding boxes) for all nodes in the frame
2. Calculate spacing between sibling elements; check against Carbon's
   8px grid and defined spacing scale
   (`$spacing-01` through `$spacing-13`: 2px, 4px, 8px, 12px, 16px, 24px,
   32px, 40px, 48px, 64px, 80px, 96px, 160px)
3. Flag spacing values that fall off the scale or are not sourced from
   a spacing token

**What it catches:** Spacing values off the 8px grid; padding that doesn't
correspond to a Carbon spacing token; elements that appear misaligned by
comparing bounding box edges.

---

### 4. Typography review
**Verdict: ✅ Viable today**

**Approach:**
1. `mcp__figma-mcp__get_metadata` and `get_design_context` — extract
   font-family, font-size, font-weight, line-height, and letter-spacing
   values from text nodes
2. `mcp__figma-mcp__get_variable_defs` — confirms whether text styles are
   sourced from Carbon type tokens
3. `mcp__carbon-mcp__docs_search` — retrieves Carbon type scale and
   typography token definitions for comparison
4. Flag: non-IBM Plex typeface; font sizes not on the Carbon type scale;
   hardcoded values where type tokens exist; weight mismatches

---

### 5. Accessibility (Carbon pattern level)
**Verdict: ✅ Viable (scoped)**

**Approach:**
1. `mcp__carbon-mcp__docs_search` — retrieves Carbon accessibility guidance
   for each identified component
2. LLM inspects the frame structure (from `get_design_context` and
   `get_metadata`) against known Carbon accessibility patterns
3. Flag: interactive elements without visible focus indicators per Carbon
   patterns; form fields without visible labels; modals without close targets;
   icon-only buttons without accessible name annotations

**Scope boundary:** This is Carbon-pattern-level accessibility only.
Mechanical WCAG checking (contrast ratios, tab order, screen reader
announcement) is outside scope and delegated to IBM Equal Access Checker.
UX Reviewer complements, not replaces, that tool.

---

### 6. Design-to-implementation comparison
**Verdict: ⚠️ Viable at useful level; pixel-precise at scale requires Phase 2**

This is the most complex capability. Three distinct options exist with
different build costs and accuracy levels.

---

#### Option A — AI vision comparison (Phase 1, buildable now)
**Complexity: Low | Accuracy: Qualitative | Build time: Days**

**How it works:**
1. `mcp__figma-mcp__get_screenshot` — renders the Figma frame as an image
2. User provides a screenshot of the live implementation (browser, Storybook,
   staging environment)
3. Both images passed to Claude vision with a structured comparison prompt
4. Claude returns a categorised Visual Drift Report

**Output structure:**
```
Visual Drift Report:
- General Summary
- Layout Differences (alignment, element repositioning, spacing drift)
- Typography Deviations (font size, weight, line-height mismatches)
- Color Differences (palette, contrast, token mismatches)
- Missing or Extra Elements
- Recommended Actions
```

**What it catches:** Obvious layout drift, wrong colors, font size mismatches,
missing elements, repositioned components — anything visually apparent at
normal inspection zoom.

**What it misses:** Differences below ~4px; token violations where the visual
result looks correct but the underlying token is wrong; interactive state
differences; responsive breakpoint issues.

**Verdict for Bob skill:** Immediately viable. No new infrastructure.
Qualitative findings are still substantially faster and more consistent than
manual visual review.

---

#### Option B — Playwright CSS extraction (Phase 2, Bob-assisted workflow)
**Complexity: Medium | Accuracy: Pixel-precise | Build time: Weeks**

**How it works:**
1. Figma MCP reads exact design spec values (font-size, spacing, padding,
   dimensions) for each element
2. A Playwright script navigates to the live implementation (Storybook or
   staging URL) in a headless browser
3. Playwright calls `getComputedStyle()` and `getBoundingClientRect()` on
   each mapped element to extract actual rendered CSS values
4. Diff engine compares Figma spec values vs. computed values, element by
   element, producing exact pixel deltas
5. Bob reads the output and provides Carbon-aware interpretation

**Output example:**
```
| Element        | Figma spec | Rendered | Delta  |
|----------------|------------|----------|--------|
| Heading size   | 24px       | 28px     | +4px   |
| Button padding | 16px       | 12px     | -4px   |
| Gap (row)      | 8px        | 10px     | +2px   |
```

**Open source option:** [`uimatch`](https://github.com/kosaki08/uimatch) is a
CLI tool that does exactly this — compares a Figma node against a
Playwright-captured implementation, produces a pixel diff image, a
`report.json`, and a Design Fidelity Score (0–100). IBM teams can run this
in CI and pipe the structured JSON to Bob for Carbon-aware interpretation.

**Fit for Bob skill:** Bob generates and maintains the Playwright comparison
script for the team's component set. The script runs in CI post-deployment.
Results JSON is passed back to Bob, which provides Carbon-aware interpretation
("this 4px spacing deviation means the button is using `$spacing-02` instead
of the correct `$spacing-03` for this context").

**Constraint:** Bob cannot autonomously run Playwright. The script execution
lives in the team's CI pipeline. Bob acts as the intelligence layer, not the
execution layer.

---

#### Option C — Applitools Eyes with Figma plugin (Phase 3, procurement required)
**Complexity: Medium (setup) | Accuracy: Enterprise-grade | Build time: N/A (off-the-shelf)**

**How it works:**
1. Designer exports Figma frames to Applitools Eyes via the Figma plugin —
   frames become visual baselines
2. Developers run their standard test suite (Playwright, Selenium, Cypress)
   with Applitools Eyes SDK injected
3. Visual AI compares rendered screenshots against Figma baselines using
   configurable match levels: `Strict` (pixel), `Layout` (structural),
   `Content` (text/data)
4. Differences surface in a shared dashboard with side-by-side annotation

**What it adds over Options A and B:** AI noise filtering (suppresses false
positives from antialiasing/rendering differences); cross-browser coverage;
collaborative dashboard; CI-integrated pass/fail gates; no custom scripting.

**What it lacks for UX Reviewer:** It is not Carbon-aware. It detects that
something looks different from the design; it does not know whether the
design or the implementation violates Carbon standards. UX Reviewer would
complement Applitools, not replace it.

**Status for IBM teams:** Requires procurement. No confirmed IBM enterprise
license. Not a Bob skill — a separate tooling investment evaluated
independently.

---

## Phased delivery plan

### Phase 1 — Bob skill (buildable now, no procurement)

**Scope:**
- Carbon compliance analysis (Figma)
- Token and variable validation
- Layout and spacing analysis
- Typography review
- Accessibility at Carbon pattern level
- AI vision design-to-implementation comparison (Option A)
- Structured Markdown compliance report

**Stack:** Figma MCP + Carbon MCP + Claude vision + Bob skill wrapper

**User workflow:**
1. User says: "Review this Figma frame for Carbon compliance"
   and pastes a Figma URL
2. Optionally: pastes or attaches a screenshot of the implementation
3. Bob calls Figma MCP to read the frame, extract tokens, take a screenshot
4. Bob calls Carbon MCP to retrieve relevant guidelines
5. Bob returns a structured UX Review Report with severity-ranked findings

**No new infrastructure. No procurement. No additional tools.**

---

### Phase 2 — Bob-assisted CI workflow (requires team setup, no procurement)

**Adds:**
- Pixel-precise design-to-implementation comparison via Playwright
  (Bob generates/maintains the script; team runs it in CI)
- Bob interprets `uimatch` or custom Playwright output in Carbon terms
- Report includes exact pixel deltas alongside Carbon-aware explanations

**Requires:** Team has Storybook or a staging environment; Bob generates the
Playwright script; team wires it into their CI pipeline.

---

### Phase 3 — Enterprise visual regression gate (procurement decision)

**Adds:**
- Applitools Eyes for CI-integrated, AI-powered visual regression with
  Figma as baseline
- Cross-browser and cross-device coverage
- Collaborative dashboard for design/dev/QA sign-off

**Decision point:** If the organisation determines that CI-integrated,
automated visual regression at scale is a priority, Applitools is the
proven production-grade solution. This is a procurement decision evaluated
separately from the Bob skill.

---

## Key risks and mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| LLM reasoning produces false positives | Medium | Frame all outputs as "findings for review" not "confirmed violations"; include confidence signals |
| Carbon rules engine requires continuous maintenance as Carbon evolves | High | Use Carbon MCP as the live rule source — it updates with Carbon; no static rule set to maintain |
| Figma API rate limits at scale | Medium | Scope Phase 1 to on-demand, single-frame analysis; not background scanning |
| Automated tools catch only ~57% of accessibility issues | Medium | Scope clearly: UX Reviewer handles Carbon pattern level; IBM Equal Access Checker handles WCAG mechanical checks |
| AI vision comparison misses sub-4px deviations | Medium | Acknowledge ceiling in output; Phase 2 Playwright option addresses pixel-precision need |
| Design-to-dev parity requires live environment access | High | Phase 1 works from user-supplied screenshot; Phase 2 requires team CI setup; fully autonomous URL scanning is out of scope |

---

## What makes UX Reviewer distinct from everything in the market

Every existing tool covers a subset of what UX Reviewer covers. None combines:

1. **Carbon-specific semantic rules** — not generic design best practices, but
   whether the correct Carbon component is used in the correct context per
   Carbon's own usage guidelines, pulled live from Carbon MCP
2. **Unified single report** — spanning Figma compliance, token validation,
   spacing, typography, accessibility patterns, and implementation comparison
   in one artifact
3. **No new tool to learn** — delivered as a Bob skill; works where IBM teams
   already work
4. **Carbon MCP as the living rule source** — the rule set cannot go stale
   because it is Carbon's own documentation queried in real time

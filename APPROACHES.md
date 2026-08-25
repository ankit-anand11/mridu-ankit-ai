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

---

## IBM-internal experience — what we can achieve with Bob and existing IBM infrastructure

The competitive analysis surfaces six gaps that no market tool addresses. This section maps each gap to what is achievable *inside IBM today* using Bob, Carbon MCP, Figma MCP, and the Jira MCP — and where inspiration from each external tool informs the UX Reviewer design.

---

### What we take from each competitor — and how we go further

| Competitor | Their best idea | What limits them | What UX Reviewer does instead |
|---|---|---|---|
| **FigmaLint** | Hardcoded-value detection per node in Figma; AI-powered auto-fix | Figma-only; no Carbon knowledge; no code inspection; bring-your-own API key | UX Reviewer applies the same token-detection pattern but cross-references against **Carbon MCP** — so `#f4f4f4` is identified as `$layer-01` specifically, not just "a hardcoded colour" |
| **Chromatic** | Merge-blocking PR gate; snapshot diff as a formal review artifact | Visual regression only; cannot distinguish Carbon `Button` from a pixel-identical custom button | UX Reviewer brings the *intent* of a PR gate — a structured report that creates a "we reviewed this" artifact — but adds Carbon semantic awareness to the findings |
| **Supernova** | Code adoption tracking (which design system components are used in the codebase); MCP context distribution | Enterprise-only; not Carbon-specific; does not flag wrong components at branch level | UX Reviewer reads source code in a branch and uses Carbon MCP to reason whether imported components are Carbon components or non-Carbon replacements, then suggests the correct Carbon / Web Component alternative |
| **Tokens Studio** | Bidirectional Figma–code token sync; ensures tokens exist in the codebase | Only ensures supply; cannot detect whether a developer used the token or bypassed it with a hardcoded value | `stylelint-plugin-carbon-tokens` (open source, IBM-endorsed) fills this at the SCSS layer; UX Reviewer interprets its output in Carbon terms and explains which token was expected and why |
| **Zeroheight** | Living documentation queryable by AI via MCP; adoption analytics | Documentation-level only; adoption measured by doc page views, not code usage | Carbon MCP already provides this queryable knowledge layer. UX Reviewer uses it as the live rule source, not as a separate platform to maintain |

---

### Capability map — what UX Reviewer can deliver IBM-internally

Each capability is mapped to the Bob/IBM infrastructure that enables it. Nothing below requires procurement.

---

#### C1 — Carbon component compliance on a Figma frame
**Inspired by:** FigmaLint (component audit scoring), Supernova (code adoption tracking)
**What it does:** Given a Figma URL, identify every component in the frame, determine whether it is a Carbon component or a custom/detached variant, and evaluate whether it is used correctly per Carbon's usage guidelines.

**How it works inside Bob:**
```
1. mcp__figma-mcp__get_code_connect_map   → which nodes are Carbon vs. custom
2. mcp__figma-mcp__get_design_context     → component structure, variants, props
3. mcp__carbon-mcp__docs_search           → usage guidelines for each component
4. LLM reasons: correct component? correct variant? Carbon alternative exists?
```

**IBM-specific advantage:** The Carbon MCP is Carbon's own live documentation — not a scraped copy. When Carbon updates a usage guideline, UX Reviewer picks it up automatically. No static rule file to maintain.

**Output:** A list of components with: ✅ Carbon-compliant / ⚠️ wrong variant / ❌ non-Carbon (Carbon alternative: `<cds-dropdown>`)

---

#### C2 — Token compliance in a Figma frame
**Inspired by:** FigmaLint (hardcoded value detection), Tokens Studio (token supply pipeline)
**What it does:** For every node in the frame, identify whether colour, spacing, and typography values are sourced from Carbon tokens or hardcoded. Flag hardcoded values and name the Carbon token that should be used.

**How it works inside Bob:**
```
1. mcp__figma-mcp__get_variable_defs      → returns token assignments per node
                                            (e.g., background: $layer-01 OR #f4f4f4)
2. mcp__carbon-mcp__docs_search           → retrieves the correct token for the
                                            context (e.g., layer, interactive, danger)
3. LLM flags: hardcoded hex where token exists; semantically wrong token for context
```

**IBM-specific advantage:** Tokens Studio shows tokens exist in code; FigmaLint finds hardcoded values in Figma. UX Reviewer does both and adds the *why* — explaining which Carbon semantic token should replace each hardcoded value and in what context.

**Output:** Per-node token report with: token name / hardcoded value / Carbon replacement / severity

---

#### C3 — Token compliance in code (developer branch)
**Inspired by:** FigmaLint (Figma-side detection) + Tokens Studio (token pipeline) — combined into a code-side check
**What it does:** Scan a developer's code branch for hardcoded hex/px values that should be Carbon tokens. Identify non-Carbon component imports.

**How it works inside Bob:**
```
1. Bob reads the source files (JSX, SCSS, CSS) in the branch
2. Regex/AST scan: flag color: #XXXXXX, padding: Npx, margin: Npx
3. mcp__carbon-mcp__docs_search → identify the correct Carbon token for each value
4. Scan import statements: flag non-Carbon component imports
   (e.g., import { Dropdown } from 'primeng/dropdown' instead of '@carbon/react')
5. mcp__carbon-mcp__code_search → find the correct Carbon/Web Component equivalent
```

**IBM-specific advantage:** The `stylelint-plugin-carbon-tokens` (official Carbon tooling) can be invoked for SCSS files. Bob interprets its output and adds Carbon-aware explanation. For React component imports, Carbon MCP code_search maps each non-Carbon component to its Carbon or `@carbon/web-components` replacement — including Web Component alternatives for Angular/PrimeNG migrations.

**Output:** File-by-file list of hardcoded values + wrong imports, with Carbon replacement for each.

---

#### C4 — Figma vs. implementation delta comparison
**Inspired by:** Chromatic (visual diff), Applitools (Figma-as-baseline comparison) — both require procurement or lose Carbon awareness
**What it does:** Compare what was designed in Figma against what was implemented, identifying visual and structural drift.

**How it works inside Bob (Phase 1 — AI vision):**
```
1. mcp__figma-mcp__get_screenshot         → renders the Figma frame as an image
2. User provides screenshot of live implementation
3. Claude vision compares both images
4. LLM produces a structured Visual Drift Report with Carbon-aware explanations
```

**How it works inside Bob (Phase 2 — pixel-precise):**
```
1. Figma MCP reads exact design spec values per element
2. Bob generates a Playwright script targeting the team's Storybook/staging URL
3. Script extracts computed CSS values via getComputedStyle() / getBoundingClientRect()
4. Bob diffs Figma spec vs. rendered values and interprets in Carbon terms:
   "Button padding is 12px; Carbon $spacing-04 (16px) was specified — missing 4px"
```

**IBM-specific advantage:** Neither Chromatic nor Applitools knows whether a visual difference is a Carbon violation or an intentional deviation. Bob does — because it can cross-reference the visual delta against Carbon MCP guidelines in the same conversation.

---

#### C5 — Structured compliance report auto-posted as a Jira ticket
**Inspired by:** Chromatic (PR artifact as gate) + Supernova (adoption reporting) — neither creates actionable Jira tickets
**What it does:** When compliance findings exist, UX Reviewer auto-creates a Jira ticket with structured description, severity-ranked findings, and Carbon-specific acceptance criteria.

**How it works inside Bob:**
```
1. UX Review Report is generated (from any of C1–C4 above)
2. Bob uses the Jira MCP to create a ticket:
   - Title: "UX Review findings — [screen/component name]"
   - Description: full structured report with finding, severity, Carbon reference
   - Acceptance criteria: one per Critical/Major finding — what "fixed" looks like
   - Labels: ux-review, carbon-compliance, [product team]
3. Ticket is assigned to the developer; linked to the Figma frame and/or PR
```

**IBM-specific advantage:** This closes the loop that every market tool leaves open. The findings do not sit in a chat transcript or a Markdown file — they become a tracked, assignable work item. Developers can take the ticket directly to Bob and say "fix the issues in this ticket" — the acceptance criteria are already machine-readable.

**Bob infrastructure required:** Jira MCP (already available as a Bob skill).

---

#### C6 — Carbon as the pre-loaded rule set (no configuration required)
**Inspired by:** Every tool surveyed — all are design-system-agnostic and require teams to configure their own rules
**What it does:** UX Reviewer ships with Carbon's component inventory, token taxonomy, and usage guidelines pre-loaded via Carbon MCP. Teams do not configure anything.

**How it works inside Bob:**
```
No configuration step. Carbon MCP is the rule source.
- Component rules:   mcp__carbon-mcp__docs_search ("When should I use Select vs Dropdown?")
- Token rules:       mcp__carbon-mcp__docs_search ("What token should be used for interactive text?")
- Code examples:     mcp__carbon-mcp__code_search ("Show me the Carbon Button with danger variant")
- Web Components:    mcp__carbon-mcp__code_search ("Show me <cds-dropdown> usage")
```

**IBM-specific advantage:** Carbon MCP is Carbon's own documentation — maintained by the Carbon team, updated with every release. The UX Reviewer skill never has a stale rule set. This is what every competitor lacks and cannot easily replicate for Carbon specifically.

---

### IBM experience summary — what the full tool feels like

The experience for IBM designers and developers is a single natural-language interface in Bob — no new dashboards, no plugins to install, no API keys to manage.

**For a designer:**
> "Review this Figma frame for Carbon compliance"
> → Pastes Figma URL
> → Gets a structured report: which components are wrong, which tokens are hardcoded, which spacing values are off — all with Carbon references and severity ratings

**For a developer:**
> "Check my branch for Carbon compliance before I raise a PR"
> → Bob scans imports and SCSS for non-Carbon components and hardcoded values
> → Returns a file-by-file findings list with Carbon replacements
> → Optionally: "Create a Jira ticket from these findings" → ticket created automatically

**For a tech lead / designer auditing another team's work:**
> "Compare this Figma frame against this screenshot of the staging build"
> → Bob compares both visually, names Carbon violations in the drift, creates a Jira ticket

**What is never required:**
- No procurement
- No new tool to learn
- No Carbon rule files to write or maintain
- No separate dashboard or subscription
- No manual copy-paste of findings into Jira

---

### Phased experience rollout

| Phase | What IBM designers/devs can do | Infrastructure |
|---|---|---|
| **Phase 1** (now) | Figma frame compliance review; token audit; AI vision Figma–vs–screenshot comparison; Jira ticket creation from findings | Bob + Carbon MCP + Figma MCP + Jira MCP |
| **Phase 2** (team setup required) | Pixel-precise Figma–vs–implementation diff via Bob-generated Playwright script in CI | Bob + Playwright (team-run) + Carbon MCP |
| **Phase 3** (procurement decision) | Enterprise visual regression gate with Figma as baseline, cross-browser, collaborative dashboard | Applitools Eyes (separate investment) |

The Phase 1 experience is available to every IBM team on Bob today — the only requirement is a Figma URL.

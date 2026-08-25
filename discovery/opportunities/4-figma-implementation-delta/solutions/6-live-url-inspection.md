# Solution 6 — Live URL Inspection

**Opportunity:** C4 — Figma vs. implementation delta comparison
**SCAMPER lens:** Adapt — adapt the visual comparison workflow to accept a live browser URL instead of a user-supplied screenshot
**Effort:** S–M (depending on sub-mode)
**Status:** Approved for risk evaluation

---

## Description

The user provides two inputs: (1) a Figma frame URL, and (2) a live URL where the implementation is accessible — a staging environment, an internal dev server, a Storybook deployment, or any browser-reachable address.

Bob uses Figma MCP's `get_screenshot` to render the Figma frame. For the implementation side, two sub-modes are available depending on what the user needs:

**6a — DOM Structure Extraction (zero setup)**
Bob calls `tavily_extract` on the implementation URL, which returns the rendered page content: DOM structure, component labels, text content, element hierarchy. Bob compares this structural content against the Figma frame's `get_design_context` output. The report covers structural drift — missing components, wrong text, incorrect hierarchy — interpreted against Carbon MCP. No visual image is produced for the implementation side.

**6c — Playwright-lite (one local command)**
The user runs a one-shot Node script that Bob generates. The script navigates to the implementation URL in a headless browser, captures a rendered screenshot, and extracts computed CSS values (`getComputedStyle`, `getBoundingClientRect`) for mapped elements. The user drops the output (screenshot + JSON) into Bob. Bob then performs the full visual + structural comparison against the Figma frame — producing a pixel-aware, Carbon-interpreted drift report.

The two modes can be combined: 6a first for a fast structural check, 6c when visual fidelity is needed.

---

## How it addresses the opportunity

Solution 6 reduces the primary friction of Solution 1 (Screenshot Drop): the user no longer needs to take and paste a screenshot. If the implementation is reachable via a URL — which is the case for any team with a staging environment, Storybook deployment, or dev server — the URL is the only input beyond the Figma frame.

Evidence that this removes a real barrier:

- **Hariharan** described a 2–3 iteration manual loop: *"I will take a snap and I will paste it in Bob… the pasted screenshot and the actual dropdown won't match. So these kinds of differences arise. So it will take 2–3 iterations."* (`interview-findings.md` W8). A URL input eliminates the snap-and-paste step from each iteration.
- **Senthil** described the desired outcome as branch + URL-driven: *"I can get the branch information from them. I can just put it on the tool and run it. I don't have to ask them."* (`interview-findings.md` D1). A URL-based input maps directly to this mental model.
- **U4** (compliance check before PR merge) was cited by Hariharan and Senthil — both of whom would have a staging or preview URL available at pre-PR time.

---

## Key capabilities

| Capability | Sub-mode | Bob infrastructure |
|---|---|---|
| Figma frame screenshot | Both | `mcp__figma-mcp__get_screenshot` |
| DOM structure extraction from URL | 6a | `mcp__tavily__tavily_extract` |
| Design context extraction | 6a | `mcp__figma-mcp__get_design_context` |
| Structural drift comparison | 6a | LLM reasoning |
| Carbon-aware interpretation | Both | `mcp__carbon-mcp__docs_search` |
| Bob-generated Playwright script | 6c | Bob code generation |
| Computed CSS extraction + screenshot | 6c | Playwright (user-run, one command) |
| Visual + pixel-aware comparison | 6c | Claude vision + LLM diff |
| Structured UX Review Report | Both | Bob skill output (Markdown) |
| Optional Jira ticket | Both | Jira MCP |

---

## Workflow

**Mode 6a — DOM Structure Extraction:**
```
1. User: "Compare this Figma frame against this URL"
   → Pastes Figma URL + implementation URL

2. Bob calls get_screenshot(figmaURL)
   → Renders Figma frame as image

3. Bob calls get_design_context(figmaURL)
   → Extracts component tree, element labels, hierarchy

4. Bob calls tavily_extract(implementationURL)
   → Returns rendered DOM structure, text content, component labels

5. LLM compares Figma context vs. extracted DOM:
   → Missing components?
   → Wrong text content?
   → Incorrect element hierarchy?
   → Extra elements not in the design?

6. Bob calls docs_search(Carbon MCP) for flagged findings
   → Carbon-aware interpretation

7. Bob returns:
   → Structural Drift Report (component/text/hierarchy findings)
   → Note: visual/spacing findings require screenshot or Mode 6c
```

**Mode 6c — Playwright-lite:**
```
1. User: "Compare this Figma frame against this URL — full visual check"
   → Pastes Figma URL + implementation URL

2. Bob generates a Playwright script:
   → Navigates to the implementation URL
   → Captures a full-page screenshot
   → Extracts getComputedStyle() and getBoundingClientRect() for key elements
   → Outputs: screenshot.png + computed-values.json

3. User runs: node check.js https://staging.example.com
   → Takes ~30 seconds; outputs screenshot.png and computed-values.json

4. User drops both files into the Bob conversation

5. Bob calls get_screenshot(figmaURL)
   → Figma frame rendered as image

6. Bob calls get_design_context(figmaURL)
   → Exact design spec values per element

7. Claude vision compares Figma screenshot vs. implementation screenshot
   → Visual drift (layout, colour, typography, missing elements)

8. LLM diffs Figma spec values vs. computed-values.json
   → Pixel-level deviations with Carbon token interpretation
   → "Button padding is 12px; Carbon $spacing-04 (16px) was specified"

9. Bob returns:
   → Full UX Review Report (visual + structural + pixel-aware findings)
   → Optional Jira ticket creation
```

---

## Effort estimate

**6a:** S — `tavily_extract` is already available. Work is the comparison prompt and report template for structural-only findings. Buildable in days alongside Solution 1.

**6c:** M — Bob-generated Playwright script requires prompt engineering and script design. User must have Node.js installed locally (standard for frontend developers). One-time script generation per team; Bob can regenerate if the URL structure changes.

---

## Key assumptions

**Both modes:**
- The implementation URL is reachable from the outside. *Discovery needed:* IBM internal staging URLs may require VPN or authentication. Tavily's extraction servers cannot access VPN-gated URLs. If the URL is internal-only, 6a degrades to "URL not reachable" and the user must fall back to Solution 1 (screenshot). This is the highest-impact unknown for 6a.

**Mode 6a:**
- `tavily_extract` returns sufficient DOM structure from the rendered page. JavaScript-heavy SPAs (React, Angular) may return minimal content if Tavily captures the pre-hydration HTML. Discovery needed: test against a real IBM webMethods staging URL.

**Mode 6c:**
- IBM developer laptops have Node.js and can run Playwright. This is standard for frontend developers (Sahana, Hariharan) but should be confirmed.
- The user is willing to run one terminal command. This is a meaningful but low step — lower than setting up CI but higher than pasting a screenshot.

---

## Advantages

- **Reduces friction below Solution 1** — URL input is available at any point in development; screenshot requires the user to switch to a browser, capture, and paste
- **Structural check is additive to visual check** — 6a catches missing components, wrong text, and hierarchy errors that may not be visible in a screenshot
- **Pixel precision on demand** — 6c provides sub-4px accuracy when needed, bridging the gap between Solution 1 (qualitative) and Solution 3 (full CI Playwright gate)
- **Mental model alignment with Senthil's desired outcome** — URL + branch as inputs matches exactly how Senthil described wanting the tool to work
- **Composable with Annotation Anchor** — if an anchor (Solution 4) exists for the screen, the 6c JSON output can be compared against the anchor spec for a traceable, structured diff
- **Graceful degradation** — if the URL is not reachable (VPN-gated), the user gets a clear message and can fall back to Solution 1 without data loss

---

## Known limitations

- **6a is blind to visual drift** — DOM extraction cannot detect spacing deviations, colour differences, or typography mismatches. It is structural-only. Visual findings still require a screenshot (Solution 1) or Playwright run (6c).
- **VPN/authentication barrier is the critical unknown** — if IBM staging URLs are not publicly reachable, 6a loses most of its value. This must be tested before building.
- **6c adds one user action** — running a terminal command is a low but real friction increase over Solution 1. Less-technical users (designers) are unlikely to use 6c.
- **JavaScript SPA hydration risk** — Tavily may capture pre-hydration HTML for React/Angular apps, which contains less rendered content. This needs testing on a real IBM webMethods URL.

---

## Risk evaluation

| Dimension | Score | Rationale |
|---|---|---|
| **Value** | 4 | Directly addresses U4 and D5 (Hariharan + Senthil). URL input aligns with Senthil's mental model. Structural check adds a signal layer beyond vision. Score not 5: value is conditional on URL reachability — if IBM URLs are VPN-gated, the solution degrades to Solution 1 with extra steps. |
| **Viability** | 3 | `tavily_extract` confirmed available. Visual comparison in 6c requires user-run Playwright. Discovery needed: URL reachability from Tavily servers; SPA hydration behaviour on IBM staging URLs. |
| **Usability** | 4 | 6a is zero-setup for users with a publicly reachable URL. 6c adds one terminal command — appropriate for developers (Hariharan, Sahana, Senthil) but not designers. Clear degradation path to Solution 1 if URL is not reachable. |
| **Feasibility** | 3 | 6a feasibility is entirely conditional on URL reachability — the single most important open question. 6c requires Node/Playwright locally (standard for frontend devs but unconfirmed for IBM laptops). Playwright script generation is straightforward Bob code generation. |

**Overall risk profile: Medium.** The URL reachability question is a binary — if IBM staging URLs are publicly reachable (or reachable over IBM network), this solution works well. If not, 6a collapses and 6c becomes the only URL-based path. The reachability test should be the first action before any build work begins.

---

## Recommended next steps

1. **Reachability test (highest priority)** — run `tavily_extract` on a real IBM webMethods staging URL (or ask Senthil/Hariharan for a URL) and confirm what is returned. This single test answers the critical feasibility question.
2. **SPA hydration test** — confirm whether `tavily_extract` returns rendered component content or pre-hydration HTML shell for a React/Angular SPA.
3. **If 6a is viable:** build the structural comparison prompt alongside Solution 1 (same sprint — both are small).
4. **If 6a is not viable:** evaluate whether 6c (Playwright-lite) is worth building as a standalone path, or whether Solution 3 (full CI Playwright gate) better serves the precision use case.

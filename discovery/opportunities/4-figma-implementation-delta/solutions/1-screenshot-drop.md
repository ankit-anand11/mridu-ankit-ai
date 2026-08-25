# Solution 1 — Screenshot Drop

**Opportunity:** C4 — Figma vs. implementation delta comparison
**SCAMPER lens:** Substitute — substitute pixel-precise tooling with AI vision
**Effort:** S
**Status:** Approved for risk evaluation

---

## Description

The user provides two inputs to Bob:

1. A Figma frame URL
2. A screenshot of the live implementation (pasted or dragged into the Bob conversation)

Bob calls Figma MCP's `get_screenshot` to render the Figma frame as an image. Claude vision then compares both images side-by-side. Each visual difference is cross-referenced against Carbon MCP (`docs_search`) to determine whether the drift constitutes a Carbon violation, an intentional design deviation, or visual noise. The output is a structured UX Review Report following the format defined in `AGENTS.md`.

No new tooling. No CI setup. No Playwright scripts. No procurement.

---

## How it addresses the opportunity

C4's core gap — confirmed as market gap G4 — is that no existing tool compares a live implementation against its Figma source of truth *with Carbon-aware interpretation*. Screenshot Drop is the most direct path to closing that gap:

- **Hariharan** explicitly described this workflow: *"There is a skill that actually evaluates — I mean, to get the styling part from the Figma. So maybe we could utilise it by connecting… and comparing with Figma and identifying the delta."* (`interview-findings.md` D5)
- **Senthil** described the same need from a tech-lead perspective: *"I can get the branch information from them. I can just put it on the tool and run it."* (`interview-findings.md` D1)
- **Animesh** captured the severity: *"I see the actual implementation and I am like, did I design this?"* (`designer-group session`)

The tool closes this gap for **any team at any maturity level** — including Hariharan's Angular/PrimeNG team, which has no Code Connect, no dev mode access, and no CI infrastructure.

---

## Key capabilities

| Capability | Bob infrastructure |
|---|---|
| Figma frame screenshot | `mcp__figma-mcp__get_screenshot` |
| Visual comparison | Claude vision |
| Carbon-aware interpretation of drift | `mcp__carbon-mcp__docs_search` |
| Structured UX Review Report | Bob skill output (Markdown) |
| Optional Jira ticket creation | Jira MCP (C5) |

---

## Workflow

```
1. User: "Compare this Figma frame against my implementation"
   → Pastes Figma URL + implementation screenshot

2. Bob calls get_screenshot(figmaURL)
   → Renders Figma frame as image

3. Claude vision compares both images:
   → Layout drift (spacing, alignment, positioning)
   → Typography deviations (size, weight, line-height)
   → Colour differences (token vs. hardcoded)
   → Missing or extra elements
   → Component identity (Carbon vs. custom)

4. Bob calls docs_search(Carbon MCP) for each flagged finding
   → Is this drift a Carbon violation?
   → Which Carbon standard was not met?
   → What is the correct token / component / pattern?

5. Bob returns:
   → Structured UX Review Report (severity-ranked findings)
   → Optional: "Create a Jira ticket from these findings"
```

---

## Effort estimate: S

All infrastructure is available today. Deliverables are:

- Skill wrapper (SKILL.md trigger phrases, context prompt)
- Structured comparison prompt (instructs Claude vision to produce Carbon-aware findings)
- Report template validation against AGENTS.md format

Estimated build time: days, not weeks. No procurement, no new MCP connections, no team setup required.

---

## Key assumptions

- Screenshots are sufficient resolution for Claude vision to identify spacing, component, and colour differences. Claude vision reliably catches differences of ~4px and above (`APPROACHES.md` Option A known ceiling).
- The user can supply a screenshot of the implementation. This is a manual step — the user must have browser access to the staging or live environment and take the screenshot themselves.
- Carbon MCP is available and queryable at the time of review (confirmed: already connected in Bob environment per `AGENTS.md`).

---

## Advantages

- **Lowest barrier to adoption** — works for every team regardless of Carbon maturity, CI setup, or Figma Code Connect configuration
- **Zero infrastructure** — no new tools, no procurement, no setup
- **Fastest path to value** — buildable in days; available to every IBM team on Bob immediately
- **Carbon-aware** — drift is interpreted against Carbon standards, not just flagged as visual difference
- **Accessible to low-maturity teams** — Hariharan's team can use this today; does not require dev mode, Code Connect, or a CI pipeline
- **Composable** — the output naturally feeds into C5 (Jira ticket creation); pairs with Solution 4 (Annotation Anchor) as a post-implementation check against the pre-handoff spec

---

## Known limitations

- **Sub-4px deviations are not reliably caught** — token violations where the visual output looks correct (e.g., correct colour but wrong semantic token) are invisible to vision. Solution 3 (Playwright CI Gate) addresses this ceiling if pixel precision is required.
- **Requires user-supplied screenshot** — no autonomous URL capture. The user must take the screenshot and provide it. Solution 6 (Live URL Inspection) reduces this friction when a browser URL is available.
- **Static states only** — hover, focus, and active states require separate screenshots. Interactive compliance is out of scope for this solution.

---

## Risk evaluation

| Dimension | Score | Rationale |
|---|---|---|
| **Value** | 5 | D5 cited by Hariharan + Senthil; Animesh's "did I design this?" moment; market gap G4 confirmed across all 5 competitive tools. Highest-frequency unmet need in the research. |
| **Viability** | 4 | Phase 1 confirmed buildable — Option A in `APPROACHES.md`. Claude vision + Figma MCP `get_screenshot` + Carbon MCP already available. Only deliverable is skill wrapper and prompt engineering. |
| **Usability** | 4 | Zero new tools, zero setup, works in a Bob conversation. Matches D6 (tool must work for low-maturity teams without process overhaul). Risk: one manual screenshot step. |
| **Feasibility** | 4 | All infrastructure confirmed. Known ceiling (sub-4px, token violations where visual output looks correct) is documented and acknowledged in output. No open feasibility questions. |

**Overall risk profile: Low.** The only meaningful risk is the accuracy ceiling of AI vision, which is documented and bounded. No infrastructure, procurement, or behaviour-change risks.

---

## Recommended next step

Build the skill scaffold and validate the report format with one designer (Diya) and one developer (Senthil) on a real Figma frame from the API team's current sprint. This is the recommended Phase 1 pilot activity from `SYNTHESIS.md` Section 8.

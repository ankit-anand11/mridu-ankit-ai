# Solution Evaluations — C4: Figma vs. Implementation Delta

**Opportunity:** C4 — Figma vs. implementation delta comparison
**Date:** August 2026
**Prepared by:** Mridusmita Nath, Ankit Anand
**Solutions evaluated:** 3 (of 5 generated via SCAMPER brainstorm)

---

## Comparison table

| Dimension | Solution 1 — Screenshot Drop | Solution 4 — Annotation Anchor | Solution 6 — Live URL Inspection |
|---|:---:|:---:|:---:|
| **Value** | **5** | 4 | 4 |
| **Viability** | **4** | 3 | 3 |
| **Usability** | **4** | 3 | 4 |
| **Feasibility** | **4** | 3 | 3 |
| **Total** | **17** | 13 | 14 |
| **Effort** | S | M | S–M |
| **Risk profile** | Low | Medium | Medium |
| **Open discovery questions** | 0 | 3 | 2 |

**Scoring:** 1–2 = high risk / low confidence · 3 = no data (default) · 4–5 = strong evidence supporting low risk

---

## Individual scores with evidence

### Solution 1 — Screenshot Drop

| Dimension | Score | Evidence |
|---|---|---|
| **Value** | 5 | D5 cited by Hariharan + Senthil (`interview-findings.md`). Animesh: *"I see the actual implementation and I am like, did I design this?"* (`designer-group session`). Market gap G4 confirmed unaddressed across all 5 competitive tools (`competitive-insights.md`). Highest-frequency unmet need in the research. |
| **Viability** | 4 | Phase 1 confirmed buildable — Option A in `APPROACHES.md:131`. Claude vision + Figma MCP `get_screenshot` + Carbon MCP confirmed available. Deliverables are skill wrapper and comparison prompt only. |
| **Usability** | 4 | Zero new tools, zero setup, works in existing Bob conversation. Matches D6 (`interview-findings.md:399`) — tool must work for low-maturity teams without process overhaul. Single friction point: user must supply a screenshot (one manual step). |
| **Feasibility** | 4 | All infrastructure confirmed in `APPROACHES.md:160`: *"Immediately viable. No new infrastructure."* Known ceiling (sub-4px, token violations where visual output looks correct) is bounded and documented. No open feasibility questions. |

---

### Solution 4 — Annotation Anchor

| Dimension | Score | Evidence |
|---|---|---|
| **Value** | 4 | Directly addresses handoff communication gap: Nagaraj's verbal custom-component warnings and Animesh's 2-hour annotation sessions (`designer-group session`). Reduces rework loop. Score not 5: no participant explicitly named this workflow — value inferred from pain points, not stated desired outcome. |
| **Viability** | 3 | `get_design_context` + `get_variable_defs` confirmed available. Anchor schema design not prototyped. Discovery needed: whether these tools return sufficient structured data from Figma files without Code Connect (Hariharan's team). |
| **Usability** | 3 | Requires designer behaviour change — a new handoff step they must initiate. No evidence that designers would adopt this without validation. Discovery needed: validate with Diya and Animesh in a 30-minute session before building. |
| **Feasibility** | 3 | Figma MCP tools confirmed. Novel work: anchor schema design, Jira Markdown attachment, degraded-file fallback. Staleness risk if design is iterated post-anchor. Jira Markdown attachment mechanism needs validation. |

---

### Solution 6 — Live URL Inspection

| Dimension | Score | Evidence |
|---|---|---|
| **Value** | 4 | Addresses U4 and D5 (Hariharan + Senthil, `interview-findings.md`). URL input matches Senthil's mental model exactly. Structural check via 6a adds signal beyond vision. Score not 5: value conditional on URL reachability — degrades to Solution 1 equivalent if IBM staging URLs are VPN-gated. |
| **Viability** | 3 | `tavily_extract` confirmed available. Discovery needed: IBM staging URL reachability from Tavily servers; SPA hydration behaviour for React/Angular apps. 6c requires user to run Playwright locally — standard for frontend devs but unconfirmed. |
| **Usability** | 4 | 6a is zero-setup with a publicly reachable URL. 6c adds one terminal command — appropriate for developers, not designers. Clear degradation path to Solution 1 if URL unreachable. |
| **Feasibility** | 3 | 6a feasibility entirely conditional on URL reachability — binary unknown. 6c requires Node/Playwright locally (standard for frontend devs, unconfirmed for IBM laptops). Playwright script generation is straightforward Bob code generation. |

---

## Recommended solution

**Solution 1 — Screenshot Drop, built first. Solution 6 (6a) built in the same sprint if the reachability test passes.**

**Justification:**

Solution 1 is the only solution with zero open discovery questions and a confirmed evidence base. It has the highest total score (17), the lowest effort (S), and the lowest risk profile. It addresses the highest-frequency unmet need in the research (D5, cited by Hariharan, Senthil, Animesh) and closes market gap G4. It is buildable in days using infrastructure already available in Bob. It is the correct first build.

Solution 6 is the natural complement to Solution 1, not a replacement. The URL input removes the one friction point Solution 1 has (user-supplied screenshot) for teams with publicly accessible staging environments. The reachability test is a one-hour effort that should run in parallel with Solution 1 skill development. If it passes, 6a can be wired into the same skill as a URL-input path with minimal additional work.

Solution 4 (Annotation Anchor) is the most strategically differentiated option — it solves a problem that Solution 1 and 6 do not address (pre-handoff compliance record, custom component flagging). It should be built second, after the designer adoption assumption is validated. It is not a replacement for Solution 1; it is a layer that makes Solution 1's post-implementation comparison more structured and traceable.

**Recommended sequencing:**
1. Build Solution 1 (days)
2. Run reachability test for Solution 6 (parallel, 1 hour)
3. Wire Solution 6a into Solution 1 skill if test passes (same sprint)
4. Validate Solution 4 designer adoption assumption with Diya + Animesh (30-minute session)
5. Build Solution 4 if validated (2–3 weeks, second sprint)

---

## Go / no-go recommendation

**Go — on Solution 1 immediately.**

The evidence base is sufficient, the infrastructure is confirmed, the risk is low, and the user need is the highest-frequency finding across both developer and designer research. There is no material discovery gap that should delay building Solution 1.

**Conditional go — on Solution 6.**
Proceed with the reachability test this week. If IBM staging URLs are reachable from Tavily, add 6a to the Solution 1 sprint. If not, defer 6c to Phase 2 alongside Solution 3 (Playwright CI Gate).

**Go pending validation — on Solution 4.**
High value potential but the designer behaviour-change assumption must be validated before building. A 30-minute session with Diya and Animesh is the gate condition. Do not build before that session.

---

## Critical evidence gaps

These are the open questions that most affect the quality of the recommendation. Resolving them in order of impact:

| # | Gap | Affects | How to resolve | Urgency |
|---|---|---|---|---|
| **EG1** | IBM staging URL reachability from Tavily servers | Solution 6a viability | Run `tavily_extract` on a real IBM webMethods staging URL (ask Senthil or Hariharan for a URL). 1 hour. | This sprint |
| **EG2** | Designer willingness to add an anchor step at handoff | Solution 4 usability | 30-minute session with Diya and Animesh — show them a prototype anchor from a real Figma frame. | Before Solution 4 build |
| **EG3** | `get_design_context` output quality on low-maturity Figma files | Solution 4 feasibility | Test against one of Hariharan's team's Figma files (no Code Connect). Confirms what degraded-output fallback must handle. | Before Solution 4 build |
| **EG4** | Jira Markdown attachment via Jira MCP | Solution 4 feasibility | 30-minute technical spike — attempt to attach a Markdown document to a test Jira ticket via Jira MCP. | Before Solution 4 build |
| **EG5** | SPA hydration: does `tavily_extract` return rendered content for React/Angular apps | Solution 6a value | Test against a known React or Angular staging URL (can use a public Storybook if IBM URLs are not reachable). | This sprint (with EG1) |

---

## Key judgment calls

**Scores I was confident in:**
- Solution 1 Value (5) — three developer interviews and the designer group session all converge on this need; market gap G4 is confirmed across five competitive tools with no exceptions
- Solution 1 Feasibility (4) — `APPROACHES.md` explicitly confirms buildability with existing infrastructure; no speculative components
- Solution 4 Usability (3) — the behaviour-change risk is real; defaulting to 3 ("no data") is the correct call rather than assuming designers will adopt without validation

**Scores I flagged as low-confidence:**
- Solution 6 Viability (3) — the URL reachability question is a binary unknown that cannot be scored higher without testing. If IBM staging URLs are publicly reachable, this score would move to 4. If VPN-gated, it drops to 2 for 6a.
- Solution 4 Viability (3) — `get_design_context` on low-maturity files is an untested path. The Figma MCP tools are confirmed but their output quality on files without Code Connect or token variables is genuinely unknown.

**Top evidence gaps that most affect the recommendation:**
1. **EG1 (URL reachability)** — determines whether Solution 6 is worth building at all in Phase 1, or whether it belongs in Phase 2 with the Playwright CI gate
2. **EG2 (designer adoption)** — determines whether Solution 4 is a product feature or a workflow nobody uses
3. Together, EG1 and EG2 define the shape of the second sprint. EG1 can be resolved in an hour; EG2 requires a user session. Both should be active before Solution 1 ships.

---

## Source files

| File | Role in this evaluation |
|---|---|
| [`SYNTHESIS.md`](../../../SYNTHESIS.md) | C4 capability definition, 6 market gaps, compliance spectrum |
| [`APPROACHES.md`](../../../APPROACHES.md) | Technical feasibility, Option A/B/C analysis, Phase 1 confirmation |
| [`research/transcripts/uxr-sessions/interview-findings.md`](../../../research/transcripts/uxr-sessions/interview-findings.md) | Developer pain points, unmet needs, desired outcomes (D1, D5, U4, W8) |
| [`research/transcripts/uxr-sessions/interview-summary-designer-group-discovery-webmethods.md`](../../../research/transcripts/uxr-sessions/interview-summary-designer-group-discovery-webmethods.md) | Designer pain points: handoff gap, annotation burden, custom component debt |
| [`research/competitive-analysis/competitive-insights.md`](../../../research/competitive-analysis/competitive-insights.md) | Market gap G4 confirmation across 5 tools |
| [`AGENTS.md`](../../../AGENTS.md) | UX Review Report format, severity definitions, MCP tool map |

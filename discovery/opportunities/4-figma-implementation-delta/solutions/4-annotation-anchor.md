# Solution 4 — Annotation Anchor

**Opportunity:** C4 — Figma vs. implementation delta comparison
**SCAMPER lens:** Rearrange — shift the comparison from post-implementation to pre-handoff
**Effort:** M
**Status:** Approved for risk evaluation

---

## Description

Rather than comparing after implementation, this solution generates a structured **compliance anchor** from the Figma frame at handoff time. Bob reads the Figma frame via `get_design_context` and `get_variable_defs`, resolves each component and token against Carbon MCP, and produces a machine-readable spec — a Markdown document listing every component, its expected Carbon tokens, spacing values, and compliance status.

This anchor is attached to the Jira ticket at handoff. The developer implements against it. Post-implementation, a check can diff the actual implementation against the anchor rather than requiring fresh Figma MCP access — making the comparison traceable, persistent, and independent of the live Figma file.

The anchor also solves a secondary problem: it surfaces, at handoff, which components are custom or non-Carbon — replacing the verbal, ad hoc warnings that designers currently give developers (and sometimes forget to give at all).

---

## How it addresses the opportunity

C4's gap is the absence of a structured comparison between what was designed and what was built. The Annotation Anchor attacks this from the left end of the timeline — it creates the comparison baseline *before* a line of code is written, rather than *after* implementation diverges.

This directly addresses pain points that the screenshot-comparison approach does not reach:

- **Nagaraj** described the handoff gap: *"Sometimes we will not tell also… they will be looking for the Carbon component and they might miss something… they will reach back to me saying that this is not the Carbon. Then I will say, I might have forgot to say."* (`designer-group session`)
- **Animesh** described the annotation burden: *"I had to spend like 2 hours actually annotating what all changes have to be made and that feedback was given. Then it was implemented in like 2 weeks, then it was reviewed again."* (`designer-group session`)
- **Diya** described the structural fix: the API Management PR review gate — a hard handoff artefact that makes designer approval a dependency before merge. The anchor is the automated equivalent of that artefact.

The anchor doesn't just enable a comparison — it changes the compliance conversation from *"this is wrong, fix it"* to *"here is exactly what I expect, implement against it."*

---

## Key capabilities

| Capability | Bob infrastructure |
|---|---|
| Component and variant extraction from Figma | `mcp__figma-mcp__get_design_context` |
| Token/variable assignment per node | `mcp__figma-mcp__get_variable_defs` |
| Custom component identification | `mcp__figma-mcp__get_code_connect_map` |
| Carbon token resolution and compliance check | `mcp__carbon-mcp__docs_search` |
| Anchor document generation | Bob skill output (Markdown) |
| Jira ticket attachment | Jira MCP |

---

## Workflow

```
At handoff (designer-initiated):

1. Designer: "Generate a compliance anchor for this Figma frame"
   → Pastes Figma URL

2. Bob calls get_design_context(figmaURL)
   → Extracts component tree, variants, props, layout values

3. Bob calls get_variable_defs(figmaURL)
   → Extracts token assignments per node
   → Flags any hardcoded values (hex, px)

4. Bob calls get_code_connect_map(figmaURL)
   → Identifies which nodes are Carbon-connected vs. custom/detached

5. Bob calls docs_search(Carbon MCP) for each component
   → Validates: correct component for context? Correct variant?

6. Bob generates the Compliance Anchor:
   → Component inventory (Carbon-connected / custom / detached)
   → Token inventory (token-linked / hardcoded — with correct token named)
   → Spacing values (Carbon grid-aligned / off-grid)
   → Custom component flags with verbal handoff notes

7. Anchor is attached to the Jira ticket (Jira MCP)
   → Developer implements against the anchor
   → Anchor persists independent of live Figma file changes

Post-implementation (developer or designer):

8. "Check this implementation against the anchor in [Jira ticket]"
   → Bob reads anchor + compares against code branch or user screenshot
   → Returns delta: what was expected vs. what was built
```

---

## Effort estimate: M

Figma MCP tools are confirmed available. The novel work is:

- **Anchor schema design** — defining the Markdown/JSON format that captures the compliance spec in a way that is both human-readable (for the developer) and machine-parseable (for the post-implementation check)
- **Jira attachment workflow** — attaching the anchor document to the Jira ticket and retrieving it later for comparison
- **Degraded-file handling** — defining graceful fallback behaviour when `get_design_context` returns limited data (Figma files without Code Connect or token-linked variables)

Estimated build time: 2–3 weeks. No procurement. No team CI setup required.

---

## Key assumptions

- Figma files are sufficiently structured for `get_design_context` and `get_variable_defs` to return meaningful data. Teams with Code Connect and token-linked variables (Diya's API Management team) will get high-quality anchors. Teams without (Hariharan's Angular team) will get degraded but still useful output (component names, layout values, text content).
- Designers are willing to run anchor generation as a handoff step. This is a behaviour change — it requires designers to initiate the step, not developers. *Discovery needed: validate with Diya and Animesh whether this feels like overhead or relief.*
- The anchor remains a useful reference even if the Figma file changes after handoff. Staleness risk exists if the design is iterated post-anchor-generation. Mitigation: anchor includes a generation timestamp; re-generation is low-effort.
- Jira MCP can attach a Markdown document to a ticket (confirmed: Jira MCP is available in Bob; attachment mechanism needs validation for Markdown files specifically).

---

## Advantages

- **Shifts compliance left** — problems are surfaced at handoff, before the developer writes a single line of code. Reduces rework cycles (Animesh's 2-hour annotation → 2-week implementation → re-review loop).
- **Replaces verbal handoff warnings** — custom and non-Carbon components are flagged in a persistent, structured document rather than mentioned verbally and forgotten.
- **Creates a compliance record** — the anchor is an artefact that lives in Jira, independent of the Figma file and the chat transcript. It protects both the designer (who can say "the spec was clear") and the developer (who can say "I implemented against the anchor").
- **Enables traceable post-implementation comparison** — once an anchor exists, the post-implementation diff is structured (anchor vs. actuals) rather than open-ended (Figma vs. screenshot). This is a higher-signal comparison.
- **Complements Solution 1** — Screenshot Drop (Solution 1) is the post-implementation check; Annotation Anchor is the pre-implementation spec. Together they close the full handoff-to-review loop.
- **Replicates Diya's PR gate model at scale** — the API Management team's formal review gate works because there is a clear artefact. The anchor automates that artefact generation for teams that do not have Diya's process discipline.

---

## Known limitations

- **Requires designer initiation** — if designers don't run the anchor step at handoff, the workflow doesn't start. This is the primary adoption risk.
- **Degrades with Figma file quality** — teams that do not use Code Connect or token-linked variables will get less structured anchors. Hariharan's team is the at-risk case.
- **Anchor can go stale** — if the design changes after handoff, the anchor may not reflect the latest spec. Mitigation: timestamp + re-generation prompt.
- **Does not solve the visual comparison** — the anchor captures the *intended* spec; it does not perform the visual drift check itself. It enables a more structured post-implementation comparison but does not replace Solution 1 or Solution 6 for visual review.

---

## Risk evaluation

| Dimension | Score | Rationale |
|---|---|---|
| **Value** | 4 | Directly addresses handoff communication gap (Nagaraj, Animesh). Reduces annotation burden. Creates compliance record that enables traceable post-implementation diff. Score not 5: no participant explicitly named this specific workflow; value is inferred from pain points rather than stated desired outcome. |
| **Viability** | 3 | Figma MCP tools confirmed available. Anchor schema design and Jira attachment workflow are novel — not prototyped. Discovery needed: whether `get_design_context` returns sufficient data from low-maturity Figma files. |
| **Usability** | 3 | Requires designer behaviour change (new handoff step). No evidence yet that designers would adopt this willingly. Discovery needed: validate with Diya or Animesh in a 30-minute session. High confidence it solves a real problem; low confidence in adoption without validation. |
| **Feasibility** | 3 | Figma MCP tools confirmed. Anchor schema is novel design work. Staleness risk is real but mitigable. Jira Markdown attachment needs validation. Degraded output for low-maturity Figma files is an open question. |

**Overall risk profile: Medium.** High value potential but three open discovery questions that each individually could affect adoption or output quality. The usability assumption (designer willingness to add a handoff step) is the highest-impact unknown and should be the first thing validated.

---

## Recommended next steps

1. **Validate with designers first** — 30-minute session with Diya (highest-maturity team) and Animesh (highest annotation burden). Show them a prototype anchor generated from a real Figma frame and ask: does this replace your annotation work, or add to it?
2. **Test `get_design_context` on a low-maturity Figma file** (one of Hariharan's team's files) — confirm what the degraded output looks like and whether it is still useful.
3. **Validate Jira Markdown attachment** — confirm the Jira MCP can attach a Markdown document to a ticket and retrieve it later.

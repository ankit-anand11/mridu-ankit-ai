# Interview Summary: Group Discovery Session — Design-to-Dev Handoff & Carbon Compliance

**Session date:** 20 August 2026
**Duration:** ~30 minutes
**Facilitator:** Ankit Anand
**Format:** Group discovery interview (3 participants)

---

## Interviewee Context

Three product designers from IBM webMethods products participated in this session.

| Participant | Product | Tenure |
|---|---|---|
| **Nagaraj Venkatraj** | webMethods B2B | 6 years at SoftwareAG/IBM (2 years on B2B) |
| **Diya Susan Joseph** | API Management / API Studio | 4 years (2 in Control Plane, 2 in API Studio) |
| **Animesh Jain** | webMethods Integration | ~1.5 years |

All three teams exist on different points of the **Carbon compliance spectrum** — from near-full compliance (API Management) to partial/low compliance (B2B, Integration). This created a natural contrast that surfaced distinct pain points, workflows, and constraints.

---

## Key Pain Points

### 1. Carbon component gaps force custom work, which creates long-term maintenance debt

> "Since we moved from webMethods to [delight] to Carbon, we made a lot of custom components… then we moved to [Carbon]. So all those components are customised. It is not a standard component… such cases we are making our own components in the product even." — Nagaraj

> "If I introduce a new component, it is on our headache, our product's responsibility to maintain that complete component. In future, if there is any issue — for example, accessibility issues — it is our responsibility. If I am using a Carbon component, it is Carbon's responsibility." — Nagaraj

**Impact:** Teams that customise or detach Carbon components inherit long-term maintenance responsibility. Carbon upgrades (e.g., theming changes, dark mode) require manual rework across every custom component. Accessibility failures become the product team's liability, not Carbon's.
**Frequency:** Ongoing; compounds with every Carbon release.
**Severity:** High — especially for B2B and Integration who have a high density of custom components.

---

### 2. Breaking Carbon components creates a communication gap at handoff

> "Sometimes we will not tell also… they will be looking for the Carbon component and they might miss something… they will reach back to me saying that this is not the Carbon. Then I will say, I might have forgot to say." — Nagaraj

> "I have highlighted with the specific developer I am working with that these components are custom — pay special attention while you are creating the experience." — Animesh

**Impact:** Developers either spend time searching for a Carbon component that does not exist, or build incorrect implementations because they were not informed about the customisation. Rework cycles follow.
**Frequency:** Per-feature; recurs every time a component is broken.
**Severity:** High for B2B and Integration. Mitigated in API Management through stricter process.

---

### 3. Carbon documentation gaps create ambiguity when components look similar

> "There are a couple of components that are very similar and there's no very clear documentation on use cases. So I remember something we were getting confused between 2 components and how to use it and then we had to reach out to the Carbon team to explain what their exact use case was." — Diya

**Impact:** Designers cannot self-serve answers and must escalate to the Carbon team, which introduces delays. For Animesh, a single disambiguation conversation took 2 weeks to resolve.
**Frequency:** Ad hoc, but recurring whenever similar-looking components appear.
**Severity:** Medium — creates delays but is eventually resolved through Carbon team consultation.

---

### 4. Getting Carbon approval for custom components is a slow, manual process

> "All the baking that I have done of the components — that needs to be also verified at some point… if we really want to be carbon compliant, we should be doing that — also adds some time." — Animesh

> "If it is a custom, there is a lot of approval that we have to get and doing anything custom is slowing down our product very drastically. So there has to be a lot of checks before we finally build something custom." — Diya

**Impact:** Designers who want to stay Carbon-compliant with custom components must go through a manual review process with the Carbon design system team. This process is not documented, unpredictable in length, and creates a bottleneck in delivery pipelines.
**Frequency:** Per custom component; some products have very few (Diya: ~3-4 custom components total), others have many.
**Severity:** High when custom components are frequent (B2B, Integration). Lower when strictly avoiding custom work (API Management).

---

### 5. Implementation review is labour-intensive and often ad hoc

> "I had to spend like 2 hours actually annotating what all changes have to be made and that feedback was given. Then it was implemented in like 2 weeks, then it was reviewed again." — Animesh

> "Officially, we do not have an official review process — it is mostly like either started by us or the developer or both of us." — Animesh

> "It's almost like I see the actual implementation and I am like, did I design this?" — Ankit (facilitator, describing Integration specifically)

**Impact:** Without a formal design review gate, deviations from design spec accumulate silently and are caught late. Integration in particular suffers dramatic drift between design and implementation, with designers having to "chase" developers for access to review.
**Frequency:** Per feature; review burden scales with feature complexity and custom component density.
**Severity:** Critical for Integration; Major for B2B; well-managed for API Management.

---

## Workflow Insights

### Design-to-handoff process

All three teams follow roughly the same pattern:

1. Figma designs are developed against an agreed spec or Jira ticket.
2. Designs are shared via Figma link in the Jira ticket.
3. A "3-in-a-box" or alignment call is held with the development team before handoff. Often recorded as a walkthrough video.
4. Annotations are added in Figma to explain interactions, flows, and component behaviour.
5. Developers reference the Figma file or a separate delivery file (distinct from the WIP file) during implementation.
6. Back-and-forth occurs over calls or async comments as questions arise.

### Key workflow variations by team

**API Management (Diya):** Most structured. Designs precede refinement, and a refinement session with developers is used to close gaps before implementation begins. A formal PR review gate has been introduced by engineering leadership — designers must approve before any UI-touching PR is merged. Also uses biweekly visual review calls. 

**webMethods B2B (Nagaraj):** Uses a separate Figma delivery file for developers. Annotations added where needed. Review process is manual and synchronous — designers sit with developers or review shared URLs.

**webMethods Integration (Animesh):** Uses a separate component tab and a separate flow tab in Figma. Review file with side-by-side "expectation vs reality" screenshots created when deviations are significant. Review is largely informal and designer-initiated.

### Slot-based customisation as a partial bridge

Multiple participants mentioned using **Figma slots** within Carbon components as an approach to extend components without fully breaking them. However, slot usage also hits limits:

> "Using slots also gets limiting at some point even though we try to use it very extensively. There are cases where we have to break it at some point which we usually try to avoid." — Animesh

---

## Collaboration Patterns

- **Carbon team consultation** is used by all teams but at different rates. Diya's team consults before any custom work (approval required). Animesh consults for significant changes and self-approves smaller ones. Nagaraj rarely consults.
- **Developer access to Figma annotations** is an active friction point: "Some developers don't have dev access and they can't see the annotations." — Animesh. This is worked around by creating standalone summary tabs.
- **PR review integration** (Diya's team) is the most mature model described — it makes designer review a hard gate, reversing the approval dynamic so developers chase designers rather than the other way around.
- **Cross-team communication** on custom components is mostly verbal (calls) with supplementary notes, rather than embedded in the Figma file itself in a structured way.

---

## Desired Improvements

1. **A way to flag broken/custom components automatically at handoff** — so developers are not surprised during implementation and do not have to be told verbally each time.
2. **Clearer Carbon documentation for similar-looking components** — reducing the need to consult the Carbon team for use-case disambiguation.
3. **Faster Carbon approval flow for custom components** — the current process is slow and opaque; some form of self-service guidance or lighter-weight review would help.
4. **Accessibility guidance integrated into the design workflow** — rather than as an external check done only for government projects.
5. **Adoption of a formal implementation review gate** (similar to API Management's PR review model) — particularly needed for Integration, where design-to-implementation drift is severe.

---

## Role-Specific Themes

### The compliance-spectrum divide
The three teams sit at very different points on the Carbon compliance spectrum, and this fundamentally shapes every aspect of their experience — from how freely they customise components, to how they communicate with developers, to how strictly they review implementations. The API Management team's experience shows that Carbon compliance is achievable and that it actually reduces long-term effort. The B2B and Integration teams' experience shows the compounding cost of non-compliance.

### Inheritance debt from legacy design systems
Both Nagaraj and Animesh described custom components that originated in the **webMethods Delight** design system and were never cleanly migrated to Carbon. These components are now orphaned — no Carbon equivalent, no Carbon team ownership, and full maintenance burden on the product team.

---

## Notable Quotes

> "If I am using a Carbon component, it is Carbon's responsibility. If somebody pointed out any issue, I will say it is not on mine. I am using Carbon component, whatever they update, they will be automatically get rectified here. That is the main reason why developers wanted to strictly follow Carbon." — Nagaraj

> "Doing anything custom is slowing down our product very drastically. So there has to be a lot of checks before we finally build something custom." — Diya

> "Unless you approve, it can't get merged, so they will get pulled up for it. So they will do it fast so that you review it." — Diya (on the PR review gate model)

> "I see the actual implementation and I am like, did I design this?" — Ankit (on Integration's design-implementation gap)

> "It is kind of that process. Officially, we do not have an official review process — it is mostly like either started by us or the developer or both of us." — Animesh

---

## Cross-Cutting Themes

- **Process maturity:** Significant variance across teams. API Management has formalised review gates and pre-refinement alignment. Integration and B2B rely on informal, designer-driven processes. The API Management model is a replicable proof point.
- **Tool effectiveness:** Figma is universal but used inconsistently. Annotation visibility for developers is a recurring friction. No team uses automated tooling to flag component compliance or customisation state.
- **Communication clarity:** Custom components are communicated verbally and ad hoc, not as structured metadata in the Figma file or Jira ticket. This creates handoff risk.
- **Decision authority:** Whether to customise a Carbon component is made at the designer level, with inconsistent escalation to the Carbon team. There is no shared threshold or decision framework.
- **Execution predictability:** API Management's PR gate model has dramatically improved predictability by making review a hard dependency. Other teams experience variable delivery quality as a result of soft, optional review.
- **Requirements quality:** Accessibility is almost entirely absent from design requirements and acceptance criteria, with the sole exception of government-mandated projects. Even then, only specific flows are covered.

---

**Tags:** `#designer` `#webmethods` `#carbon-compliance` `#handoff` `#design-review` `#custom-components` `#accessibility`

**Sentiment:** Mixed — frustrated with current friction, but constructive and specific about what better looks like.

**Priority Themes:** Carbon component customisation debt, design-to-implementation gap, absence of formal review gates.

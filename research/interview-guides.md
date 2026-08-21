# Interview Guides — Carbon Adoption & Design-to-Implementation Gaps

## Study overview

**Goal:** Understand how IBM product designers and developers experience the
Carbon Design System adoption pipeline — from design creation through review
to implementation — and where gaps emerge, persist, or go uncorrected under
release pressure.

**Primary research questions:**

- How do IBM product designers navigate the gap between Carbon Design System
  standards and their Figma deliverables, and what factors cause them to deviate
  from Carbon patterns — especially as release timelines compress?
- What signals, tools, and processes do IBM front-end developers rely on when
  implementing Figma designs, and where do design-to-implementation gaps emerge
  before and after UI review?
- How do IBM product teams currently detect and correct Carbon compliance issues
  in the design-to-implementation pipeline, and what causes issues to reach
  production without review or remediation?

| Parameter | Decision |
|---|---|
| **Designer session format** | Group session first (3–4 participants, 60 min), followed by individual 1:1 follow-ups as needed |
| **Developer sessions** | 3-4 participants, 30 min each (individual) |
| **Recruitment** | IBM product teams actively using Carbon, shipped in last 6 months |
| **Screener criteria** | Participated in at least one design review or UI review in last 6 months |
| **Recording** | With consent; transcribe for synthesis |
| **Analysis method** | Affinity mapping → themes → JTBD job map |
| **Primary outputs** | As-is story map, pain points ranked by frequency and severity, opportunity areas for UX Reviewer |

> **Note on designer session format:** The designer team has established psychological safety
> and comfort surfacing process shortcomings together. Start with a single group session
> (3–4 participants, ~60 min) to surface systemic issues — process gaps, review cadence,
> tooling friction, and shared workarounds. Group sessions are effective here because the
> team already speaks openly about gaps; consensus findings from the group provide a strong
> baseline. Schedule individual 1:1 follow-ups (30 min each) only where a participant's
> workflow or experience needs deeper exploration beyond what the group covered.

---

## Guide 1 — Designer Group Session

**Screener:** Designers who have shipped at least one Carbon-based feature in
the last 6 months and have participated in at least one design review.

**Format:** Group session, 3–4 participants. Facilitate as a structured discussion,
not a lecture — use the questions as prompts, let participants build on each other's
answers, and note where stories diverge (those divergences are signals for 1:1 follow-up).

**Duration:** 60 minutes

**Follow-up:** After synthesis, schedule individual 1:1 sessions (30 min each) with
participants whose workflows surfaced unique patterns, edge cases, or gaps that the
group did not fully explore.

---

### Warm-up (1 min)

1. Tell me about your role and the product you're currently working on.

---

### Section A — Carbon adoption and deviation (8 min)

2. At what point in your design process does Carbon stop being enough — and what does that moment typically look like?
3. Are there parts of Carbon — specific components, spacing, tokens, typography — that you find harder to apply consistently? What makes them harder?
4. Tell me about a time the right Carbon component didn't exist or didn't fit. What did you do?

---

### Section B — Handoff: how design travels to developers (10 min)

5. How does a design typically make its way from your Figma file to a developer's hands on your team?
6. When you hand off a design that includes custom or modified components — ones that go beyond a standard Carbon pattern — how do you communicate that to the developer? What do you include, and what do you leave out?
7. How do you handle accessibility guidance in your handoff — things like focus order, labels, error states? Is that documented, communicated verbally, or assumed?

---

### Section C — Review, gaps, and release pressure (10 min)

8. Describe how design reviews work on your team — who's involved, how often, and at what stage of the release cycle.
9. What kinds of things get flagged most often? Walk me through a recent example, and how you addressed it.
10. Tell me about a feature that shipped with known Carbon gaps — or without a complete review. What were the circumstances?
11. When time is short, how do you decide what to fix versus defer? Who else is in that conversation?

---

### Wrap-up (5 min)

12. If you had a tool that gave you instant Carbon feedback on your Figma work before any human reviewer sees it — how would you use it, and what would make you trust it?
13. Anything important about your design or handoff experience I haven't asked about?

---

## Guide 2 — Developer Interview

**Screener:** Front-end developers who implement Figma designs using Carbon
React or Carbon Web Components, and who have participated in or been the
subject of a UI review in the last 6 months.

**Duration:** 30 minutes

---

### Warm-up (2 min)

1. Tell me about your role and the product you're building.

---

### Section A — Implementation process (10 min)

2. Walk me through what you do when you receive a Figma design to implement.
   Start from when you first open the file.
3. What information is typically missing or unclear in a design file that makes
   accurate implementation harder?
4. Tell me about a time the design called for something that didn't map cleanly
   to a Carbon component. What did you do?

---

### Section B — Review, correction, and release pressure (13 min)

5. What does a UI review look like from your side — who initiates it, what do
   they look at, and how do you receive feedback?
6. Describe a recent review where something was flagged. What was the gap, and
   how did you address it?
7. Have you ever shipped something you knew didn't match the design or Carbon
   standards? What were the circumstances?
8. Right now, how would you know if your implementation has drifted from the
   Figma design or from Carbon standards before a review catches it?

---

### Wrap-up (5 min)

9. If there was a way to get automated Carbon compliance feedback during
   implementation — what would you want it to tell you, and when in your
   workflow would it be most useful?
10. What's the most frustrating part of the design-to-implementation handoff
    for you?

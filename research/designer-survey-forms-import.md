# Designer Survey — Microsoft Forms Import Guide

Copy each question below into Microsoft Forms in order.
The **Form type** label tells you which question type to select.
The **Options** block is the exact text to paste or type into each choice/row field.

---

## Block 1 — Baseline

---

**Q1**
**Form type:** Choice (single answer)
**Question text:** What best describes your seniority level?
**Options:**
- Junior designer (0–2 years)
- Mid-level designer (3–5 years)
- Senior designer (6–9 years)
- Principal / Staff designer (10+ years)

---

**Q2**
**Form type:** Choice (single answer)
**Question text:** On average, how many new screens or flows do you deliver per sprint?
**Options:**
- 1–2
- 3–5
- 6–10
- More than 10

---

## Block 2 — Component difficulty

---

**Q3**
**Form type:** Likert
**Question text:** Rate your confidence using each of the following Carbon components correctly.
**Column labels:** Comfortable / Uncertain / Avoid or customise
**Rows (one per line):**
- Button
- Breadcrumb
- ComboBox
- DataTable
- DatePicker
- Form
- Modal
- Notification
- Overflow Menu
- Page Header
- Side Nav
- Side Panel
- Tab
- Tag
- Tier Sheet

> **Note:** Microsoft Forms Likert does not support a free-text "Other" row.
> Add a separate Q3b Text question immediately after: *"Are there other Carbon
> components you avoid or customise? Please list them."* (optional)

---

**Q4**
**Form type:** Choice (multiple answers)
**Question text:** For components you customise or avoid, what are the reasons? Select all that apply.
**Options:**
- Doesn't fit the use case
- Unclear which Carbon component is the right fit for the use case
- Missing variant or state
- Behaviour limitations
- Accessibility gaps
- Difficult to work with in Figma (kit configuration or customisation)
- Documentation unclear
- Other

---

**Q5**
**Form type:** Likert
**Question text:** How consistently are you able to follow Carbon guidelines in each of these domains?
**Column labels:** Always / Usually / Sometimes / Rarely / Never
**Rows (one per line):**
- Components
- Spacing & layout
- Grid
- Colour
- Typography
- Tokens
- Iconography

---

## Block 3 — Handoff completeness

---

**Q6**
**Form type:** Choice (multiple answers)
**Question text:** For a typical handoff, which of the following are consistently included in your Figma file? Select all that apply.
**Options:**
- Component states (default, focus, disabled)
- Hover states
- Error states
- Empty states
- Responsive behaviour
- Grid and layout specs
- Accessibility annotations
- Focus order
- Copy
- Nothing formal
- Other

---

**Q7**
**Form type:** Choice (single answer)
**Question text:** When you deviate from a Carbon component, how do you flag that in the handoff?
**Options:**
- I annotate it explicitly in Figma
- I mention it verbally during a walkthrough
- I expect the developer to figure it out
- I don't flag it
- It depends

---

**Q8**
**Form type:** Likert (single row) or Rating (1–5)
**Question text:** How often does a developer come back with questions your handoff didn't answer?
**Scale labels:** Never / Rarely / Sometimes / Often / Very often

> **Tip:** Use a single-row Likert or a Rating question set to 5 points.
> Label point 1 as "Never" and point 5 as "Very often".

---

**Q9**
**Form type:** Choice (multiple answers)
**Question text:** What do developers most commonly ask about after receiving your designs? Select all that apply.
**Options:**
- Component behaviour
- Spacing details
- Accessibility
- States
- Carbon compliance
- Other

---

## Block 4 — Self-assessment

---

**Q10**
**Form type:** Likert (single row) or Rating (1–5)
**Question text:** How confident are you that your Figma deliverables are Carbon-compliant before handoff?
**Scale labels:** Not at all confident / Slightly confident / Moderately confident / Very confident / Completely confident

---

**Q11**
**Form type:** Likert (single row) or Rating (1–5)
**Question text:** How often do you discover a Carbon gap in your own design after handoff or review?
**Scale labels:** Never / Rarely / Sometimes / Often / Very often

---

**Q12**
**Form type:** Choice (multiple answers)
**Question text:** Who typically catches Carbon compliance issues in your work? Select all that apply.
**Options:**
- Me before handoff
- Peer designer
- Developer during implementation
- UI review
- Reaches production uncaught
- Other

---

## Block 5 — Decision making

---

**Q13**
**Form type:** Choice (single answer)
**Question text:** When a Carbon gap is identified late, who decides whether to fix or defer?
**Options:**
- Me
- Design lead
- Product manager
- Developer
- It's a group call
- No one explicitly decides

---

**Q14**
**Form type:** Choice (single answer)
**Question text:** What most commonly causes a Carbon issue to reach production unresolved?
**Options:**
- Time pressure
- Low visibility — the gap wasn't noticed
- No clear owner
- No formal review process
- Reviewer availability
- Other

---

## Block 6 — Open field

---

**Q15**
**Form type:** Text (long answer)
**Required:** No (mark as optional)
**Question text:** Which Carbon component or pattern do you wish had better documentation, more variants, or clearer guidance?

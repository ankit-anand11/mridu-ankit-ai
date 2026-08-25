# Opportunity Backlog — UX Reviewer
**Technique:** Opportunity tree
**Sources:** interview-findings.md, interview-summary-designer-group-discovery-webmethods.md, synthesis.md, PROJECT-OVERVIEW.md
**Date:** August 2026

---

## Business Objective

> Empower IBM product teams to build consistently high-quality, accessible, and Carbon-compliant experiences by providing automated UX review and design-to-development validation at scale.

IBM product teams today lack an automated, objective way to continuously evaluate whether a design or implemented experience adheres to Carbon Design System standards, accessibility requirements, and intended design specifications. Manual review is time-consuming, dependent on individual expertise, performed late in the lifecycle, and inconsistent across teams — leading to accumulated UX debt, design system violations, and implementation drift that damages user experience and increases maintenance costs.

---

## Product Outcomes

### PO1 — Carbon compliance adoption increases measurably across IBM product teams

**Measurable behaviour:** More IBM designers and developers are catching and correcting Carbon violations before code merges. Teams that currently rely on hex fallbacks, custom components, and no review gate move toward token-based, Carbon-standard implementations.

**Target metric:** 40% reduction in Carbon violations found in post-merge QA, measured against a pre-tool baseline on the pilot team. Carbon token adoption rate in scanned branches rises from observed baseline (approx. 0% for Integration, ~80% for API) toward ≥90% across pilot teams within one quarter.

**Connection to business objective:** The business objective is scaled compliance across IBM products. This outcome is the first-order signal that the product is working — teams cannot "build consistently high-quality Carbon-compliant experiences" without first being able to detect and correct deviations reliably and early.

---

### PO2 — Design-to-implementation review cycle time drops significantly

**Measurable behaviour:** Designers spend less time manually annotating implementation deviations. Developers receive structured, actionable compliance findings before PR review rather than receiving undifferentiated feedback after the fact. Review conversations move from "this is wrong" to "fix these three specific items."

**Target metric:** 60% reduction in time spent by designers on post-implementation review (from Animesh's observed 2-hour annotation sessions toward under 30 minutes), and a 50% reduction in PR review cycles caused by design-system rework.

**Connection to business objective:** The business objective explicitly targets design-to-development validation at scale. This outcome measures whether the tool is actually compressing the compliance feedback loop — the core mechanism by which UX debt accumulates or is prevented.

---

### PO3 — Compliance becomes a verifiable, team-portable gate — not an individual expert's judgement

**Measurable behaviour:** Teams with no formal review process (Integration, B2B) adopt UX Reviewer as a pre-merge compliance check, producing a report artefact on every UI-touching PR. The dependency on individual process maturity (Senthil's rules file, Diya's PR gate) is replaced by a shared, repeatable tool that any team can invoke.

**Target metric:** At least 2 additional IBM webMethods teams adopt UX Reviewer-generated compliance reports as part of their PR process within the first two quarters post-launch. The Integration team moves from 0 formal review gates to at least 1 tool-supported gate per sprint.

**Connection to business objective:** The vision calls for compliance that scales. Today it scales only as far as individual champions can take it. This outcome measures whether the tool has broken that dependency — making compliance portable and institutional rather than personal.

---

## Customer Opportunities

### CO1 — Developers need to know, before they commit, whether their code uses Carbon tokens — not just Carbon-looking styles

**Unmet need:** Developers need an automated signal that distinguishes genuine Carbon token usage from visually similar hardcoded values. The visual output of `color: #0f62fe` and `color: $interactive-01` looks identical in a browser — but one breaks under theme changes and is not Carbon compliant. No current tool, process, or human review catches this reliably.

**Supporting evidence:**
> *"If they are really using the Carbon component, are they really using the tokens? No one has any idea. So that gap is still there."*
> — Senthil Kumaran Pattabiraman, Senior Developer / Tech Lead, API

> *"It would mainly be for the backgrounds — say the error background. It would be a bit time saving, but also we wouldn't have found the exact code for the colour and we would have proceeded with the hex code."*
> — Sahana S, Frontend Developer, Integration

**User segments affected:** Frontend developers across all maturity levels — most acutely Sahana (mid-maturity, acknowledged hex fallback habit) and Hariharan (low-maturity, no token awareness). Even Senthil's team, the most mature, identifies this as the residual gap they cannot close with human review alone.

**Current workarounds:**
- Sahana: Copies hex values from Figma Inspect and treats it as "close enough." No detection mechanism exists.
- Senthil: Writes a Bob AI PDLC rules file instructing Bob not to use hex values — effective only for Bob-generated code, not developer-written code.
- Hariharan: No workaround; the problem is entirely invisible to him.

**Competitive gap:** Every competitive tool surveyed (FigmaLint, Chromatic, Supernova, Tokens Studio, Zeroheight) operates on either Figma or code in isolation. None detect hardcoded hex or px values in code and map them to the correct Carbon token with a named fix. This is confirmed Gap G1 in the competitive analysis.

**How meeting this need drives outcomes:** Directly supports PO1 (Carbon compliance adoption) by surfacing the most silent and widespread violation across all teams. Satisfies U3 (automated detection of hardcoded values) and closes a gap Sahana admitted is "common" across her team.

---

### CO2 — Designers need handoff to flag broken or custom components automatically — not verbally, and not just once

**Unmet need:** When a Carbon component has been customised or detached, developers have no reliable way to know from the Figma file itself. Today the signal is a verbal mention during a handoff call — easily missed, not recorded, and not scalable across multiple developers or features. The absence of this signal causes rework cycles, incorrect implementations, and accumulating maintenance debt.

**Supporting evidence:**
> *"Sometimes we will not tell also… they will be looking for the Carbon component and they might miss something… they will reach back to me saying that this is not the Carbon. Then I will say, I might have forgot to say."*
> — Nagaraj Venkatraj, Designer, webMethods B2B

> *"I have highlighted with the specific developer I am working with that these components are custom — pay special attention while you are creating the experience."*
> — Animesh Jain, Designer, webMethods Integration

> *"If I introduce a new component, it is on our headache, our product's responsibility to maintain that complete component. In future, if there is any issue — for example, accessibility issues — it is our responsibility."*
> — Nagaraj Venkatraj, Designer, webMethods B2B

**User segments affected:** Both designers (who carry the cognitive burden of remembering and communicating customisation) and developers (who waste implementation time searching for a non-existent Carbon component or building something incorrect). Severest impact on B2B and Integration teams, which have a high density of Delight-era custom components.

**Current workarounds:**
- Nagaraj: Verbal mention during handoff calls; acknowledged as unreliable.
- Animesh: Direct conversation with the specific developer; creates a single point of failure when developers change.
- Diya: Consults Carbon team before any custom work and keeps custom components to a minimum (~3–4 total). Avoidance, not detection.

**Competitive gap:** No surveyed tool detects custom or non-Carbon components in a Figma frame and surfaces them with a named Carbon replacement. FigmaLint detects detached instances in Figma but does not suggest Carbon equivalents. This is confirmed Gap G2 in the competitive analysis.

**How meeting this need drives outcomes:** Supports PO2 (review cycle reduction) by eliminating the most common source of post-implementation rework — developer discovery that a component they built doesn't exist in Carbon. Supports PO3 (portable compliance gate) by embedding the custom-component signal in the artefact rather than in a person.

---

### CO3 — Developers and tech leads need to run a compliance check themselves, before PR review, without depending on a designer's availability

**Unmet need:** Developers currently cannot initiate a compliance check without involving a designer or waiting for a QA cycle. There is no self-service path to produce a compliance artefact before a PR is opened. This means compliance findings arrive either too late (post-merge QA) or not at all. Teams that want a pre-merge gate cannot implement one without a tool to generate the evidence.

**Supporting evidence:**
> *"The moment I know this developer has worked on this feature, I can get the branch information from them. I can just put it on the tool and run it. I don't have to ask them — I can run it by myself and generate the report, create the ticket, assign it back to them."*
> — Senthil Kumaran Pattabiraman, Senior Developer / Tech Lead, API

> *"I will be manually checking if it is matching the Figma mockup and maybe after my check, I want this compliance check to run."*
> — Hariharan SV, Frontend Developer, Integration

> *"Currently, they are not even taking that responsibility or ownership."*
> — Senthil Kumaran Pattabiraman, on the absence of accountability in the Integration team

**User segments affected:** Tech leads who want to verify their team's output without being the bottleneck (Senthil). Developers who want a self-service gate before a code review (Hariharan). Product teams that have no formal review process and need one without building it from cultural scratch.

**Current workarounds:**
- Senthil: Mandatory screen-recording video attached to every UI-touching PR, reviewed by designers who pause and scan for gaps. Catches visual deviations but not token or component compliance.
- Hariharan: Manual screenshot-to-Bob iteration (2–3 cycles) before submitting code. Approximate, slow, and dependent on visual similarity rather than compliance.
- Integration team broadly: No workaround — non-compliant code merges with no accountability, surfaces in QA or not at all.

**Competitive gap:** Chromatic provides a PR-level visual regression gate, but it is not Carbon-aware — it cannot distinguish a Carbon `Button` from a custom button that looks identical. No tool provides a Carbon-specific pre-merge compliance gate. Confirmed Gap G3 in the competitive analysis.

**How meeting this need drives outcomes:** Directly supports PO3 (compliance as a portable gate) — this opportunity is the mechanism that makes a pre-merge gate possible for any team, regardless of process maturity. Also drives PO1 by moving the catch-point for violations earlier in the cycle, where they are cheapest to fix.

---

### CO4 — Designers need a visual diff between what was designed and what was actually built — with a Carbon-aware explanation of the gap

**Unmet need:** After implementation, designers have no tool to quickly and objectively compare a live build against its Figma source of truth. The only current method is manual side-by-side comparison, which is time-consuming, subjective, and catches only visually obvious drift. It misses token-level deviations entirely and cannot attribute the gap to a specific Carbon violation.

**Supporting evidence:**
> *"I had to spend like 2 hours actually annotating what all changes have to be made and that feedback was given. Then it was implemented in like 2 weeks, then it was reviewed again."*
> — Animesh Jain, Designer, webMethods Integration

> *"It's almost like I see the actual implementation and I am like, did I design this?"*
> — Ankit Anand, Designer / Facilitator (describing Integration's design-implementation gap)

> *"There is a skill that actually evaluates — to get the styling part from the Figma. Maybe we could utilise it by connecting and comparing with Figma and identifying the delta."*
> — Hariharan SV, Frontend Developer, Integration

> *"You can pass in the branch information… ask Bob to run the scan."*
> — Senthil Kumaran Pattabiraman, Senior Developer / Tech Lead, API

**User segments affected:** Designers across all three teams, most severely Integration (Animesh) where visual drift is dramatic. Tech leads who audit feature branches before or after merge. Product owners who need a shareable compliance record for governance.

**Current workarounds:**
- Animesh: Creates a side-by-side "expectation vs reality" screenshot document inside Figma, then annotates deviations manually. Takes 2+ hours per feature.
- Senthil: Screen recording video attached to PR; designers manually pause and inspect. Catches layout deviations, not token or component compliance.
- Nagaraj: Sits with developers synchronously during review. Blocks both designer and developer for the review duration.

**Competitive gap:** Every surveyed tool operates on one side of the Figma/code boundary — none provide a cross-boundary delta. Applitools and Chromatic provide visual regression between builds, not Figma-to-implementation. Confirmed Gap G4 in the competitive analysis — described by both Hariharan and Senthil as the most valuable missing capability.

**How meeting this need drives outcomes:** Directly targets PO2 (review cycle reduction) — this is the opportunity that compresses Animesh's 2-hour annotation sessions. Also supports PO3 by producing an objective, shareable compliance artefact that replaces a designer's subjective verbal feedback.

---

### CO5 — Teams need compliance findings to become actionable tickets automatically — so nothing is lost between the report and the fix

**Unmet need:** Even when a compliance problem is identified, the path from finding to fix is manual: a designer writes feedback, a developer creates a Jira ticket, acceptance criteria are written from memory, Bob is invoked to fix it. Every manual step is a point where context is lost, severity is softened, or the ticket is never created. Teams need the compliance report to automatically produce a structured Jira ticket with acceptance criteria precise enough for Bob to act on.

**Supporting evidence:**
> *"Ask it to create a report itself and attach that report as a description in a Jira ticket… there will be acceptance criteria — that also you can ask Bob to coin it according to your rules and expectations. If the ticket has that information, that is more than enough for Bob to run this and fix the code as well."*
> — Senthil Kumaran Pattabiraman, Senior Developer / Tech Lead, API

> *"Bob is going to offer them the solution as well. So they will just say yes, go ahead and fix it, and Bob will fix it happily."*
> — Senthil Kumaran Pattabiraman

**User segments affected:** Tech leads who currently chase developers for fixes without a documented artefact (Senthil's aspiration). Product owners who need compliance evidence for governance and OKR reporting. Developers who benefit from structured, actionable tickets over vague "this looks wrong" feedback.

**Current workarounds:**
- Senthil: Manually copies review notes into Jira after a video review. Process takes additional time and loses structured metadata.
- Animesh: 2-hour annotation session produces Figma comments, not Jira tickets — developers must manually translate.
- Most teams: Compliance findings are verbal or async comments in Figma; no persistent, tracked record.

**Competitive gap:** None of the five surveyed competitive tools integrates with Jira to auto-create tickets from compliance findings. This capability does not exist in any tool in the market. Confirmed Gap G5 in the competitive analysis.

**How meeting this need drives outcomes:** Completes the loop for PO1 (adoption) and PO2 (cycle time) — without auto-ticket creation, findings can be ignored or lost. Also supports PO3 (portable gate) by producing a persistent compliance record that creates accountability. This opportunity is the downstream amplifier: it converts a compliance report from an advisory output into a trackable work item with an owner.

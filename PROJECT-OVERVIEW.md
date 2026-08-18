# PROJECT-OVERVIEW.md — Business Context and Goals

## Problem statement

Design systems like Carbon provide standards for components, spacing,
typography, color usage, accessibility, and interaction patterns. However, as
IBM products scale and multiple designers and developers contribute across
teams, inconsistencies emerge between:

- Figma designs and Carbon standards
- Approved designs and implemented experiences
- Individual screens and the broader product experience
- Accessibility requirements and final execution

Today, identifying these issues requires manual UX reviews, design audits,
accessibility checks, and design-development comparisons. This process is:

- Time-consuming and difficult to scale
- Dependent on individual reviewer expertise
- Often performed late in the development lifecycle
- Prone to human oversight
- Inconsistent across teams and products

As a result, IBM products accumulate UX debt, design system violations,
accessibility gaps, visual inconsistencies, and implementation drift that
negatively impact user experience and increase maintenance costs.

---

## Core challenge

IBM product teams lack an automated and objective way to continuously evaluate
whether a design or implemented experience adheres to Carbon Design System
standards, accessibility requirements, and intended design specifications.

---

## Vision

**UX Reviewer** is an AI-powered design quality assistant that automatically
analyses Figma files and implemented experiences to identify deviations from
Carbon Design System standards, accessibility requirements, and design best
practices — before they reach users.

UX Reviewer acts as a virtual design system expert, accessibility specialist,
and UX reviewer that provides continuous feedback throughout the product
development lifecycle.

### Vision statement

> Empower IBM product teams to build consistently high-quality, accessible, and
> Carbon-compliant experiences by providing automated UX review and
> design-to-development validation at scale.

---

## Target users

| User | Primary need |
|---|---|
| **IBM designers** | Fast Carbon compliance feedback without waiting for a design review cycle |
| **IBM developers** | Clear signal on whether an implementation matches the approved design and Carbon standards |
| **Product owners / leads** | Shareable audit reports for design reviews, OKR tracking, and UX debt visibility |

This is an **IBM-internal tool**. Users are IBM product teams building on
Carbon. It is not scoped for external Carbon adopters in v1.

---

## What UX Reviewer analyses

### 1. Carbon compliance
- Incorrect component usage
- Custom components where Carbon components exist
- Component variants not aligned with standards
- Improper interaction patterns
- Unsupported design patterns

### 2. Layout and spacing
- Inconsistent spacing against Carbon's 8px grid
- Grid violations
- Misalignment and layout imbalance
- Hardcoded padding and margin values (not from spacing tokens)

### 3. Typography
- Typeface usage (IBM Plex required)
- Type scale adherence
- Font weights and line heights
- Text hierarchy consistency
- Carbon typography token compliance

### 4. Color and theming
- Color token usage vs. hardcoded hex values
- Theme compliance (White, Gray 10, Gray 90, Gray 100)
- Unsupported custom colors

### 5. Accessibility (Carbon pattern level)
- Missing focus considerations in interactive patterns
- Inconsistent semantic structure against Carbon patterns
- Accessible name and label concerns
- Carbon accessibility pattern violations
> Note: Mechanical WCAG testing (contrast ratios, axe rules) is delegated
> to IBM Equal Access Checker. UX Reviewer covers Carbon-pattern-level
> accessibility only.

### 6. Design consistency
- Duplicate or competing interaction models within a flow
- Inconsistent terminology
- Visual inconsistency across screens
- Drift from established product patterns

### 7. Design-to-implementation comparison
- Visual drift between Figma design and rendered implementation
- Spacing and typography deviations
- Missing states or incorrect component implementation

---

## What UX Reviewer does NOT do

- Modify Figma files or codebases
- Replace manual UX reviews for complex interaction decisions
- Provide definitive WCAG pass/fail verdicts (use IBM Equal Access Checker)
- Run continuous background scans without user initiation
- Replace Applitools or Chromatic for CI-integrated visual regression

---

## Success outcomes

### For designers
- Faster pre-review feedback
- Reduced manual auditing effort
- Higher Carbon adoption rate
- Lower UX debt accumulation

### For developers
- Clear implementation guidance against Carbon standards
- Early defect detection before QA
- Reduced rework from design review rejections

### For product teams
- Consistent user experiences across products
- Improved accessibility compliance
- Shareable compliance reports for design governance
- Faster release cycles with fewer late-stage design changes

---

## Market context

### Tools IBM employees can use today (no procurement required)

| Tool | What it covers |
|---|---|
| Figma native AI accessibility checker | Contrast, touch targets, color blindness (Figma canvas only) |
| IBM Equal Access Checker (browser extension) | WCAG mechanical checking on live pages |
| IBM Accessibility Design Kit for Figma | Checklists and handoff guidance |
| Figma Library Analytics | Component and variable adoption metrics |
| Carbon MCP | Live queryable Carbon knowledge base for AI assistants |

### The confirmed gap

None of the above tools provide:
- Carbon usage-guideline compliance (correct component *for the context*, correct variant, correct interaction pattern)
- Unified Carbon report spanning Figma + implementation
- Carbon-aware interpretation of visual drift findings

This gap is what UX Reviewer fills.

### Competitive tools (require procurement or not IBM-specific)

| Tool | Capability | Limitation for IBM |
|---|---|---|
| Applitools Eyes | Design-to-code visual comparison with Figma plugin | Not Carbon-aware; requires procurement |
| Chromatic | Storybook visual regression | Component-level only; not Carbon-aware |
| OverlayQA / Pixelay | Figma-to-browser visual overlay | No Carbon knowledge; manual interpretation |
| onBeacon / ClarityUX | AI design review in Figma | Generic best practices; no Carbon specificity |
| Omlet | Code-level component adoption tracking | No Figma analysis; no Carbon compliance |

---

## Delivery model

UX Reviewer is delivered as a **Bob skill** — a capability extension of IBM's
AI assistant. Users interact with it via natural language in Bob, passing
Figma URLs and optionally implementation screenshots or URLs.

**Interaction model:** On-demand. Designers and developers initiate a review
when they choose. The output is a structured Markdown report that can be
shared, acted on, or brought to a design review.

**No new tools to learn.** No subscriptions. No separate dashboard. Works
where IBM teams already work.

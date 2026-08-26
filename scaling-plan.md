# UX Reviewer — MVP & Scaling Plan
**Prepared for:** Friday showcase
**Authors:** Mridusmita Nath, Ankit Anand
**Date:** August 2026

---

## The problem in one line

IBM product teams have no automated way to check whether a design or
implementation follows Carbon standards — so violations accumulate silently
and surface late, when they are most expensive to fix.

---

## What we built for MVP

UX Reviewer is a Bob skill. A designer or developer starts a conversation,
shares two screenshots, and gets back a structured compliance report in
under a minute — with a specific Carbon fix for every finding.

**The MVP does exactly three things:**

| Step | What happens |
|---|---|
| 1 | User shares a Figma screenshot (or URL) and a dev screenshot |
| 2 | Bob analyses both against Carbon v11 standards using Carbon MCP and AI vision |
| 3 | Bob generates a downloadable HTML report with every finding, its severity, and an inline Carbon fix example |

**No new tools. No plugins. No procurement. No setup.**
It works in the same Bob conversation IBM teams already use.

---

## What the MVP report contains

Every report covers six areas and is downloadable as an HTML file:

| Section | What it flags |
|---|---|
| **Carbon Compliance** | Custom components where a Carbon one exists; wrong variants; deprecated patterns |
| **Token & Spacing** | Hardcoded hex colours and px values where Carbon tokens should be used |
| **Typography** | Non-IBM Plex fonts; sizes off the Carbon type scale; hardcoded values |
| **Accessibility** | Missing focus indicators; icon buttons without labels; form inputs without labels |
| **Handoff Completeness** | Interactive components missing hover, focus, or error states |
| **Design-to-Dev Comparison** | Visual drift between the Figma design and the live build |

Every finding includes:
- **Severity** — Critical / Major / Minor
- **What was found** — exact description with component or layer reference
- **Carbon standard violated** — with link to Carbon docs
- **Inline fix example** — exact Carbon component, token, or import to use

---

## Severity levels

| | Definition | Example |
|---|---|---|
| 🔴 **Critical** | Breaks a core Carbon pattern or creates an accessibility barrier | Custom dropdown instead of Carbon `<Dropdown>`; button with no focus ring |
| 🟠 **Major** | Deviates from Carbon standards; creates visual or behavioural inconsistency | Spacing hardcoded as `20px` instead of `$spacing-06`; wrong component variant |
| 🟡 **Minor** | Improvement opportunity; does not violate Carbon standards | Suboptimal component choice; spacing on the 8px grid but not tokenised |

---

## What the MVP does NOT do

Being clear about scope is as important as what it does.

- Does not run automated WCAG checks — IBM Equal Access Checker handles those
- Does not modify Figma files or codebases
- Does not run continuously in the background — it is on-demand, user-initiated
- Does not require Code Connect to be set up (but produces higher-accuracy
  results when it is)
- Does not create Jira tickets automatically — the user decides after seeing
  the report

---

## How it scales — the three-phase roadmap

### Phase 1 — MVP (now, no procurement required)

**Stack:** Bob + Carbon MCP + Figma MCP + Claude vision

**What it covers:**
- Screenshot-to-screenshot comparison
- Carbon component identification via AI vision and Code Connect
- Token and spacing validation via `get_variable_defs`
- Downloadable HTML report with inline fix examples
- User-initiated Jira ticket creation from findings

**User workflow:** Single Bob conversation, two screenshots, one report.

**Who can use it today:** Any IBM designer or developer with Bob access.

---

### Phase 2 — Code branch scanning (no procurement required)

**Adds:** Developers can share a GitHub branch link instead of a screenshot.
Bob reads the source files directly and flags:
- Non-Carbon component imports (catches the silent failure where Bob or a
  developer reused a legacy component from an existing codebase)
- Hardcoded hex and px values in SCSS/CSS that should be Carbon tokens
- Missing `pkg.component.X = true` flags for IBM Products components

**Stack:** Bob file reading + Carbon MCP `code_search` +
`stylelint-plugin-carbon-tokens`

**Why it matters:** Token violations are invisible to visual review — a screen
can look correct while the underlying code uses `#0f62fe` instead of
`$interactive-01`. Phase 2 catches this class of violation that Phase 1
cannot see.

**Pre-requisite:** None. Works on any GitHub repo the user can share.

---

### Phase 3 — Pixel-precise CI comparison (no procurement required)

**Adds:** A Playwright script (generated and maintained by Bob) that runs in
the team's CI pipeline, extracts computed CSS values from the live build, and
compares them element-by-element against the Figma spec.

**Output example:**
```
Element          Figma spec   Rendered    Delta
Heading size     24px         28px        +4px ← use $productive-heading-03
Button padding   16px         12px        -4px ← use $spacing-05
Row gap          8px          10px        +2px ← use $spacing-03
```

Bob interprets the delta in Carbon terms — not just "it's different"
but "this means the button is using `$spacing-02` instead of `$spacing-03`."

**Why it matters:** This closes the sub-4px gap that AI vision cannot reliably
catch, and produces an exact compliance record that can be attached to a PR.

**Pre-requisite:** Team has a Storybook or staging environment. Bob generates
the Playwright script; team wires it into their CI pipeline (one-time setup).

---

### Phase 4 — Enterprise visual regression gate (procurement decision)

**Adds:** Applitools Eyes for CI-integrated visual regression with Figma
as the baseline. Cross-browser, cross-device, with a collaborative dashboard
for design/dev/QA sign-off.

**What Applitools adds over Phase 3:** AI noise filtering to suppress
false positives; no custom scripting; enterprise dashboard with role-based
access.

**What it still does not add:** Carbon awareness. Applitools detects
*that* something looks different from the design; it does not know *whether*
the design or the implementation violates Carbon standards. UX Reviewer
complements Applitools; it does not replace it.

**Status:** Requires procurement. No confirmed IBM enterprise license.
Evaluated separately from the Bob skill.

---

## Roadmap summary

```
Phase 1 — MVP                    Phase 2                 Phase 3                  Phase 4
Screenshot comparison     →   Code branch scan    →   CI Playwright delta   →   Applitools gate
HTML report + fix examples    Non-Carbon imports      Pixel-precise delta        Enterprise scale
Jira ticket offer             Token check in code     Bob interprets output      Procurement needed
────────────────────────────────────────────────────────────────────────────────────────────────
Available today               Available today         Requires CI setup          Requires procurement
No setup needed               No setup needed         (~1 sprint to wire up)
```

---

## Why this is defensible

Every commercial tool in the market is design-system-agnostic. Their business
model requires them to work for *any* design system — so they cannot ship
Carbon-specific rules, token names, or component recommendations.

UX Reviewer is IBM-internal and Carbon-specific by design. That is not a
limitation — it is the entire advantage.

| | Market tools | UX Reviewer |
|---|---|---|
| Rule source | Team-configured, goes stale | Carbon MCP — live, maintained by the Carbon team |
| Component knowledge | Generic abstractions | Carbon's full component inventory and variant rules |
| Token knowledge | Whatever the team loaded | Carbon's full token taxonomy and semantic intent |
| Web Component alternatives | Not provided | Carbon Web Components named for every non-Carbon import |
| Jira integration | Not available in any surveyed tool | Built-in via Jira MCP |
| Procurement | Most require it | Zero — runs through Bob |
| Learning curve | Plugins, dashboards, onboarding | Zero — same Bob conversation the team already uses |

---

## The pilot plan

**Recommended first team:** Senthil's API team (webMethods).

Why: Highest Carbon maturity, most articulate about what the tool should do,
and the only team with an existing PR review gate to measure against.

**What the pilot looks like:**

1. Run UX Reviewer on one real Figma frame from the API team's current sprint
2. Senthil reviews the output — does it match what he would catch manually?
3. Adjust report format based on feedback (one iteration session, ~30 min)
4. Run on one PR in progress — generate a report and show Jira ticket output
5. Measure: findings per screen, findings that become tickets, tickets closed
   before merge

**Success signal:** Senthil can run a compliance check on a branch himself,
without waiting for a designer, and the output is specific enough for a
developer to act on without a follow-up conversation.

---

## The one ask for Friday

> Run UX Reviewer on one real sprint item with the API team.
> One frame. One report. One Jira ticket.
> That is the proof of concept.

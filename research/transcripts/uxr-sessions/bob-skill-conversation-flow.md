# UX Reviewer — Bob Skill Conversation Flow + Live Demo Script

## Overview

UX Reviewer is triggered conversationally inside Bob.  
The user never has to know which MCP tools are running — Bob handles everything.  
The flow has **3 phases**: intake → scan → report + action.

---

## Trigger phrases (Bob recognises any of these)

- "I want to run a UI review"
- "Review my design"
- "Check Carbon compliance"
- "Run a UX review"
- "Does my design match the implementation?"

---

## Conversation Flow (turn-by-turn)

---

### TURN 1 — Bob introduces the skill

**User says:**
> "I want to run a UI review"

**Bob replies:**
```
Sure! I'll compare your Figma design against Carbon standards
and your implementation (if you have one).

This takes about a minute. Let's go.

👉 First — share your Figma link or paste a screenshot of the screen
   you want reviewed.
```

*Behind the scenes: nothing yet. Bob is just setting expectations.*

---

### TURN 2 — User shares Figma input

**User says (option A — link):**
> "https://www.figma.com/design/abc123/MyProduct?node-id=12-34"

**User says (option B — screenshot):**
> *(pastes image)*

**Bob replies:**
```
Got it. Pulling your design now...
```

*Behind the scenes (option A):*
- `figma-mcp get_metadata` → layer tree
- `figma-mcp get_screenshot` → visual render
- `figma-mcp get_variable_defs` → token assignments
- `figma-mcp get_design_context` → component context + reference code

*Behind the scenes (option B):*
- Claude vision analyses the screenshot
- Carbon MCP docs_search validates component patterns against findings

**Bob replies (after scan):**
```
Design loaded ✓  — I can see [N] layers across [M] components.

Now, do you have a dev implementation to compare against?
You can share:
  • A GitHub link to the component / page
  • A screenshot of the live/staged UI
  • Or skip this step to get a design-only Carbon review
```

---

### TURN 3 — User shares dev input (or skips)

**User says (option A — repo link):**
> "https://github.com/ibm/myproduct/blob/main/src/components/Header.tsx"

**User says (option B — screenshot):**
> *(pastes screenshot of live app)*

**User says (option C — skip):**
> "Just check the design for now"

**Bob replies:**
```
Perfect. Running the full scan now — I'll check:
  ✦ Carbon component usage
  ✦ Design tokens (colour, spacing, typography)
  ✦ Design-to-implementation delta  ← (skipped if no dev input)
  ✦ Accessibility flags (Carbon pattern level)

Give me a moment...
```

*Behind the scenes:*
- Carbon MCP `docs_search` → validates each component pattern
- Carbon MCP `code_search` → checks correct Carbon component exists for pattern
- Figma MCP `get_variable_defs` → flags hardcoded hex/px vs token names
- Claude vision (if screenshot) → pixel-level comparison to Figma render
- Carbon MCP `code_search` (if repo link) → checks token usage in code

---

### TURN 4 — Bob delivers the report

**Bob replies:**
```
## UX Review Report — [Screen name] · [date]

### Summary
Found 8 findings: 2 Critical · 3 Major · 3 Minor

---

### 🔴 Critical (2)

1. **Custom dropdown** detected — replace with `<Dropdown>` from @carbon/react
   Token used: none (custom CSS `border: 1px solid #8d8d8d`)
   Carbon standard: use `$border-subtle-01` token
   → Fix in Figma: swap to Carbon Dropdown component
   → Fix in code: import Dropdown from '@carbon/react'

2. **Interactive element unreachable by keyboard**
   The "Filter" button has no visible focus ring
   Carbon standard: all interactive elements must use `$focus` token
   → Fix: add `--cds-focus` token to button :focus-visible

---

### 🟠 Major (3)

3. Spacing between cards is 20px hardcoded — should be `$spacing-05` (16px)
4. Body text uses `font-size: 14px` — should be `$body-compact-01` type token
5. Icon-only button missing `iconDescription` prop (Carbon a11y requirement)

---

### 🟡 Minor (3)

6. Modal close button is left-aligned — Carbon pattern places it top-right
7. Table row hover state uses #e8e8e8 — should be `$layer-hover-01`
8. Empty state illustration is not from the Carbon pictogram library

---

### Design-to-Implementation Delta
⚠ 3 discrepancies found vs your dev screenshot:
  • Figma: Blue-60 primary button / Dev: Blue-70 (wrong token)
  • Figma: 48px header height / Dev: 56px (extra padding)
  • Figma: Tag component / Dev: custom pill (non-Carbon)

---

Want me to:
  [A] Create Jira tickets for the Critical findings
  [B] Export this report as Markdown
  [C] Show fix examples for any finding
  [D] Done for now
```

---

### TURN 5 — User picks an action

**User says:**
> "A"  or  "Create the Jira tickets"

**Bob replies:**
```
Creating 2 Jira tickets in [PROJECT-KEY]...

✓ Ticket created: PROJECT-1042
  Title: [UX Review] Replace custom dropdown with Carbon Dropdown
  Priority: Critical | Component: Header | Sprint: Current

✓ Ticket created: PROJECT-1043
  Title: [UX Review] Add focus ring to Filter button — keyboard a11y
  Priority: Critical | Component: Filter bar | Sprint: Current

Both tickets link back to this report and the Figma node.
Anything else?
```

*Behind the scenes: Jira MCP creates tickets with pre-filled fields.*

---

### TURN 5b — User asks for a fix example

**User says:**
> "Show me the fix for finding 1"

**Bob replies:**
```
Here's the Carbon fix for the custom dropdown:

Remove this (custom CSS):
  <div class="my-dropdown" style="border: 1px solid #8d8d8d">

Replace with:
  import { Dropdown } from '@carbon/react';

  <Dropdown
    id="my-dropdown"
    titleText="Select option"
    label="Choose..."
    items={items}
    itemToString={(item) => (item ? item.text : '')}
  />

Carbon Dropdown gives you tokens, keyboard nav, and a11y
out of the box — no custom CSS needed.
```

---

## Live Demo Script (8-minute showcase)

### Structure

| Segment | Time | Content |
|---|---|---|
| 1. Hook | 0:00–1:00 | The problem in one sentence |
| 2. Research evidence | 1:00–2:30 | What we heard from teams |
| 3. Live Bob demo | 2:30–6:00 | Full conversation walkthrough |
| 4. So what | 6:00–7:30 | Impact + next steps |
| 5. Ask | 7:30–8:00 | One clear ask from audience |

---

### Segment 1 — Hook (1 min)

> "Every IBM product team knows Carbon. But every day, buttons ship as
> custom divs, spacing is hard-coded as 20px, and colours live as hex values
> in CSS files. Nobody catches it because there's no review gate.
> UX Reviewer is the gate."

---

### Segment 2 — Research evidence (90 sec)

> "We interviewed 3 developer teams and 1 designer group in webMethods.
>
> Sahana's team uses Carbon React but falls back to hex colours when
> a token 'doesn't look right'. Hariharan's Angular team uses PrimeNG —
> not Carbon at all. Senthil's API team has a PR gate and AI PDLC rules.
> They have zero Carbon violations. That's the benchmark we're designing for.
>
> Five existing tools — Chromatic, Supernova, Tokens Studio, FigmaLint,
> Zeroheight — were checked. None of them close any of the 6 gaps we found
> for Carbon. There is a clear space here."

---

### Segment 3 — Live Bob demo (3.5 min)

**Narrator says:**
> "Here's UX Reviewer running live inside Bob right now.
> No staging environment. No prototype. Real Figma URL."

**Demo steps (run live in Bob):**

1. Type: *"I want to run a UI review"*
   → Bob asks for Figma link

2. Paste a real Figma URL (pre-prepared, node with known violations)
   → Bob scans, confirms design loaded

3. Bob asks for dev input — say "just check the design"
   → Bob runs scan

4. Report appears — point out:
   - Critical finding: custom component + token violation
   - Design delta section
   - Severity system

5. Say "A" — create Jira tickets
   → Bob creates tickets, shows ticket IDs

**Talking points while demo runs:**
- "This is Figma MCP + Carbon MCP running inside Bob — zero new tools"
- "The token check is exact — it reads the Figma variable assignments, not visual colour"
- "Jira ticket pre-filled — engineer doesn't have to write the brief"

---

### Segment 4 — So what (90 sec)

> "What this means for teams:
>
> — No more manual design review checklists
> — No more 'I didn't know that was the wrong token'
> — A Jira ticket with the fix already written, linked to the exact Figma node
>
> Phase 1 is fully viable today. Figma MCP, Carbon MCP, Claude vision
> are all connected in Bob. No procurement, no new tooling.
>
> The next step is a Bob skill that any IBM product team can invoke
> with four words: I want to run a UI review."

---

### Segment 5 — Ask (30 sec)

> "We have one ask: a pilot team.
>
> Senthil's API team already has the Carbon discipline — they're our
> ideal first user. We'd like to run UX Reviewer on one real sprint
> and measure: how many findings per screen, how many become Jira tickets,
> how many get fixed before PR.
>
> That's the test."

---

## Notes for Figma prototype

The prototype should mirror the Bob conversation above as a 4-screen flow:

| Screen | What it shows |
|---|---|
| 1 — Trigger | Bob chat window: user types "I want to run a UI review" |
| 2 — Intake | Bob asking for Figma link; user pastes URL; loading state |
| 3 — Report | Full UX Review Report rendered in Bob chat (the report format above) |
| 4 — Action | Jira ticket creation confirmation (tickets created, IDs shown) |

Optional 5th screen: Fix example — Bob showing the Carbon code fix inline.

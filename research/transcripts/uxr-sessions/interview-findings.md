# Interview Findings — UI Reviewer Discovery Sessions
**Date conducted:** 21 August 2026
**Sessions:** 3 developer interviews
**Conducted by:** Mridusmita Nath (UX Researcher), Ankit Anand (Designer)

## Participants

| ID | Name | Role | Team | Carbon maturity |
|---|---|---|---|---|
| `sahana` | Sahana S | Frontend Developer | Integration (webMethods) | High — Carbon React, occasional hex fallbacks |
| `senthil` | Senthil Kumaran Pattabiraman | Senior Developer / Tech Lead | API (webMethods) | Highest — 100% Carbon React, AI PDLC rules in place |
| `hariharan` | Hariharan SV | Frontend Developer | Integration (webMethods) | Low — Angular / PrimeNG, no dev mode access |

> **Key context:** These three developers represent a wide spectrum of Carbon adoption maturity within the same organisation. Senthil's API team is an outlier "utopia" — the Integration team (Sahana, Hariharan) is the more representative baseline.

---

## 1. Pain Points

### P1 — Navigating multiple Carbon storybooks is slow and confusing
Carbon components are split across several libraries (Carbon React, Carbon for IBM Products, etc.). Developers cannot always tell which library a component belongs to from Figma alone, and have to manually cross-reference multiple bookmarks and storybook URLs.

> *"Carbon is divided into 3 to 4 files, right? Because IBM products, Carbon reactor products and all that. So this is something that helps us to know what it is, which component is used in the Figma… the link doesn't help much because it opens in Figma itself."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### P2 — The Figma → Carbon documentation link chain requires 3+ navigations
The "View documentation" link in Figma opens the Carbon for IBM Products site, not storybook. Developers then have to navigate to the Code tab, then find the storybook link — three hops to get to the code-level API they actually need.

> *"It just gives the same Carbon for IBM Products. I mean you have to scan, yeah, storybook — then to go to storybook — code again gives you the insight of how it can be added in the code structure. But here is the storybook link. So it is like 3 times navigated to get there."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### P3 — Interaction and hover behaviour is rarely documented in Figma designs
Figma files show static states but frequently omit behaviour annotations — what happens on hover, click, and focus. This forces developers to either use Carbon defaults (which may be wrong for the use case) or stop and ask the designer mid-implementation.

> *"One more thing which we would like is to let us know what is the behaviour — maybe with an annotation or anything — like what would be the behaviour if you hover over that object. Sometimes we will use the default hover method of Carbon."*
> — Sahana S

> *"Toggle tip is with respect to clicking on it and displaying; tooltip is just hovering over it. So that information would also be helpful — what has to be added."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### P4 — Icon library source is undiscoverable from Figma
Colour icons used in runtimes and apps cannot easily be traced back to their source library from Figma. Developers have to rely on colleague knowledge or internal bookmarks rather than any navigable link.

> *"With respect to the colour icons — as of now, which even till date I have not found the library for it… anything with respect to the icons — it's a bit difficult to navigate and find the source of this."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### P5 — Spacing is read from Figma inspect and hard-coded as px values
Neither Sahana nor Hariharan uses Carbon spacing tokens in CSS. Both read spacing values by inspecting the Figma file and applying them as hardcoded `padding` / `margin` px values — a habit carried over from pre-Carbon workflows.

> *"We do that with padding and margins, the CSS part."*
> — Sahana S (confirming spacing is not token-based)

> *"I faced issues with identifying the numbers only — like to identify the space that has been left relative to the parent component."*
> — Hariharan SV

- **Interviews:** `sahana`, `hariharan`
- **Frequency:** 2 of 3

---

### P6 — Bob reuses non-Carbon components from the existing codebase without warning
When Bob generates UI for a new screen in a repo that already contains non-Carbon (legacy) components, it may reuse those components for similar elements — unless explicitly told to use Carbon. There is no automatic detection or warning that this is happening.

> *"There is an existing component in the screen that might be of older design before Carbon, so it might use that… if we have used the same thing which is existing in the previous step, if we have not mentioned to use Carbon, so we have to clearly state it."*
> — Sahana S

> *"When you just share a design even in a Figma frame, if it is not able to figure out the component, if the component is not connected well in Figma, then what Bob thinks is: maybe this is not a component available in Carbon. So let me create it on my own. So it writes its own CSS, own component."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `sahana`, `senthil`
- **Frequency:** 2 of 3

---

### P7 — Figma file organisation does not map cleanly to implementation scenarios
Design files sometimes lack a clear hierarchy of states and use-case scenarios. Developers see a complete mockup but struggle to correlate sections of it to specific runtime conditions (e.g. "private runtime owned by current user" vs "owned by other user").

> *"A few more details — like if it is a private runtime owned by current user, private runtime owned by other user — I mean, a little more context will be helpful… like a hierarchy could have been better."*
> — Hariharan SV

- **Interviews:** `hariharan`
- **Frequency:** 1 of 3

---

### P8 — Carbon web components are not adopted in the Angular codebase; full rewrites are required
The Integration team's Angular codebase uses PrimeNG. Even though Carbon web components are framework-agnostic, the team has not migrated because replacing PrimeNG components with Carbon web components requires a full rewrite rather than a drop-in swap.

> *"In our Angular codebase, currently we are not using the Carbon web components, so we are trying to provide the same kind of experience with the existing modules — I mean the PrimeNG modules we had."*
> — Hariharan SV

> *"We need to spend a significant amount of time to utilise these — I mean, rewrite all these components."*
> — Hariharan SV

- **Interviews:** `hariharan`
- **Frequency:** 1 of 3

---

### P9 — Token-level compliance is invisible to visual UI review
Even when the visual output looks correct, there is no way for a designer reviewing a video or screenshot to know whether the developer used Carbon tokens or hardcoded hex/px values. The compliance gap at the token level goes undetected until it causes a problem (e.g. theme switch breaks).

> *"If they are really using the Carbon component, are they really using the tokens? No one has any idea. So that gap is still there."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3

---

### P10 — UI compliance has no documented ownership; teams can ship non-compliant code with no accountability
For the Integration team, there is no formal gate preventing non-compliant UI from merging. Non-compliance gets caught by QA (post-merge) or stakeholder demos — or not at all. Without a clear owner or a compliance artefact, teams have no recourse when issues surface late.

> *"Currently, they are not even taking that responsibility or ownership. One day — I am damn sure — one day even if they are discussing internally with the management, they will simply say: 'this is what we got from you.'"*
> — Senthil Kumaran Pattabiraman (about the Integration team)

> *"No, currently it's not [happening]."*
> — Hariharan SV, confirming no UI review exists in his team

- **Interviews:** `senthil`, `hariharan`
- **Frequency:** 2 of 3

---

## 2. Unmet Needs

### U1 — A single, navigable link from Figma directly to the storybook code example
Developers need Figma's component link to land on the storybook Code tab — not on the Figma library frame, not on the Carbon docs landing page. The current 3-hop chain should be one click.

> *"One thing that would be good is this link would take us to the storybook rather than Figma itself."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### U2 — Automated detection of wrong or non-Carbon components in code
Developers and tech leads need a tool that can scan a branch, identify where a non-Carbon component has been used (or where the wrong Carbon component was chosen — e.g. `Select` instead of `Dropdown`), and report it with enough context for the developer to fix it.

> *"The designer had used Select by mistake, and we blindly trusted… when you click on it, you will see dropdown values in the native browser dropdown rather than the customised Carbon one."*
> — Senthil Kumaran Pattabiraman

> *"Currently Bob has access to the Carbon MCP, right? So maybe we can leverage that to say that the current developed screens — if a custom data table is used and it is not Carbon compliant, that can be found."*
> — Sahana S

- **Interviews:** `sahana`, `senthil`
- **Frequency:** 2 of 3

---

### U3 — Automated detection of hardcoded colour hex values and non-token spacing
The tool must go beyond component identity and check whether Carbon design tokens are used for colour, typography, and spacing — not just whether a component visually resembles a Carbon one.

> *"You don't want the developer to use their own px values or even a third-party library like Tailwind, but they will be recommended to use the spacing tokens provided by Carbon itself."*
> — Senthil Kumaran Pattabiraman

> *"You can also make sure they're using the colour values directly from Carbon, not any random hex value or any random colours from Tailwind CSS."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3 (but corroborated by Sahana's admission of hex usage)

---

### U4 — A compliance check that runs post-implementation, before PR merge
Developers want to run a compliance check themselves — after they've done their own visual check — and before the code goes to PR review. The check should be a final gate they control, not only something that surfaces in QA.

> *"I will be manually checking if it is matching the Figma mockup and maybe after my check, I want this compliance check to run."*
> — Hariharan SV

> *"UI review will again cross-check all these things are met. If there is anything, it will create a detailed report and it will also give you the next action items where Bob can get in and fix these."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`, `hariharan`
- **Frequency:** 2 of 3

---

### U5 — A compliance report that auto-creates a Jira ticket with acceptance criteria
When issues are found, the output should not just be a text report. It should become a Jira ticket with structured findings and acceptance criteria — so the developer can take the ticket straight to Bob and ask it to fix the issues.

> *"Ask it to create a report itself and attach that report as a description in a Jira ticket… there will be acceptance criteria — that also you can ask Bob to coin it according to your rules and expectations. If the ticket has that information, that is more than enough for Bob to run this and fix the code as well."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3

---

### U6 — The tool must work across any repository, not be tied to one product
The compliance tool should accept any git repository and branch — not be hard-coded to a specific product like Integration. Teams across webMethods products (Studio, API Connector, Integration) should be able to point it at their own branches.

> *"You make sure you are creating something generalised, not tied to one single product. I can use the same tool for my Studio repository, I can use the same tool for API Connector repository, any repository I wish."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3

---

### U7 — Figma dev mode access for all frontend developers
Hariharan does not have Figma dev mode access. Without it, he cannot inspect component names, view spacing values, or see connected component metadata — making accurate implementation significantly harder and forcing reliance on verbal handoffs.

> *"Last time when I requested for dev mode, they told in this bucket we couldn't accommodate me, and after that I haven't checked on it."*
> — Hariharan SV

> *"Without dev mode it is absolutely impossible to get the right components and get all of these kind of information."*
> — Ankit Anand (confirming the severity)

- **Interviews:** `hariharan`
- **Frequency:** 1 of 3

---

## 3. Workarounds

### W1 — Maintaining personal bookmarks to Carbon storybooks
Rather than navigating from Figma to docs, experienced developers (Sahana) keep personal bookmarks to Carbon React, Carbon for IBM Products, and other storybooks. This knowledge is not discoverable by newer developers.

> *"We do have certain bookmarks for Carbon React and all that where we go here and search the component."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### W2 — Searching the existing codebase before asking the designer
When a component or pattern is unclear in Figma, Sahana's first step is to search the codebase for prior implementations of the same component. Only if no existing usage exists does she escalate to the designer.

> *"First I would check in the codebase if anywhere else it's been used, and if I don't find any implementation of it, then the next is the designer."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3

---

### W3 — Using hex colour codes when the exact Carbon token is unknown
When developers cannot quickly identify the correct Carbon colour token for a specific use case (e.g. error background colour), they fall back to copying the hex value from Figma inspect and hardcoding it. They regard this as an "indirect match" and largely acceptable.

> *"It would be a bit time saving, but also we wouldn't have found the exact code for the colour and we would have proceeded with the hex code. It would mainly be for the backgrounds — say the error background."*
> — Sahana S

- **Interviews:** `sahana`
- **Frequency:** 1 of 3 (behaviour acknowledged as common)

---

### W4 — Using PrimeNG to visually approximate Carbon UI in Angular
The Integration Angular team uses PrimeNG components styled to look like Carbon, rather than Carbon web components. This avoids a full rewrite but produces code that is visually compliant but not tokenised or behaviourally Carbon.

> *"We are trying to provide the same kind of experience with the existing modules — I mean the PrimeNG modules we had… we didn't use the Carbon component. We provided the similar kind of experience."*
> — Hariharan SV

- **Interviews:** `hariharan`
- **Frequency:** 1 of 3

---

### W5 — In-person verbal handoff for component identification
Hariharan's primary method for understanding which Carbon components to use is a verbal meeting with the UX team. He receives storybook links verbally, which creates a dependency on meetings and leaves no persistent record.

> *"Basically I identify the components with the in-person discussion — in general meeting with the UX people only."*
> — Hariharan SV

- **Interviews:** `hariharan`
- **Frequency:** 1 of 3

---

### W6 — Adding Carbon rules to AI PDLC skills and Bob rules files
Senthil has proactively written a rules MD file that instructs Bob not to deviate from Carbon — no Tailwind, no Bootstrap, no hardcoded hex. This is the most mature workaround observed, effectively automating compliance at the generation stage, but it only works for developers using Bob to generate code.

> *"When you are implementing a UI, make sure you're using only the things provided by Carbon, don't use Tailwind classes, don't use Bootstrap classes — like that. You just type to Bob, Bob will create the MD file and you just have to integrate it."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3

---

### W7 — Mandatory screen-recording video attached to every UI-related PR
Senthil's team requires a video screen recording (not just screenshots) attached to every PR with UI changes. Designers can pause the video to spot visual gaps. This is a human-review workaround that catches visual issues but not code-level token or component compliance.

> *"We will be sharing a screen recording video, which is attached to the pull request and then they play it. And then since it is a video, they can pause and then find the gaps where all misalignments are there."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3

---

### W8 — Manual pixel-by-pixel iteration between Bob output and Figma mockup
Hariharan pastes screenshot images of designs into Bob to generate UI, then manually compares the output against the Figma mockup, iterates 2–3 times, and only then considers running a compliance check.

> *"I will take a snap and I will paste it in Bob and ask it to generate the output… the pasted screenshot and the actual dropdown won't match. So these kinds of differences arise. So it will take 2–3 iterations. So I will be manually checking if it is matching the Figma mockup."*
> — Hariharan SV

- **Interviews:** `hariharan`
- **Frequency:** 1 of 3

---

## 4. Desired Outcomes

### D1 — Carbon compliance is verifiable at any point in the development cycle
Developers, tech leads, and designers should be able to run a compliance check on demand — on any branch, at any point — and get a structured report. The check should not depend on a human reviewer's eye or a specific team's process maturity.

> *"The moment I know this developer has worked on this feature, I can get the branch information from them. I can just put it on the tool and run it. I don't have to ask them — I can run it by myself and generate the report, create the ticket, assign it back to them."*
> — Senthil Kumaran Pattabiraman

> *"Maybe we can leverage [Carbon MCP] to say that the current developed screens — if a custom data table is used and it is not Carbon compliant, that can be found."*
> — Sahana S

- **Interviews:** `sahana`, `senthil`
- **Frequency:** 2 of 3

---

### D2 — Bob generates Carbon-compliant code by default, without requiring explicit prompting
Developers should not have to remember to add "use Carbon strictly" to every Bob prompt. The expectation is that Carbon compliance is a default guardrail — enforced by rules or skills — not an opt-in behaviour.

> *"Saying that it has to use Carbon ensures that Bob is able to comply and leverage the Carbon components, the typography tokens, the colour tokens — all of those things it is able to leverage and implement correctly."*
> — Ankit Anand

> *"It depends on how well we prompt it. If you say to use Carbon — to test all the strictly."*
> — Sahana S (identifying this as a current gap)

- **Interviews:** `sahana`, `senthil`
- **Frequency:** 2 of 3

---

### D3 — UI review is a formal, documented gate — not a post-merge QA activity
Teams want compliance review to happen before code merges, producing an artefact (report, ticket) that creates accountability. "We approved this" should be on record — protecting both designers and developers.

> *"Unless until they get one approved from the UX team, they can't merge the PR. So that's the rule we follow."*
> — Senthil Kumaran Pattabiraman (describing his team's ideal, now practised)

> *"You can tell them: 'we don't give clearance because you're not meeting these.' So once they finish it, you can run it again."*
> — Senthil Kumaran Pattabiraman (describing desired outcome for the Integration team)

- **Interviews:** `senthil`, `hariharan` (absent in current process)
- **Frequency:** 2 of 3

---

### D4 — The compliance tool produces a fix, not just a finding
A report alone is not enough. The ideal outcome is that Bob can take the compliance report (or the Jira ticket generated from it) and fix the issues autonomously — the developer reviews and approves the fix, rather than starting from scratch.

> *"Bob is going to offer them the solution as well. So they will just say yes, go ahead and fix it, and Bob will fix it happily."*
> — Senthil Kumaran Pattabiraman

> *"Bob will be able to read the description and go through the code and fix them all."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`
- **Frequency:** 1 of 3

---

### D5 — A compliance check that compares implementation against the original Figma design
Beyond just checking Carbon compliance in isolation, developers want a tool that can compare what was implemented against what was designed — identifying the delta between the live implementation and the Figma source of truth.

> *"There is a skill that actually evaluates — I mean, to get the styling part from the Figma. So maybe we could utilise it by connecting… and comparing with Figma and identifying the delta."*
> — Hariharan SV

> *"You can pass in the branch information… ask Bob to run the scan."*
> — Senthil Kumaran Pattabiraman

- **Interviews:** `senthil`, `hariharan`
- **Frequency:** 2 of 3

---

### D6 — Compliance tooling accelerates less-mature teams without requiring a full process overhaul
Senthil's team achieved compliance through a ground-up culture change. Most teams cannot replicate that. The desired outcome is a tool that delivers meaningful compliance uplift even for teams that lack the AI PDLC structure, Figma connected components discipline, or mandatory PR review culture.

> *"If they are not matured enough to have something like this AI PDLC, then the second idea helps — and that serves the purpose of having something tangible for your use case also."*
> — Senthil Kumaran Pattabiraman

> *"This level of maturity for teams — it is not there for all the teams, so we have to."*
> — Mridusmita Nath (interviewer, reflecting on the gap)

- **Interviews:** `senthil`
- **Frequency:** 1 of 3 (but is the implicit goal of the whole product)

---

## Summary heatmap

| Finding | sahana | senthil | hariharan | Frequency |
|---|:---:|:---:|:---:|:---:|
| **P3** Interaction behaviour missing in Figma | ✓ | | | 1 |
| **P5** Spacing hard-coded as px values | ✓ | | ✓ | 2 |
| **P6** Bob inherits non-Carbon components from codebase | ✓ | ✓ | | 2 |
| **P9** Token compliance invisible to visual review | | ✓ | | 1 |
| **P10** No UI review gate; no ownership | | ✓ | ✓ | 2 |
| **U2** Detect wrong / non-Carbon components in code | ✓ | ✓ | | 2 |
| **U4** Compliance check before PR merge | | ✓ | ✓ | 2 |
| **U5** Auto-create Jira ticket from compliance findings | | ✓ | | 1 |
| **U7** Figma dev mode access for all devs | | | ✓ | 1 |
| **W3** Hex codes when token is unknown | ✓ | | | 1 |
| **W4** PrimeNG to approximate Carbon in Angular | | | ✓ | 1 |
| **W6** Carbon rules in Bob AI PDLC skills file | | ✓ | | 1 |
| **D1** Compliance verifiable at any point in dev cycle | ✓ | ✓ | | 2 |
| **D3** UI review as formal pre-merge gate | | ✓ | ✓ | 2 |
| **D5** Implementation vs Figma delta comparison | | ✓ | ✓ | 2 |

---

## Source transcripts

| Participant | Cleaned transcript |
|---|---|
| Sahana S | [`cleaned-UI reviewer - Discovery session Sahana.md`](cleaned-UI%20reviewer%20-%20Discovery%20session%20Sahana.md) |
| Senthil Kumaran Pattabiraman | [`cleaned-UI reviewer - Discovery session Senthil.md`](cleaned-UI%20reviewer%20-%20Discovery%20session%20Senthil.md) |
| Hariharan SV | [`cleaned-UI reviewer - Discovery session Hariharan.md`](cleaned-UI%20reviewer%20-%20Discovery%20session%20Hariharan.md) |

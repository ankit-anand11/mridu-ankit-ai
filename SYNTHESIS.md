# SYNTHESIS.md — UX Reviewer: Research, Market & Product Direction

**Date:** August 2026
**Prepared by:** Mridusmita Nath, Ankit Anand
**Status:** Discovery complete. Synthesis ready for delivery planning.

---

## 1. What we set out to learn

Three questions framed the discovery phase:

1. **Do IBM designers and developers have a real, recurring compliance problem** — or is Carbon compliance "good enough" across teams?
2. **What does the problem look like from both sides** — the developer implementing from Figma, and the designer handing off?
3. **Is there any commercial tool that already solves this** — and if not, what exactly is missing?

All three questions now have answers grounded in evidence.

---

## 2. What the research found

### 2.1 The developer side (3 interviews — Sahana, Senthil, Hariharan)

Developers across three Carbon maturity levels — high, highest, and low — reported the same core failures, just at different severity levels.

**The highest-frequency problems (2 of 3 developers):**

| Finding | What it means in practice |
|---|---|
| Spacing hard-coded as px values | Developers read spacing from Figma inspect and write `padding: 16px` instead of using `$spacing-05`. Theme switches break silently. |
| Bob inherits non-Carbon components from the codebase | When Bob generates UI in a repo that already has legacy components, it reuses them without warning — unless the developer explicitly says "use Carbon". |
| Token compliance invisible to visual review | A screen can look correct while the underlying code uses hex values. No one can tell from a screenshot or a video recording. |
| No formal UI review gate; no ownership | Non-compliant code can merge with no accountability. Issues surface in QA post-merge — or not at all. |
| Detecting wrong/non-Carbon components in code | Developers and tech leads want a tool that flags the problem and names the fix — not a manual audit. |
| Compliance check before PR merge | A self-service gate developers control — not a QA catch. |
| Figma vs. implementation comparison | Teams want a delta between the design source of truth and what was actually built. |

**The most articulate expression of the problem** (Senthil Kumaran, Tech Lead, API):
> *"If they are really using the Carbon component, are they really using the tokens? No one has any idea. So that gap is still there."*

**The most actionable desired outcome** (Senthil):
> *"The moment I know this developer has worked on this feature, I can get the branch information from them. I can just put it on the tool and run it. I don't have to ask them — I can run it by myself and generate the report, create the ticket, assign it back to them."*

---

### 2.2 The designer side (group session — Nagaraj, Diya, Animesh)

Designers surface the same compliance gap from the opposite direction: they see what was designed, then see what was built, and experience the drift as a personal failure.

**The highest-severity findings:**

| Finding | What it means in practice |
|---|---|
| Custom component inheritance debt | Components built during Delight → Carbon migration are orphaned — no Carbon owner, full maintenance on the product team. Accessibility failures become the team's liability. |
| Custom component handoff gap | Designers often forget to verbally flag broken components. Developers search for a non-existent Carbon component, then build something incorrect. |
| No formal implementation review gate (most teams) | Without a hard gate, drift accumulates silently. API Management's PR review model (designer must approve before merge) is the only team that has solved this — and it works. |
| Implementation review is manual and labour-intensive | Animesh: "I had to spend 2 hours annotating what all changes had to be made. Then it was implemented in 2 weeks, then reviewed again." |

**The proof point** (Diya, API Management):
> *"Unless you approve, it can't get merged, so they will get pulled up for it. So they will do it fast so that you review it."*

The API Management team's PR review gate is a replicable model. UX Reviewer automates the evidence generation that makes that gate possible at scale.

---

### 2.3 Cross-cutting theme: the compliance spectrum

The three developer interviews and three designer interviews span the same four IBM webMethods teams — and together they reveal a compliance spectrum:

```
Low compliance                                    High compliance
     │                                                  │
Hariharan (Integration)  Sahana (Integration)  Senthil (API)
Animesh (Integration)    Nagaraj (B2B)         Diya (API Mgmt)
     │                                                  │
Angular/PrimeNG          Carbon React           Carbon React
No dev mode              Hex fallbacks          100% tokens
No review gate           No gate                PR gate enforced
```

The right end of this spectrum shows what is achievable. UX Reviewer's job is to give teams at the left end a path toward it — without requiring them to build the culture and discipline from scratch first.

---

### 2.4 The market (competitive analysis — 5 tools)

Five tools represent the current state of the market: FigmaLint, Chromatic, Supernova, Tokens Studio, Zeroheight.

**What they collectively do well:**
- FigmaLint: detects hardcoded values and detached instances *in Figma*
- Chromatic: provides a production-proven PR merge gate on visual changes
- Supernova: tracks design system component adoption across a codebase (Enterprise)
- Tokens Studio: ensures Carbon tokens *exist* in the codebase via bidirectional sync
- Zeroheight: makes design system documentation queryable by AI via MCP

**What none of them do — the six confirmed market gaps:**

| Gap | Why it matters for IBM |
|---|---|
| **G1** No tool detects hardcoded hex/px in *code* | Sahana and Hariharan both admitted to copying hex values from Figma inspect. This behaviour is invisible to every tool surveyed. |
| **G2** No tool flags non-Carbon components and suggests Carbon/Web Component replacements | PrimeNG, Delight-era custom components, and wrong Carbon choices all look "fine" in every tool surveyed. |
| **G3** No PR gate is Carbon-specific | Chromatic catches visual regression. It cannot tell a Carbon `Button` from a custom button that looks identical. |
| **G4** No tool compares a live implementation against its Figma source of truth | Every tool operates on one side only — Figma or code. The delta comparison is the gap Hariharan and Senthil both described as the most valuable capability. |
| **G5** No tool auto-creates a structured issue from compliance findings | Senthil's vision — run the tool, get a Jira ticket with acceptance criteria, assign to developer, bring to Bob to fix — is not achievable with any surveyed tool. |
| **G6** No tool ships with Carbon as a pre-loaded rule set | All five tools are design-system-agnostic. Every team must configure their own rules. UX Reviewer starts Carbon-aware by default. |

---

## 3. What UX Reviewer is — the synthesis

UX Reviewer is the only tool that closes all six gaps simultaneously, because it is the only tool that:

1. Is built *inside* Bob — so it works where IBM teams already work
2. Uses Carbon MCP as its live rule source — so it is always current, never configured
3. Connects Figma MCP, Carbon MCP, and Jira MCP in a single workflow — so findings become tickets automatically

It is not a design linter. It is not a visual regression tool. It is not a documentation platform.

It is a **Carbon compliance workflow** — from Figma frame to code branch to Jira ticket — delivered as a conversation in Bob.

---

## 4. The IBM-internal experience

### What each persona gets

**Designer — pre-handoff**
> "Review this Figma frame for Carbon compliance"
> → Which components are wrong or custom
> → Which tokens are hardcoded
> → Which spacing values are off-grid
> → All findings with Carbon references and severity — in under a minute

**Developer — pre-PR**
> "Check my branch for Carbon compliance"
> → Which imports are non-Carbon (with Carbon/Web Component replacement named)
> → Which SCSS/CSS values are hardcoded (with correct Carbon token named)
> → "Create a Jira ticket from these findings" → structured ticket with acceptance criteria, assigned automatically

**Tech lead / designer — auditing another team**
> "Compare this Figma frame against this screenshot of the staging build"
> → Visual drift identified with Carbon-aware explanation
> → Findings exported to a Jira ticket with acceptance criteria

**What is never required:**
- No procurement
- No plugins to install
- No API keys to manage
- No Carbon rule files to write or maintain
- No separate dashboard or login
- No manual copy-paste of findings into Jira

---

## 5. Capability map — what is built from what

| Capability | Inspired by | Bob infrastructure | Phase |
|---|---|---|---|
| **C1** Carbon component compliance on a Figma frame | FigmaLint, Supernova | Figma MCP (`get_code_connect_map`, `get_design_context`) + Carbon MCP (`docs_search`) | 1 |
| **C2** Token compliance in a Figma frame | FigmaLint, Tokens Studio | Figma MCP (`get_variable_defs`) + Carbon MCP (`docs_search`) | 1 |
| **C3** Token + component compliance in code | Supernova, Tokens Studio | Bob reads source files + Carbon MCP (`code_search`) + `stylelint-plugin-carbon-tokens` | 1 |
| **C4** Figma vs. implementation delta — AI vision | Chromatic, Applitools | Figma MCP (`get_screenshot`) + Claude vision + Carbon MCP | 1 |
| **C5** Auto-create Jira ticket from findings | Chromatic (PR artifact), Supernova | Jira MCP | 1 |
| **C6** Carbon as the pre-loaded rule set | All 5 tools — inverted | Carbon MCP (live, no config) | 1 |
| **C4b** Figma vs. implementation delta — pixel-precise | Chromatic, uimatch | Bob-generated Playwright script in team CI + Carbon MCP interpretation | 2 |

Everything in Phase 1 is available today using infrastructure that IBM teams already have access to through Bob.

---

## 6. What makes this defensible

Every commercial tool in the market is design-system-agnostic. Their business model requires them to work for any design system, which means they cannot ship Carbon-specific rules, Carbon-specific token names, or Carbon-specific component recommendations.

UX Reviewer is IBM-internal and Carbon-specific by design. That is not a limitation — it is the entire advantage.

| Dimension | Market tools | UX Reviewer |
|---|---|---|
| Rule source | Team-configured, static, goes stale | Carbon MCP — live, maintained by the Carbon team, never stale |
| Component knowledge | Generic design system abstractions | Carbon's full component inventory, usage guidelines, and variant rules |
| Token knowledge | Whatever tokens the team loaded | Carbon's full token taxonomy, semantic intent, and context rules |
| Web Component alternatives | Not provided | Carbon Web Components (`@carbon/web-components`) named for every non-Carbon import |
| Jira integration | Not available in any surveyed tool | Built-in via Jira MCP |
| Procurement | Most require procurement or BYOAK | Zero — everything runs through Bob |
| Learning curve | Plugin installs, dashboards, onboarding | Zero — works in the same Bob conversation the team already uses |

---

## 7. Open questions for delivery planning

These questions are unresolved and should be addressed before the first sprint:

| Question | Why it matters |
|---|---|
| Which team is the pilot? | The pilot needs a Figma file with Code Connect set up; ideally a team already on Bob. Senthil's API team is the strongest candidate — highest Carbon maturity, most articulate about what the tool should do. |
| What is the minimum viable report format? | The AGENTS.md report format is defined. It needs to be validated with at least one designer and one developer before it is finalised. |
| How does the tool handle frames with no Code Connect? | Hariharan's team has no Code Connect. The tool needs a fallback — either image-based identification or a graceful "Code Connect not set up" message with a setup guide. |
| What is the Jira project structure for the pilot team? | Jira MCP needs a board ID, label taxonomy, and assignee mapping before it can create tickets. This is a 30-minute setup with the pilot team's tech lead. |
| How is the skill triggered? | Natural language ("review this frame") or a slash command (`/ux-review`)? This affects the skill description and example prompts. |
| What does "fixed" look like for a Critical finding? | Acceptance criteria in the Jira ticket need to be specific enough for a developer to close them without designer re-review. A few examples need to be written and validated. |

---

## 8. Recommended next steps

1. **Validate the report format** with one designer (Diya or Animesh) and one developer (Senthil or Sahana) — 30-minute session each. Show them a sample report generated from a real Figma frame.
2. **Set up Code Connect on a pilot frame** with the API team. This enables C1 (component compliance) to work at its full capability.
3. **Build the skill scaffold** — the Bob skill wrapper, trigger phrases, and the report template as defined in AGENTS.md.
4. **Run a live demo** on the API team's current sprint work. Generate a real compliance report on a real Figma frame. Show Senthil the Jira ticket output.
5. **Iterate on the report format** based on the demo feedback before opening to other teams.

---

## 9. Source documents

| Document | What it contains |
|---|---|
| [`PROJECT-OVERVIEW.md`](PROJECT-OVERVIEW.md) | Problem statement, vision, target users, analysis scope, market context |
| [`APPROACHES.md`](APPROACHES.md) | Technical feasibility, capability-by-capability analysis, phased delivery plan, IBM-internal experience section |
| [`research/transcripts/uxr-sessions/interview-findings.md`](research/transcripts/uxr-sessions/interview-findings.md) | Synthesised developer findings — 10 pain points, 7 unmet needs, 8 workarounds, 6 desired outcomes |
| [`research/transcripts/uxr-sessions/interview-summary-designer-group-discovery-webmethods.md`](research/transcripts/uxr-sessions/interview-summary-designer-group-discovery-webmethods.md) | Designer group session findings — handoff pain, custom component debt, review gate gap |
| [`research/competitive-analysis/competitive-insights.md`](research/competitive-analysis/competitive-insights.md) | 5-tool competitive analysis with company profiles, comparison matrix, 6 market gaps, 35 sources |
| [`AGENTS.md`](AGENTS.md) | Agent rules, MCP tool map, UX Review Report format, severity definitions |

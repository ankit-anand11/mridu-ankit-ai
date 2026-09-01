PRESENTATION OUTLINE
============================================================
Template: IBM-Template_AI-Readyv2.pptx
Total Slides: 24

Slide 1: cover (COVER-01)
------------------------------------------------------------
• title: "UX Reviewer — discovery findings" [32/70 chars] ✓
• name_and_job_title: "Mridusmita Nath, UX Researcher
Ankit Anand, Designer" [52/40 chars] ✗
• contact_details: "August 2026 | IBM webMethods" [28/50 chars] ✓

Slide 5: agenda (TOC-01)
------------------------------------------------------------
• title: "Agenda" [6/40 chars] ✓
• table_of_contents_01: "01  The problem
02  What we heard — research
03  What the market offers" [71/50 chars] ✗ ⚠️ IBM-BRAND
• table_of_contents_02: "04  The solution — UX Reviewer
05  What it feels like to use
06  Next steps" [75/50 chars] ✗ ⚠️ IBM-BRAND

Slide 6: section_problem (SECTION-01)
------------------------------------------------------------
• title: "01  The problem" [15/60 chars] ✓

Slide 7: problem_statement (SECTION-02)
------------------------------------------------------------
• big_statement: "IBM teams ship non-Carbon UI every day — and no one can tell until it breaks." [77/60 chars] ✗

Slide 22: problem_2col (CONTENT-2COL)
------------------------------------------------------------
• title: "Why Carbon compliance is hard to enforce today" [46/80 chars] ✓
• body_copy_01: "Teams implement from Figma but have no way to verify whether the code they wr..." [461/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_02: "The review process that should catch these issues is manual, ad hoc, and late..." [394/600 chars] ✓ ⚠️ IBM-BRAND

Slide 8: senthil_quote (STATEMENT-01)
------------------------------------------------------------
• title: "The token gap is invisible" [26/80 chars] ✓
• quote: "“If they are really using the Carbon component, are they really using the tok..." [131/150 chars] ✓ ℹ️ IBM-BRAND (must use curly quotes: )
• quote_name: "Senthil Kumaran Pattabiraman — Tech Lead, IBM API (webMethods)" [62/60 chars] ⚠ ⚠️ IBM-BRAND (must use curly quotes: )

Slide 6: section_research (SECTION-01)
------------------------------------------------------------
• title: "02  What we heard — research" [28/60 chars] ✓

Slide 24: who_we_spoke_to (CONTENT-2COL-HEADERS)
------------------------------------------------------------
• title: "Who we spoke to" [15/80 chars] ✓
• body_copy_title_01: "3 developer interviews" [22/50 chars] ✓
• body_copy_01: "Sahana S — Frontend Dev, Integration (Carbon React, hex fallbacks)
Senthil Ku..." [244/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_02: "1 designer group session" [24/50 chars] ✓
• body_copy_02: "Nagaraj Venkatraj — webMethods B2B (6 years, high custom component debt)
Diya..." [249/600 chars] ✓ ⚠️ IBM-BRAND

Slide 17: dev_pain_points (CONTENT-3COL-DIVIDERS)
------------------------------------------------------------
• title: "What developers told us" [23/80 chars] ✓
• body_copy_title_01: "Token compliance is invisible" [29/50 chars] ✓
• body_copy_01: "Spacing is copied as px values from Figma inspect. Colours are pasted as hex ..." [173/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_02: "No formal review gate" [21/50 chars] ✓
• body_copy_02: "Non-compliant code can merge with no accountability. Issues surface in QA pos..." [174/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_03: "Bob inherits wrong components" [29/50 chars] ✓
• body_copy_03: "When Bob generates UI in a repo with legacy components, it reuses them withou..." [168/600 chars] ✓ ⚠️ IBM-BRAND

Slide 17: designer_pain (CONTENT-3COL-DIVIDERS)
------------------------------------------------------------
• title: "What designers told us" [22/80 chars] ✓
• body_copy_title_01: "Custom components create debt" [29/50 chars] ✓
• body_copy_01: "Components built during past migrations are now orphaned — no Carbon owner, f..." [172/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_02: "Handoff gaps cause rework" [25/50 chars] ✓
• body_copy_02: "Designers forget to flag broken components verbally. Developers search for a ..." [173/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_03: "Review is late and labour-intensive" [35/50 chars] ✓
• body_copy_03: "Animesh: 'I spent 2 hours annotating changes, then waited 2 weeks for impleme..." [188/600 chars] ✓

Slide 8: diya_quote (STATEMENT-01)
------------------------------------------------------------
• title: "The PR gate model works" [23/80 chars] ✓
• quote: "“Unless you approve, it can’t get merged — so they will get pulled up for it...." [125/150 chars] ✓ ℹ️ IBM-BRAND (must use curly quotes: )
• quote_name: "Diya Susan Joseph — Designer, IBM API Management (webMethods)" [61/60 chars] ⚠ ⚠️ IBM-BRAND (must use curly quotes: )

Slide 6: section_market (SECTION-01)
------------------------------------------------------------
• title: "03  What the market offers" [26/60 chars] ✓

Slide 36: market_tools (GRID-6UP-01)
------------------------------------------------------------
• title: "Five tools cover parts of the problem — but none covers it for Carbon" [69/80 chars] ✓
• body_copy_title_01: "FigmaLint" [9/20 chars] ✓
• body_copy_01: "AI token & component audit inside Figma. Detects hardcoded values pre-handoff..." [132/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_02: "Chromatic" [9/20 chars] ✓
• body_copy_02: "Visual regression CI gate. Blocks PR on pixel-level changes. Cannot distingui..." [137/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_03: "Supernova" [9/20 chars] ✓
• body_copy_03: "Design system management with code adoption tracking (Enterprise). Framework-..." [141/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_04: "Tokens Studio" [13/20 chars] ✓
• body_copy_04: "Figma-to-code token pipeline. Ensures tokens exist in the codebase. Cannot de..." [139/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_05: "Zeroheight" [10/20 chars] ✓
• body_copy_05: "Living design system documentation with MCP. Adoption measured at doc-page le..." [121/150 chars] ✓
• body_copy_title_06: "The gap" [7/20 chars] ✓
• body_copy_06: "All five tools are design-system-agnostic. None ships with Carbon rules pre-l..." [136/150 chars] ✓ ⚠️ IBM-BRAND

Slide 36: market_gaps (GRID-6UP-01)
------------------------------------------------------------
• title: "Six gaps no market tool addresses" [33/80 chars] ✓
• body_copy_title_01: "G1 — Hardcoded values in code" [29/20 chars] ✗
• body_copy_01: "No tool detects hex/px values in a developer's branch and maps them to the co..." [96/150 chars] ✓
• body_copy_title_02: "G2 — Non-Carbon component detection" [35/20 chars] ✗
• body_copy_02: "No tool flags a PrimeNG dropdown or a custom component and names the Carbon W..." [102/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_03: "G3 — Carbon-specific PR gate" [28/20 chars] ✗
• body_copy_03: "Chromatic blocks on visual regression. No tool blocks on Carbon compliance — ..." [105/150 chars] ✓
• body_copy_title_04: "G4 — Figma vs. implementation delta" [35/20 chars] ✗
• body_copy_04: "No tool compares what was designed in Figma against what was implemented in t..." [87/150 chars] ✓
• body_copy_title_05: "G5 — Auto-create Jira ticket" [28/20 chars] ✗
• body_copy_05: "No tool turns compliance findings into a structured Jira ticket with acceptan..." [89/150 chars] ✓
• body_copy_title_06: "G6 — Carbon as the rule set" [27/20 chars] ✗
• body_copy_06: "Every tool requires teams to configure their own rules. No tool ships Carbon-..." [98/150 chars] ✓

Slide 6: section_solution (SECTION-01)
------------------------------------------------------------
• title: "04  The solution — UX Reviewer" [30/60 chars] ✓ ⚠️ IBM-BRAND

Slide 7: solution_statement (SECTION-02)
------------------------------------------------------------
• big_statement: "UX Reviewer closes all six gaps — inside Bob, using infrastructure IBM teams ..." [90/60 chars] ✗

Slide 20: what_ux_reviewer (SECTION-03)
------------------------------------------------------------
• title: "UX Reviewer" [11/60 chars] ✓
• number: "04" [2/4 chars] ✓
• subtitle: "A Carbon compliance workflow — from Figma frame to code branch to Jira ticket..." [114/80 chars] ✗ ⚠️ IBM-BRAND
• body_copy: "Not a linter. Not a visual regression tool. Not a documentation platform.

UX..." [341/800 chars] ✓ ⚠️ IBM-BRAND

Slide 28: capabilities (GRID-4UP-01)
------------------------------------------------------------
• header: "Six capabilities. One workflow." [31/30 chars] ⚠
• title: "What UX Reviewer can do" [23/80 chars] ✓
• body_copy_title_01: "C1 — Figma frame compliance" [27/20 chars] ✗
• body_copy_01: "Identify Carbon vs. custom components. Flag wrong variants. Name the correct ..." [96/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_02: "C2 — Token audit (Figma)" [24/20 chars] ✗ ⚠️ IBM-BRAND
• body_copy_02: "Detect hardcoded hex and px values per node. Name the Carbon token that shoul..." [96/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_03: "C3 — Code compliance (branch)" [29/20 chars] ✗
• body_copy_03: "Scan imports and SCSS for non-Carbon components and hardcoded values. Suggest..." [114/150 chars] ✓ ⚠️ IBM-BRAND
• body_copy_title_04: "C4–C6 — Delta, report, ticket" [29/20 chars] ✗
• body_copy_04: "Compare Figma vs. implementation visually. Generate a structured report. Auto..." [124/150 chars] ✓ ⚠️ IBM-BRAND

Slide 22: experience_designer (CONTENT-2COL)
------------------------------------------------------------
• title: "The experience — designer" [25/80 chars] ✓
• body_copy_01: ""Review this Figma frame for Carbon compliance"
→ Pastes Figma URL

Returns:
..." [231/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_02: "No plugins to install
No API keys to manage
No Carbon rules to configure
No s..." [198/600 chars] ✓ ⚠️ IBM-BRAND

Slide 22: experience_dev (CONTENT-2COL)
------------------------------------------------------------
• title: "The experience — developer" [26/80 chars] ✓
• body_copy_01: ""Check my branch for Carbon compliance"

Returns:
Non-Carbon imports — with C..." [358/600 chars] ✓ ⚠️ IBM-BRAND
• body_copy_02: "Developer takes the ticket to Bob:
"Fix the issues in this ticket"
→ Bob read..." [271/600 chars] ✓ ⚠️ IBM-BRAND

Slide 11: why_now (STATS-3UP)
------------------------------------------------------------
• title: "Why this is buildable now" [25/80 chars] ✓
• statistic_01: "0" [1 chars]
• statistic_claim_01: "New tools required — everything runs through Bob infrastructure IBM teams alr..." [85 chars]
• statistic_02: "0" [1 chars]
• statistic_claim_02: "Procurement needed — Carbon MCP, Figma MCP, and Jira MCP are available to all..." [93 chars] ⚠️ IBM-BRAND
• statistic_03: "Live" [4 chars]
• statistic_claim_03: "Carbon MCP rule source — maintained by the Carbon team, never stale, no confi..." [94 chars]
• statistic_sources: "Carbon MCP public preview, August 2026 | Figma MCP connected in Bob | Jira MC..." [101 chars] ⚠️ IBM-BRAND

Slide 6: section_next (SECTION-01)
------------------------------------------------------------
• title: "05  Next steps" [14/60 chars] ✓

Slide 19: next_steps (CONTENT-4COL-DIVIDERS-WITH-LIST)
------------------------------------------------------------
• title: "Recommended next steps" [22/80 chars] ✓
• body_copy_title_01: "Validate report format" [22/50 chars] ✓
• body_copy_list_01: "30-min session with one designer (Diya or Animesh)
30-min session with one de..." [149 chars] ⚠️ IBM-BRAND
• body_copy_title_02: "Set up pilot" [12/50 chars] ✓
• body_copy_list_02: "Set up Code Connect on a pilot Figma frame with the API team
Confirm Jira boa..." [150 chars] ⚠️ IBM-BRAND
• body_copy_title_03: "Run a live demo" [15/50 chars] ✓
• body_copy_list_03: "Generate a real compliance report on the API team's current sprint work
Show ..." [162 chars]

Slide 48: closing (CLOSING-01)
------------------------------------------------------------

============================================================
VALIDATION SUMMARY
============================================================

Character Limits:
  ✓ = Within character limit
  ⚠ = At or near limit (90-110%)
  ✗ = Exceeds limit (requires truncation)

IBM Brand Guidelines:
  ⚠️ IBM-BRAND = High priority issue (capitalization)
  ℹ️ IBM-BRAND = Medium priority issue (quotation marks)


============================================================
IBM BRAND GUIDELINE ISSUES
============================================================

HIGH PRIORITY (Capitalization):
------------------------------------------------------------
• agenda - table_of_contents_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: 01 the problem
02 what we heard — research
03 what the market offers

• agenda - table_of_contents_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: 04 the solution — UX reviewer
05 what it feels like to use
06 next steps

• problem_2col - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Teams implement from figma but have no way to verify whether the code they write uses the right carbon components, the right variants, or the right design tokens. spacing is copied as raw pixel values. colour tokens are bypassed with hex codes. wrong components are inherited from legacy codebases without any warning.

All of this looks correct on screen — until a theme switch breaks it, an accessibility audit fails, or a design review catches it post-merge.

• problem_2col - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: The review process that should catch these issues is manual, ad hoc, and late. designers review a screen recording attached to a PR. QA catches issues after merge. some teams have no review gate at all.

This creates compounding UX debt: inconsistent experiences, maintenance liability, and a widening gap between what was designed and what was built — with no shared artefact to trace back to.

• senthil_quote - quote_name
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Senthil kumaran pattabiraman — tech lead, IBM API (webmethods)

• who_we_spoke_to - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Sahana S — frontend dev, integration (carbon react, hex fallbacks)
Senthil kumaran — tech lead, API (100% carbon, AI PDLC rules in place)
Hariharan SV — frontend dev, integration (angular / primeng, no figma dev mode)

Conducted: 21 august 2026

• who_we_spoke_to - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Nagaraj venkatraj — webmethods B2B (6 years, high custom component debt)
Diya susan joseph — API management (full carbon, PR review gate enforced)
Animesh jain — webmethods integration (~1.5 years, severe design–dev drift)

Conducted: 20 august 2026

• dev_pain_points - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Spacing is copied as px values from figma inspect. colours are pasted as hex codes. the screen looks correct — but the code is not carbon-compliant. no tool can detect this.

• dev_pain_points - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Non-compliant code can merge with no accountability. issues surface in QA post-merge — or are never caught. without a gate, teams have no recourse when problems surface late.

• dev_pain_points - body_copy_03
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: When Bob generates UI in a repo with legacy components, it reuses them without warning. developers must explicitly say 'use carbon' — compliance is opt-in, not default.

• designer_pain - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Components built during past migrations are now orphaned — no carbon owner, full maintenance burden on the product team. accessibility failures become the team's liability.

• designer_pain - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Designers forget to flag broken components verbally. developers search for a non-existent carbon component and build something incorrect. rework cycles follow every feature.

• diya_quote - quote_name
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Diya susan joseph — designer, IBM API management (webmethods)

• market_tools - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: AI token & component audit inside figma. detects hardcoded values pre-handoff. figma-only — no code inspection, no carbon knowledge.

• market_tools - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Visual regression CI gate. blocks PR on pixel-level changes. cannot distinguish carbon button from a custom look-alike. not carbon-aware.

• market_tools - body_copy_03
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Design system management with code adoption tracking (enterprise). framework-agnostic — does not flag specific carbon violations in a branch.

• market_tools - body_copy_04
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Figma-to-code token pipeline. ensures tokens exist in the codebase. cannot detect whether a developer bypassed them with a hardcoded value.

• market_tools - body_copy_06
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: All five tools are design-system-agnostic. none ships with carbon rules pre-loaded. none integrates figma + code + Jira in one workflow.

• market_gaps - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: No tool flags a primeng dropdown or a custom component and names the carbon web component replacement.

• section_solution - title
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: 04 the solution — UX reviewer

• what_ux_reviewer - subtitle
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: A carbon compliance workflow — from figma frame to code branch to Jira ticket — delivered as a conversation in Bob

• what_ux_reviewer - body_copy
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Not a linter. not a visual regression tool. not a documentation platform.

UX reviewer uses carbon MCP as its live rule source — the same documentation maintained by the carbon team, updated with every release. no static rule files. no configuration. no procurement.

It works where IBM teams already work — inside Bob, via natural language.

• capabilities - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Identify carbon vs. custom components. flag wrong variants. name the correct carbon alternative.

• capabilities - body_copy_title_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: C2 — token audit (figma)

• capabilities - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Detect hardcoded hex and px values per node. name the carbon token that should replace each one.

• capabilities - body_copy_03
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Scan imports and SCSS for non-carbon components and hardcoded values. suggest carbon / web component replacements.

• capabilities - body_copy_04
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Compare figma vs. implementation visually. generate a structured report. auto-create a Jira ticket with acceptance criteria.

• experience_designer - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: "Review this figma frame for carbon compliance"
→ pastes figma URL

Returns:
Which components are wrong or custom
Which tokens are hardcoded
Which spacing values are off-grid
All findings with carbon references and severity ratings

• experience_designer - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: No plugins to install
No API keys to manage
No carbon rules to configure
No separate dashboard or login

Works in the same Bob conversation the team already uses.

Powered by: figma MCP + carbon MCP

• experience_dev - body_copy_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: "Check my branch for carbon compliance"

Returns:
Non-carbon imports — with carbon replacement named
Hardcoded SCSS values — with correct carbon token named
File-by-file findings list

"Create a Jira ticket from these findings"
→ structured ticket created automatically:
  Title, description, severity-ranked findings,
  Acceptance criteria, labels, assignee

• experience_dev - body_copy_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Developer takes the ticket to Bob:
"Fix the issues in this ticket"
→ Bob reads the acceptance criteria
→ Bob fixes the code
→ developer reviews and approves

The compliance loop is closed — without a single manual step.

Powered by: Bob file tools + carbon MCP + Jira MCP

• why_now - statistic_claim_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Procurement needed — carbon MCP, figma MCP, and Jira MCP are available to all IBM teams today

• why_now - statistic_sources
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Carbon MCP public preview, august 2026 | figma MCP connected in Bob | Jira MCP available as Bob skill

• next_steps - body_copy_list_01
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: 30-min session with one designer (diya or animesh)
30-min session with one developer (senthil or sahana)
Show a sample report from a real figma frame

• next_steps - body_copy_list_02
  Issue: Uses title case instead of sentence-case capitalization
  Suggested: Set up code connect on a pilot figma frame with the API team
Confirm Jira board ID and label taxonomy
Build the Bob skill scaffold and report template

MEDIUM PRIORITY (Quotation Marks):
------------------------------------------------------------
• senthil_quote - quote
  Issue: Quote text should be wrapped in quotation marks
  Suggested: "“If they are really using the Carbon component, are they really using the tokens? No one has any idea. So that gap is still there.”"

• senthil_quote - quote_name
  Issue: Quote text should be wrapped in quotation marks
  Suggested: "Senthil Kumaran Pattabiraman — Tech Lead, IBM API (webMethods)"

• diya_quote - quote
  Issue: Quote text should be wrapped in quotation marks
  Suggested: "“Unless you approve, it can’t get merged — so they will get pulled up for it. So they will do it fast so that you review it.”"

• diya_quote - quote_name
  Issue: Quote text should be wrapped in quotation marks
  Suggested: "Diya Susan Joseph — Designer, IBM API Management (webMethods)"

============================================================
Total Issues: 39

IBM Brand Guidelines:
• Use sentence-case capitalization (capitalize only first word and proper nouns)
• Wrap quote text in curly quotation marks ()
• Proper nouns: IBM, Watson, watsonx, Bob


============================================================
Next Steps:
1. Review the outline above
2. Verify all content is accurate
3. Check character counts for any ✗ or ⚠ indicators
4. Fix any IBM brand guideline issues (⚠️ or ℹ️ indicators)
5. Approve to proceed with generation

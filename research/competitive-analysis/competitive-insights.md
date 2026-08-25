# Competitive Insights — UI Compliance & Design-to-Code Tooling
**Prepared for:** UX Reviewer — IBM Bob Skill
**Date:** August 2026
**Scope:** AI-powered and automated tools supporting Carbon-ecosystem design system compliance — covering *visual compliance* (correct component, correct variant) and *token-level compliance* (Carbon tokens in code vs hardcoded hex/px). Includes tools used by both developers (self-check, CI/PR) and tech leads / designers (audit-on-demand). All claims carry cited sources.

---

## 1. Scope & Methodology

Five tools were selected to represent the dominant approaches to design system compliance and design-to-code fidelity as of August 2026:

| # | Tool | Approach |
|---|---|---|
| 1 | **FigmaLint** | AI-powered Figma-side component and token audit |
| 2 | **Chromatic** | Visual regression testing in CI/CD, Storybook-native |
| 3 | **Supernova** | Design system management with code adoption tracking |
| 4 | **Tokens Studio** | Design token pipeline: Figma → code |
| 5 | **Zeroheight** | Design system documentation with adoption measurement |

**Exclusions:** Figma-to-code generators (Anima, Locofy, Builder Fusion) were excluded as they generate code rather than audit it. Mechanical WCAG checkers (axe-core, IBM Equal Access Checker) are out of scope. None of the tools surveyed is Carbon-specific by default.

---

## 2. Tool Profiles

---

### 2.1 FigmaLint

#### Company Overview
FigmaLint is an open-source AI plugin built by **Southleft, LLC** — a small US-based design systems consultancy. It is not a standalone funded company; it is a tool built and maintained by the Southleft team as a commercial open-source project. The GitHub repository shows active maintenance as of August 2026. [(Source: github.com/southleft/figmalint)](https://github.com/southleft/figmalint) [(Source: southleft.com/tag/mcp-servers)](https://southleft.com/tag/mcp-servers)

- **Founded:** Southleft, LLC — active since at least 2023; FigmaLint plugin launched December 2025
- **Headquarters:** United States
- **Business model:** Freemium Figma plugin; bring-your-own AI API key

#### Key Products
**FigmaLint** — AI-powered Figma plugin that audits design components for design system compliance, token adoption, accessibility readiness, and developer handoff quality. Uses Claude, GPT-4, or Gemini via user-supplied API keys. [(Source: figma.com/community/plugin/1521241390290871981)](https://www.figma.com/community/plugin/1521241390290871981/figmalint)

Key capabilities:
- **Design token detection:** Identifies Figma Variables, Named Styles, and hardcoded values (colours, spacing, typography) per node. Distinguishes tokenised values from raw hex/px. [(Source: figma.com/community/plugin/1521241390290871981)](https://www.figma.com/community/plugin/1521241390290871981/figmalint)
- **Component audit scoring:** Scores each component on token adoption (2× weight), interactive state coverage (3× weight), accessibility, and readiness. [(Source: figma.com/community/plugin/1521241390290871981)](https://www.figma.com/community/plugin/1521241390290871981/figmalint)
- **Auto-fix:** Binds hardcoded colours and spacing to design system variables using fuzzy matching; renames generic layers. [(Source: github.com/southleft/figmalint)](https://github.com/southleft/figmalint)
- **Detached instance detection:** Flags frames matching a component name that are no longer library-linked. [(Source: figma.com/community/plugin/1521241390290871981)](https://www.figma.com/community/plugin/1521241390290871981/figmalint)

Southleft also maintains **Figma Console MCP** — an MCP server providing project-wide Figma context, variable/token extraction, and WCAG linting via AI conversation. [(Source: southleft.com/tag/mcp-servers)](https://southleft.com/tag/mcp-servers)

#### Target Users
Designers and design system authors working in Figma, pre-handoff. Not developer-facing; does not inspect code. [(Source: github.com/southleft/figmalint)](https://github.com/southleft/figmalint)

#### Framework Coverage
Figma-only. No awareness of Carbon, React, or Web Components. Cannot flag non-Carbon components in a codebase or suggest Web Component replacements. [(Source: github.com/southleft/figmalint)](https://github.com/southleft/figmalint)

#### Pricing
Free plugin (basic). Paid tier at $15 (introductory) for variable-related detection. [(Source: figma.com/community/plugin/1577978298506710437)](https://www.figma.com/community/plugin/1577978298506710437/design-system-compliance-checker)

#### Strengths
- Deepest token-level inspection on the *design* side of the pipeline
- Auto-fix reduces remediation effort for designers
- Bring-your-own-AI model keeps infrastructure costs low
- Active OSS community with rapid iteration (2 versions within 1 month of launch)

#### Recent News
- **August 2026:** Active development continues; Figma Console MCP (companion MCP server) receiving updates alongside FigmaLint. [(Source: github.com/southleft)](https://github.com/southleft)

---

### 2.2 Chromatic

#### Company Overview
Chromatic is the visual testing and UI review platform built by the team that also maintains **Storybook** — the industry-standard component development tool. It is bootstrapped (no outside VC funding) and profitable, with approximately **$5.6M estimated ARR** and **51 employees** as of September 2025. Headquartered in San Francisco. [(Source: getlatka.com/companies/chromatic.com)](https://getlatka.com/companies/chromatic.com)

- **Founded:** 2017
- **Headquarters:** San Francisco, California
- **Revenue:** ~$5.6M ARR (estimated, 2025)
- **Employees:** ~51 (September 2025)
- **Business model:** SaaS, per-snapshot pricing; free tier available

#### Key Products
**Chromatic** — Cloud-based visual regression testing and UI review platform. Captures UI snapshots at component level on every PR and surfaces visual diffs for human approval. Native Storybook integration. [(Source: chromatic.com/pricing)](https://www.chromatic.com/pricing)

Key capabilities:
- **Visual regression testing:** Pixel-level diff between baseline and PR snapshots across Chrome, Firefox, Safari, Edge. [(Source: qaskills.sh/blog/chromatic-storybook-visual-testing-guide)](https://qaskills.sh/blog/chromatic-storybook-visual-testing-guide)
- **PR/CI gate:** Posts a review status check to PR; merge is blocked until visual changes are approved. [(Source: crosscheck.cloud/blogs/percy-vs-applitools-vs-chromatic)](https://crosscheck.cloud/blogs/percy-vs-applitools-vs-chromatic-visual-regression-testing)
- **TurboSnap:** Incremental rebuild — only re-snapshots stories affected by a code change, reducing snapshot count by 90%+ on most PRs. [(Source: qaskills.sh/blog/chromatic-storybook-visual-testing-guide)](https://qaskills.sh/blog/chromatic-storybook-visual-testing-guide)
- **Figma plugin:** Side-by-side design-vs-code comparison in Figma using embedded Storybook stories. [(Source: chromatic.com/pricing)](https://www.chromatic.com/pricing)
- **Interaction tests:** Runs Storybook play functions as part of the snapshot workflow. [(Source: qaskills.sh/blog/chromatic-storybook-visual-testing-guide)](https://qaskills.sh/blog/chromatic-storybook-visual-testing-guide)

#### Target Users
Frontend engineers and tech leads running component-driven frameworks. Secondary: designers using the UI Review workflow to approve visual changes before merge. [(Source: chromatic.com/pricing)](https://www.chromatic.com/pricing)

#### Framework Coverage
React, Vue, Angular — any framework Storybook supports. No design-system-specific intelligence. Cannot distinguish a Carbon `Button` from a custom button visually unless a baseline exists. Cannot detect token usage or flag non-Carbon source code. [(Source: bug0.com/knowledge-base/visual-regression-testing-tools)](https://bug0.com/knowledge-base/visual-regression-testing-tools)

#### Pricing
Free: 5,000 snapshots/month. Starter: $179/month (35,000 snapshots). Pro: $399/month (85,000 snapshots). Enterprise: custom. [(Source: chromatic.com/pricing)](https://www.chromatic.com/pricing)

#### Strengths
- Strongest PR gate model of tools surveyed; merge-blocking review is production-proven
- Git-aware baselines handle branch-heavy workflows cleanly
- Built by the Storybook team — deepest ecosystem integration available
- Bootstrapped sustainability signals product longevity without VC pressure

#### Recent News
- **August 2026:** No major announcements found in the last 30 days. Ongoing maintenance of Storybook (primary product) with regular releases. [(Source: releasebot.io/updates/figma)](https://releasebot.io/updates/figma)

---

### 2.3 Supernova

#### Company Overview
Supernova is a Prague- and New York-based design system management platform founded in 2018 by **Jiri Trecak** (CEO) and **Oskar Koristka** (COO). It closed a **$9.2M Series A** in September 2025 (total funding $22.2M across 4 rounds), with backers including Taiwania Capital and Wing Venture Capital. Customers include Air France, KLM, Kraft Heinz, Paramount, and Mozilla. [(Source: prnewswire.com — Supernova Series A)](https://www.prnewswire.com/news-releases/supernova-raises-9-2-million-to-bring-vibe-coding-to-professional-product-teams-302570922.html) [(Source: tracxn.com/d/companies/supernova)](https://tracxn.com/d/companies/supernova/__F0aQs3jcmBn1ZLEQOVM2SpTuBU9p5EGYX7Pu8JauOME)

- **Founded:** 2018 (Prague, Czech Republic)
- **Funding:** $22.2M total; Series A closed September 2025
- **Business model:** Per-seat SaaS; free tier available
- **Notable customers:** Air France, KLM, Kraft Heinz, Paramount, Mozilla

#### Key Products
**Supernova Platform** — Design system management combining token management, documentation, code automation pipelines, and AI context distribution via MCP. [(Source: supernova.io/pricing)](https://www.supernova.io/pricing)

Key capabilities:
- **Token management and export:** Syncs Figma Variables; exports to CSS, JSON, Tailwind v4, and custom formats via automation pipelines. [(Source: learn.supernova.io/changelog)](https://learn.supernova.io/changelog)
- **Code adoption tracking (Enterprise):** Monitors whether design system components are used in the codebase; includes a design system adoption dashboard (launched May 2026). [(Source: learn.supernova.io/changelog)](https://learn.supernova.io/changelog)
- **Supernova Portal + MCP:** Exposes design system data (tokens, components, rules) as a remote MCP server — 40+ tools, unlimited access on all plans. AI contexts launched June 2026 give each team or agent a filtered governance layer. [(Source: learn.supernova.io/changelog)](https://learn.supernova.io/changelog)
- **Documentation with live previews:** Embeds Storybook stories and live code examples alongside component docs. [(Source: capterra.com/p/266448/Supernova)](https://www.capterra.com/p/266448/Supernova)

**Supernova Portal** — Enterprise vibe-coding tool generating PRDs, prototypes, and business cases synced to the codebase, announced alongside the Series A (September 2025). [(Source: prnewswire.com — Supernova Series A)](https://www.prnewswire.com/news-releases/supernova-raises-9-2-million-to-bring-vibe-coding-to-professional-product-teams-302570922.html)

#### Target Users
Design system teams, DesignOps, and engineering leads managing mid-to-large design systems. Not a developer self-check tool. [(Source: softwareadvice.com/app-development/supernova-profile)](https://www.softwareadvice.com/app-development/supernova-profile)

#### Framework Coverage
Framework-agnostic at token and documentation level. Code adoption tracking (Enterprise) is codebase-aware but does not flag specific non-compliant component instances or token violations at the branch level. [(Source: capterra.com/p/266448/Supernova)](https://www.capterra.com/p/266448/Supernova)

#### Pricing
Free: up to 5 seats, 1 design system. Pro: $35/seat/month (up to 15 seats, 2 design systems). Enterprise: custom (includes code adoption tracking, unlimited pipelines). [(Source: supernova.io/pricing)](https://www.supernova.io/pricing)

#### Strengths
- Only tool in this set with explicit *code adoption tracking* of design system components
- MCP server (40+ tools, unlimited, all plans) is the most capable AI context layer surveyed
- End-to-end platform: tokens + docs + code pipelines in one product
- Well-funded ($22.2M) with strong enterprise customer reference list

#### Recent News
- **June 2026:** Launched AI context governance layer — teams can now control which subset of design system data each team or AI agent can read. [(Source: learn.supernova.io/changelog)](https://learn.supernova.io/changelog)
- **May 2026:** Launched design system adoption dashboard — tracks which components teams are actually using over time. [(Source: learn.supernova.io/changelog)](https://learn.supernova.io/changelog)

---

### 2.4 Tokens Studio

#### Company Overview
Tokens Studio is built by **HYMA**, a Rotterdam-based (Netherlands) infrastructure company founded by **Mike Kamminga** (CEO), **Jan Six**, **Esther Cheran**, and **Marcel van Zwieten** (CCO). The Tokens Studio Figma plugin has **300,000+ users** and 34,000 daily active users. Team size is 11–50 employees. Funding details are not publicly disclosed. [(Source: tokens.studio/about)](https://tokens.studio/about) [(Source: tokens.studio)](https://tokens.studio)

- **Parent company:** HYMA (Rotterdam, Netherlands)
- **Employees:** 11–50
- **Business model:** Freemium Figma plugin + paid Studio platform
- **Adoption:** 300,000+ users; 34,000 daily active users

#### Key Products
**Tokens Studio for Figma** — Figma plugin for managing and syncing design tokens bidirectionally between Figma and code repositories. The de facto standard token management tool. [(Source: tokens.studio)](https://tokens.studio)

**Tokens Studio Platform (Studio)** — Web-based platform extending the plugin with advanced token management, versioning, branching, asset management, documentation, and MCP access. [(Source: tokens.studio/pricing)](https://tokens.studio/pricing)

Key capabilities:
- **23+ token types:** Colours, typography, spacing, border radius, shadows, sizing, and more. [(Source: cssauthor.com/design-token-management-tools)](https://cssauthor.com/design-token-management-tools)
- **Git sync:** Pushes token changes from Figma to GitHub/GitLab/Bitbucket as DTCG-compliant JSON, triggering a PR to update CSS custom properties in the codebase. [(Source: docs.tokens.studio/token-storage/remote)](https://docs.tokens.studio/token-storage/remote)
- **W3C Design Tokens Specification v1 compliance:** Cross-tool interoperability with Style Dictionary v4 and other pipeline tooling. [(Source: cssauthor.com/design-token-management-tools)](https://cssauthor.com/design-token-management-tools)
- **MCP access:** Available on all paid plans; exposes token data to AI coding assistants. [(Source: tokens.studio/pricing)](https://tokens.studio/pricing)

#### Target Users
Design system authors, designers managing tokens, and DesignOps engineers building automation pipelines. Developer-facing at the token-sync output stage, not at the compliance-check stage. [(Source: cssauthor.com/design-token-management-tools)](https://cssauthor.com/design-token-management-tools)

#### Framework Coverage
Framework-agnostic export (CSS, JSON, iOS, Android, Tailwind). Ensures tokens *exist* in code — does not inspect whether developers used them. [(Source: tokens.studio)](https://tokens.studio)

#### Pricing
Free plugin (basic). Starter Plus: €39–49/month per editor. Essential: €169/month. Organization: €499/month (5 editors, 20 projects). Enterprise: custom. [(Source: tokens.studio/pricing)](https://tokens.studio/pricing)

#### Strengths
- De facto standard for the Figma → code token pipeline; 300k+ users signals exceptional community lock-in
- Bidirectional sync means token changes flow both ways without manual steps
- W3C-compliant output ensures interoperability with Style Dictionary and downstream tooling
- The most reliable mechanism for ensuring tokens *exist* in the codebase

#### Recent News
- **2026 (ongoing):** Active collaboration with Penpot to build native Design Tokens into Penpot's core product, expanding Tokens Studio's reach beyond Figma. [(Source: linkedin.com/company/hyma-tokens-studio)](https://www.linkedin.com/company/hyma-tokens-studio)

---

### 2.5 Zeroheight

#### Company Overview
Zeroheight is a London-based design system documentation platform founded in 2015. It has raised **$10.5M across 4 rounds** (last round: Series A, August 2021) with investors including Y Combinator and Pharus. The company has not raised since 2021, suggesting it is operating near profitability. It is repositioning in 2026 as a full design system platform (documentation + analytics + governance). [(Source: tracxn.com/d/companies/zeroheight)](https://tracxn.com/d/companies/zeroheight/__Fdr4at0e54NFimhAHp60JQMvRLktPrVqwauJfrh2lpQ) [(Source: together.agency/work/zeroheight)](https://together.agency/work/zeroheight)

- **Founded:** 2015 (London, United Kingdom)
- **Funding:** $10.5M total; Series A August 2021
- **Investors:** Y Combinator, Pharus, London Co-Investment Fund, and others
- **Business model:** Per-editor SaaS; free tier available

#### Key Products
**Zeroheight** — Living design system documentation platform that syncs from Figma and Storybook into a continuously updated documentation site. [(Source: zeroheight.com/documentation)](https://zeroheight.com/documentation)

Key capabilities:
- **Continuous Figma/Sketch sync:** Documentation auto-updates on Figma changes — no manual republish needed. [(Source: glow.team/blog/zeroheight-design-system-full-guide)](https://glow.team/blog/zeroheight-design-system-full-guide)
- **Live interactive code blocks:** Developers test and tweak React, Angular, Vue component props inline; copy production-ready code snippets. [(Source: zeroheight.com/documentation)](https://zeroheight.com/documentation)
- **Adoption measurement:** Tracks which teams and products are consuming documentation — usage analytics per page. [(Source: zeroheight.com)](https://zeroheight.com)
- **MCP integration (March 2026):** Exposes design system documentation as a remote MCP server for AI coding assistants. Each viewer gets a unique MCP URL. [(Source: help.zeroheight.com — MCP setup)](https://help.zeroheight.com/hc/en-us/articles/43737291730331-Set-up-MCP-access-via-link)
- **AI assistant:** Conversational interface for querying design system content. [(Source: zeroheight.com)](https://zeroheight.com)

Per Zeroheight's own 2026 Design Systems Report, **Figma holds 97% adoption among design system teams**, and 30% of teams want "linting and guidance for design system consumers" from AI tooling. [(Source: report.zeroheight.com)](https://report.zeroheight.com)

#### Target Users
Design system teams, designers, and developers needing a shared reference. Leadership and DesignOps tracking adoption at documentation level. Not a compliance tool for individual developer branches. [(Source: zeroheight.com)](https://zeroheight.com)

#### Framework Coverage
Framework-agnostic documentation. Supports React, Angular, Vue code snippet embeds. Cannot inspect a developer's branch for non-compliant component usage or hardcoded values. [(Source: zeroheight.com/documentation)](https://zeroheight.com/documentation)

#### Pricing
Free: 1 editor, unlimited viewers. Starter: ~$49/editor/month (annual). Team: ~$69–89/editor/month. Enterprise: custom (SSO, analytics, priority support). [(Source: vendr.com/marketplace/zeroheight)](https://www.vendr.com/marketplace/zeroheight)

#### Strengths
- Best adoption measurement at documentation-coverage level
- MCP integration (March 2026) positions it as a real-time design system query layer alongside AI coding assistants
- Y Combinator-backed; strong brand reputation in design systems community
- Zeroheight's own research data (Design Systems Report 2026) signals deep market intelligence advantage

#### Recent News
- **March 2026:** Launched remote MCP server — design system documentation now queryable by AI tools. [(Source: help.zeroheight.com — MCP setup)](https://help.zeroheight.com/hc/en-us/articles/43737291730331-Set-up-MCP-access-via-link)

---

## 3. Comparison Matrix

| Dimension | FigmaLint | Chromatic | Supernova | Tokens Studio | Zeroheight |
|---|:---:|:---:|:---:|:---:|:---:|
| **Visual compliance (component, variant)** | ✓ Figma-side | ✓ pixel diff | ✗ | ✗ | ✗ |
| **Token compliance detection in code** | ✗ | ✗ | ✗ | ✗ (supply only) | ✗ |
| **Token compliance detection in Figma** | ✓ | ✗ | ✓ sync | ✓ sync | ✓ display |
| **Non-Carbon component detection in code** | ✗ | ✗ | Partial (Enterprise) | ✗ | ✗ |
| **Carbon-specific rules** | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Carbon Web Component replacement suggestions** | ✗ | ✗ | ✗ | ✗ | ✗ |
| **PR / CI merge gate** | ✗ | ✓ | ✗ | Partial (token PR) | ✗ |
| **Developer self-check (branch / file)** | ✗ | ✓ | ✗ | ✗ | ✗ |
| **Tech lead / designer audit on demand** | ✓ Figma | ✓ UI Review | ✓ docs | ✗ | ✓ docs |
| **Structured compliance report** | ✓ per component | ✓ per snapshot | ✗ | ✗ | ✗ |
| **Auto-create Jira / issue tracker ticket** | ✗ | ✗ | ✗ | ✗ | ✗ |
| **Multi-repo / cross-product support** | ✓ | ✓ | ✓ | ✓ | ✓ |
| **React support** | ✓ design-side | ✓ | ✓ | ✓ | ✓ |
| **Web Components / Angular support** | ✓ design-side | ✓ | ✓ | ✓ | ✓ |
| **MCP / AI assistant integration** | Partial (Console MCP) | ✗ | ✓ 40+ tools | ✓ | ✓ March 2026 |
| **Free tier** | ✓ | ✓ 5k snapshots | ✓ 5 seats | ✓ plugin | ✓ 1 editor |
| **Pricing model** | Freemium | Per snapshot | Per seat | Per editor/month | Per editor/month |
| **Company funding** | Bootstrapped (Southleft) | Bootstrapped | $22.2M (Series A) | Undisclosed | $10.5M (Series A 2021) |

---

## 4. Market Gaps

The following gaps are derived directly from the comparison matrix. No tool surveyed addresses them in the context of the Carbon Design System ecosystem.

### G1 — No tool detects hardcoded values (hex/px) in *code*
Every tool in this analysis detects hardcoded values in Figma (FigmaLint, Tokens Studio, Supernova) or ignores them entirely. None inspects a developer's codebase or open branch to flag `color: #f4f4f4` or `padding: 16px` where a Carbon token (`$layer-01`, `$spacing-05`) should have been used. The open-source `stylelint-plugin-carbon-tokens` exists for SCSS files but is not integrated into any of these platforms and requires manual configuration. [(Source: carbondesignsystem.com — web components tutorial)](https://carbondesignsystem.com/developing/web-components-tutorial/step-5)

### G2 — No tool flags non-Carbon components and suggests Carbon / Web Component replacements
Supernova's Enterprise adoption dashboard tracks whether design system components are used broadly, but no tool identifies a specific instance — for example, a PrimeNG `p-dropdown` or a custom `<div class="select">` in a React or Angular codebase — and maps it to its Carbon equivalent (`Dropdown`, or the Carbon Web Component `<cds-dropdown>`). The identification + replacement-suggestion pairing is absent across the entire surveyed market. [(Source: carbondesignsystem.com — community frameworks)](https://carbondesignsystem.com/developing/community-frameworks/other-frameworks)

### G3 — No tool provides a PR-gated, Carbon-specific compliance check
Chromatic provides the strongest PR gate but detects visual regression — not Carbon compliance. It cannot distinguish a visually correct Carbon `Button` from a custom button that looks identical. No tool posts a structured Carbon compliance report (components, tokens, spacing) as a PR check and blocks merge until findings are resolved. [(Source: crosscheck.cloud)](https://crosscheck.cloud/blogs/percy-vs-applitools-vs-chromatic-visual-regression-testing)

### G4 — No tool compares a live implementation against its Figma source of truth
All tools operate either on the Figma side (FigmaLint, Tokens Studio, Supernova) or the code side (Chromatic), but none performs a direct delta comparison between what was designed in Figma and what was implemented in a branch — identifying spacing, component, or token differences between the design source of truth and the staged implementation. The Figma MCP `get_variable_defs` and Carbon MCP `docs_search` together provide the knowledge layer, but no commercial product orchestrates this comparison workflow. [(Source: systemsandsignals.co — design systems as AI infrastructure)](https://www.systemsandsignals.co/p/design-systems-as-ai-infrastructure)

### G5 — No tool auto-creates a structured issue from compliance findings
Every tool produces some form of output (Chromatic snapshot diff, FigmaLint score, Supernova adoption dashboard). None generates a structured, actionable issue in a project management tool (Jira, Linear, GitHub Issues) with pre-populated acceptance criteria derived from compliance findings. Zeroheight's Design Systems Report 2026 shows 30% of design system teams want "linting and guidance for design system consumers" from AI, yet no tool closes the loop from finding to ticket. [(Source: report.zeroheight.com)](https://report.zeroheight.com)

### G6 — No tool ships with Carbon as a pre-loaded rule set
All five tools are design-system-agnostic. They operate on tokens, components, and styles as abstract concepts — not as Carbon-specific entities. No commercial tool ships with Carbon's component inventory, token taxonomy, and usage rules pre-loaded, enabling it to answer the question "is this implementation Carbon-compliant?" without requiring teams to configure their own rule set. Carbon MCP provides the knowledge layer, but no compliance tool currently consumes it as a live authoritative rules engine. [(Source: carbondesignsystem.com — Carbon MCP overview)](https://carbondesignsystem.com/developing/carbon-mcp/overview)

---

## 5. Sources

| # | Source |
|---|---|
| 1 | FigmaLint GitHub — [github.com/southleft/figmalint](https://github.com/southleft/figmalint) |
| 2 | FigmaLint Figma Community — [figma.com/community/plugin/1521241390290871981](https://www.figma.com/community/plugin/1521241390290871981/figmalint) |
| 3 | Design System Compliance Checker plugin — [figma.com/community/plugin/1577978298506710437](https://www.figma.com/community/plugin/1577978298506710437/design-system-compliance-checker) |
| 4 | Southleft MCP blog — [southleft.com/tag/mcp-servers](https://southleft.com/tag/mcp-servers) |
| 5 | Southleft GitHub org — [github.com/southleft](https://github.com/southleft) |
| 6 | Chromatic revenue & company profile — [getlatka.com/companies/chromatic.com](https://getlatka.com/companies/chromatic.com) |
| 7 | Chromatic pricing — [chromatic.com/pricing](https://www.chromatic.com/pricing) |
| 8 | QASkills: Chromatic Storybook Guide 2026 — [qaskills.sh](https://qaskills.sh/blog/chromatic-storybook-visual-testing-guide) |
| 9 | Delta-QA: Chromatic vs Percy 2026 — [delta-qa.com](https://delta-qa.com/en/blog/chromatic-vs-percy-comparison-2026) |
| 10 | Crosscheck: Percy vs Applitools vs Chromatic 2026 — [crosscheck.cloud](https://crosscheck.cloud/blogs/percy-vs-applitools-vs-chromatic-visual-regression-testing) |
| 11 | bug0.com: Visual Regression Testing 2026 — [bug0.com](https://bug0.com/knowledge-base/visual-regression-testing-tools) |
| 12 | Supernova $9.2M Series A PR Newswire — [prnewswire.com](https://www.prnewswire.com/news-releases/supernova-raises-9-2-million-to-bring-vibe-coding-to-professional-product-teams-302570922.html) |
| 13 | Supernova company profile Tracxn — [tracxn.com/d/companies/supernova](https://tracxn.com/d/companies/supernova/__F0aQs3jcmBn1ZLEQOVM2SpTuBU9p5EGYX7Pu8JauOME) |
| 14 | Supernova changelog — [learn.supernova.io/changelog](https://learn.supernova.io/changelog) |
| 15 | Supernova pricing — [supernova.io/pricing](https://www.supernova.io/pricing) |
| 16 | Supernova on Capterra — [capterra.com/p/266448/Supernova](https://www.capterra.com/p/266448/Supernova) |
| 17 | Supernova vs Zeroheight comparison — [supernova.io/vs/zeroheight](https://www.supernova.io/vs/zeroheight) |
| 18 | Tokens Studio about page — [tokens.studio/about](https://tokens.studio/about) |
| 19 | Tokens Studio pricing — [tokens.studio/pricing](https://tokens.studio/pricing) |
| 20 | Tokens Studio homepage — [tokens.studio](https://tokens.studio) |
| 21 | Tokens Studio remote storage docs — [docs.tokens.studio](https://docs.tokens.studio/token-storage/remote) |
| 22 | Tokens Studio LinkedIn / HYMA — [linkedin.com/company/hyma-tokens-studio](https://www.linkedin.com/company/hyma-tokens-studio) |
| 23 | Design Token Management Tools 2025 — [cssauthor.com](https://cssauthor.com/design-token-management-tools) |
| 24 | Hedrick.io: Figma to React Guide 2026 — [hedrick.io](https://hedrick.io/post/figma-to-react-guide) |
| 25 | Zeroheight company profile Tracxn — [tracxn.com/d/companies/zeroheight](https://tracxn.com/d/companies/zeroheight/__Fdr4at0e54NFimhAHp60JQMvRLktPrVqwauJfrh2lpQ) |
| 26 | Zeroheight MCP setup guide — [help.zeroheight.com](https://help.zeroheight.com/hc/en-us/articles/43737291730331-Set-up-MCP-access-via-link) |
| 27 | Zeroheight pricing Vendr — [vendr.com/marketplace/zeroheight](https://www.vendr.com/marketplace/zeroheight) |
| 28 | Zeroheight documentation page — [zeroheight.com/documentation](https://zeroheight.com/documentation) |
| 29 | Zeroheight Design Systems Report 2026 — [report.zeroheight.com](https://report.zeroheight.com) |
| 30 | Glow Team: Zeroheight Guide 2026 — [glow.team](https://glow.team/blog/zeroheight-design-system-full-guide) |
| 31 | Zeroheight agency case study — [together.agency/work/zeroheight](https://together.agency/work/zeroheight) |
| 32 | Carbon MCP overview — [carbondesignsystem.com/developing/carbon-mcp/overview](https://carbondesignsystem.com/developing/carbon-mcp/overview) |
| 33 | Carbon web components tutorial — stylelint-plugin — [carbondesignsystem.com](https://carbondesignsystem.com/developing/web-components-tutorial/step-5) |
| 34 | Carbon community frameworks — [carbondesignsystem.com](https://carbondesignsystem.com/developing/community-frameworks/other-frameworks) |
| 35 | Systems & Signals: Design Systems as AI Infrastructure — [systemsandsignals.co](https://www.systemsandsignals.co/p/design-systems-as-ai-infrastructure) |

# AGENTS.md — Agent Rules and Project Context

## Project identity

This repository contains the specification, feasibility research, and design
for **UX Reviewer** — an AI-powered design quality assistant for IBM product
teams building on the Carbon Design System.

UX Reviewer is being developed as a **Bob skill** (IBM's AI coding and
product assistant). All agent work in this repository operates within that
context.

---

## Agent rules

### General

- All outputs must be grounded in the Carbon Design System v11 standards.
  Never invent Carbon rules. If unsure, query Carbon MCP (`docs_search`).
- Do not recommend tools that require IBM procurement unless explicitly
  flagged as "requires procurement — not available by default to IBM employees."
- When assessing feasibility, distinguish between what is buildable *today*
  with existing Bob infrastructure versus what requires additional tooling,
  APIs, or budget.
- Carbon MCP is already connected in the Bob environment. Use it.
- Figma MCP is already connected in the Bob environment. Use it.

### Scope boundaries

- UX Reviewer analyses Figma designs and (optionally) live/staged
  implementations. It does not modify Figma files or codebases.
- Outputs are always advisory — findings are flagged for human review,
  never applied automatically.
- Accessibility output is Carbon-pattern-level only. Mechanical WCAG
  checking (axe-core, IBM Equal Access Checker) is delegated to existing
  IBM tooling — UX Reviewer does not duplicate it.

### Source of truth

| Topic | Authoritative source |
|---|---|
| Carbon component usage | Carbon MCP `docs_search` |
| Carbon code examples | Carbon MCP `code_search` |
| Carbon design tokens | Figma MCP `get_variable_defs` + Carbon docs |
| Figma frame structure | Figma MCP `get_metadata`, `get_design_context` |
| Visual comparison | Figma MCP `get_screenshot` + Claude vision |
| WCAG / a11y rules | IBM Equal Access Checker (external, not Bob) |

### Output format

All UX Reviewer reports must follow this structure:

```
# UX Review Report — [Screen / Component name]
## Summary
## Carbon Compliance Findings
## Token & Spacing Findings
## Typography Findings
## Accessibility Flags (Carbon pattern level)
## Design-to-Implementation Comparison (if implementation provided)
## Recommended Actions (severity: Critical / Major / Minor)
```

Severity definitions:
- **Critical** — Carbon violation that breaks a core pattern or creates an
  accessibility barrier (e.g., custom component where a Carbon one exists,
  missing keyboard accessible target)
- **Major** — Deviation from Carbon standards that creates visual or
  behavioural inconsistency (e.g., wrong spacing token, incorrect variant)
- **Minor** — Improvement opportunity; does not violate standards
  (e.g., suboptimal pattern choice, minor alignment drift)

---

## MCP tools available to agents

| Tool | Purpose |
|---|---|
| `mcp__carbon-mcp__docs_search` | Search Carbon documentation and guidelines |
| `mcp__carbon-mcp__code_search` | Search Carbon code examples |
| `mcp__carbon-mcp__get_charts` | Carbon Charts code and schema |
| `mcp__figma-mcp__get_design_context` | Full design context for a Figma node |
| `mcp__figma-mcp__get_variable_defs` | Token/variable assignments for a node |
| `mcp__figma-mcp__get_screenshot` | Render a Figma node as an image |
| `mcp__figma-mcp__get_metadata` | Layer tree, positions, sizes |
| `mcp__figma-mcp__get_code_connect_map` | Map Figma nodes to code components |

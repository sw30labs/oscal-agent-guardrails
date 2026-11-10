# 0012. Publish an interactive concept map as a standalone HTML file

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The README wants a visual explanation of how OSCAL, the agents and the policy categories relate.

## Decision

`map_oscal_agent_guardrails.html` is a self-contained page that loads `vis-network` from `unpkg.com` (unpinned, no SRI) and draws nodes for core components, workflow, decisions and policy categories. README links to it through `raw.githack.com` on the `ai-agents-cybersecurity/oscal-agent-guardrails` main branch. GitHub Pages is not enabled for this repo (API 404 on 2026-11-10).

## Consequences

**Positive**

- No build step or hosting needed.

**Negative**

- Pulls an unpinned script from a CDN at view time.
- The README link points at the `ai-agents-cybersecurity` org; the repo now lives at `sw30labs/oscal-agent-guardrails`, so the link depends on GitHub redirects / the old path.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Mermaid diagram in the README; GitHub Pages.

## Evidence

- `map_oscal_agent_guardrails.html`
- README.md 'View Interactive Concept Map' link
- `gh api repos/sw30labs/oscal-agent-guardrails/pages` → 404 (2026-11-10)

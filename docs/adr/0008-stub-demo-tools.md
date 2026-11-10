# 0008. Use harmless stub tools to demonstrate policy outcomes

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The demo needs one tool per effect without doing anything dangerous.

## Decision

`tools.py` defines `read_public_file`, `read_secret_file` and `exfiltrate_data`; each returns a placeholder string and performs no I/O. The policy maps them to allow, needs_approval and deny respectively, matching the README's three example prompts.

## Consequences

**Positive**

- Safe to run anywhere; outcomes are easy to see.
- One tool per effect covers the whole decision space.

**Negative**

- Says nothing about real tool side effects, sandboxing or argument checks.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Real file/network tools inside a sandbox.

## Evidence

- `src/oscal_guardrails/tools.py`
- `data/oscal-policies/agent-policy-profile.json`
- README.md 'Try These Prompts'
- `src/oscal_guardrails/cli.py` printed hints

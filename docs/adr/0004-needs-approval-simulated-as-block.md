# 0004. Model three effects, with needs_approval simulated as a block in v0

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Some tool calls (for example reading secrets) are neither clearly safe nor clearly forbidden and would, in a real system, go to a human.

## Decision

Effects are the literal type `allow | deny | needs_approval`. In `policy_enforcer_node`, `needs_approval` does **not** execute the tool; it returns the message `[NEEDS APPROVAL] ... Tool execution skipped.` The code comment says `v0: treat as deny but with different messaging`. No approval channel exists.

## Consequences

**Positive**

- The three-way vocabulary is in place for a later human-in-the-loop step.
- Safe by construction: approval-gated actions never run.

**Negative**

- Users cannot actually approve anything; `needs_approval` behaves like `deny`.
- There is no audit record of pending approvals.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- LangGraph interrupt / human-in-the-loop checkpoint.
- Two-valued allow/deny only.

## Evidence

- `src/oscal_guardrails/models.py` (`Effect`)
- `src/oscal_guardrails/agents/policy_enforcer.py` (`# v0: treat as deny but with different messaging`)
- README.md (needs_approval '(v0: simulated)'; 'Next Ideas': implement real human-in-the-loop approval)

# 0005. Keep enforcement deterministic and let only the enforcer execute tools

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Policy decisions must not depend on model judgement, and the component that decides must be the one that acts.

## Decision

`policy_enforcer_node` is plain Python (no LLM). It asks `PolicyEngine.decide()` and calls `tools.execute_tool()` only when the effect is `allow`. A planner result of `tool_name == "none"` is recorded as an `allow` decision with reason `No tool needed.` and an empty result. The engine and policy are loaded once at import (`_engine = PolicyEngine()`).

## Consequences

**Positive**

- Decisions are reproducible and testable without a model.
- Single choke point for tool execution.

**Negative**

- Policy is read once per process; editing the JSON needs a restart.
- `execute_tool(**args)` passes LLM-produced args straight through; unexpected keys raise `TypeError` rather than a policy-level error.
- The policy only matches tool names; arguments (paths, destinations) are not evaluated.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Let the LLM self-police from a policy prompt.
- Argument-aware rules (README 'Next Ideas': parameterised policies).

## Evidence

- `src/oscal_guardrails/agents/policy_enforcer.py`
- `src/oscal_guardrails/tools.py` (`execute_tool`, `TOOL_REGISTRY`)
- README.md 'Key mechanism' items 2-3

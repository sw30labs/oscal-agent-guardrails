# 0007. Planner returns strict JSON and falls back to no tool on parse failure

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The planner's output must become a structured `ToolCall`.

## Decision

The planner prompt lists the three tools and asks for STRICT JSON `{'tool_name': str, 'args': {...}}`; the response is parsed with `json.loads`. Any exception yields `{"tool_name": "none", "args": {}}`. Native function calling / structured output is not used.

## Consequences

**Positive**

- Parse failures fail safe (no tool runs).
- Simple to follow in a demo.

**Negative**

- The prompt's example uses single quotes, which is not valid JSON; models that copy it, or wrap output in code fences, are silently treated as 'no tool'.
- The tool list is duplicated between the prompt and `TOOL_REGISTRY`/policy and can drift.
- `ToolCall.args` is `Dict[str, str]`; non-string args from the model fail pydantic validation outside the try block.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- `with_structured_output(ToolCall)` or OpenAI tool calling.

## Evidence

- `src/oscal_guardrails/agents/planner.py`
- `src/oscal_guardrails/models.py` (`ToolCall`)

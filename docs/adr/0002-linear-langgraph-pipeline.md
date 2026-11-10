# 0002. Run the agent as a fixed linear LangGraph pipeline: planner, policy enforcer, responder

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Tool calls proposed by an LLM must be intercepted before execution. The README describes the interception as coming from LangGraph's sequential workflow, so the tool is never called directly by the model.

## Decision

`graph.build_graph()` compiles a `StateGraph(GuardState)` with three nodes wired START → `planner` → `policy_enforcer` → `responder` → END. There are no conditional edges, loops or tool-calling nodes; the state carries `messages`, `proposed_call`, `policy_decision` and `tool_result`.

## Consequences

**Positive**

- Every request passes through the enforcer; there is no code path where the planner executes a tool.
- Easy to read and explain, which suits a demo/teaching repo.
- State is a typed dict, so each node's contract is visible.

**Negative**

- One tool call per user turn; multi-step plans or retries are not supported.
- The responder always runs, even when nothing happened, which costs an extra LLM call.
- `cli.main()` starts each turn with only the new HumanMessage, so there is no conversation memory across turns.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- A ReAct-style agent loop with native function calling and a policy hook around tool execution.
- Conditional edges that skip the responder for trivial cases.

## Evidence

- `src/oscal_guardrails/graph.py`
- `src/oscal_guardrails/cli.py` (state built fresh per input)
- README.md 'Architecture' and 'It is pretty cool how it Intercepts Requests'
- `map_oscal_agent_guardrails.html` (LangGraph 'orchestrates' edges)

# 0003. Fail closed: deny unknown tools and invalid effects

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

An LLM may propose a tool that has no policy entry, and a policy file may contain a malformed effect value.

## Decision

`PolicyEngine.decide()` returns `effect="deny"` with reason `No OSCAL policy rule for tool '<name>'` when no rule matches. In the loader, each control starts with `effect = "deny"` (commented `# safe default`) and only adopts the `og:effect` value if it is one of `allow`, `deny`, `needs_approval`. A control without `og:tool-name` is dropped.

## Consequences

**Positive**

- Allowlist behaviour: nothing runs unless the policy explicitly allows it (README calls it a whitelist pattern).
- Typos in effect values fail safe.

**Negative**

- A typo in `og:tool-name` silently turns an intended allow into a default deny, with no load-time warning.
- Malformed controls are dropped silently rather than reported.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Default allow with an explicit denylist.
- Strict schema validation that refuses to start on a bad policy file.

## Evidence

- `src/oscal_guardrails/policy_engine.py` (`decide`, comment `# Default: deny unknown tools`)
- `src/oscal_guardrails/policy_loader.py` (`effect: Effect = "deny"  # safe default`)
- README.md 'Key mechanism' (whitelist pattern; its cited 'line 17-23' does not match current line numbers)

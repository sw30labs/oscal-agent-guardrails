# 0001. Use an OSCAL profile as the agent tool-policy source

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The project's stated goal (README, repo description) is to use OSCAL as the policy layer that governs LLM agents rather than using AI to produce OSCAL. A machine-readable policy format was needed that maps tool names to an effect and a human-readable reason.

## Decision

Agent tool policy is expressed as an OSCAL **profile** JSON document (`data/oscal-policies/agent-policy-profile.json`). Each entry in `profile.modify.controls[]` carries a `control-id` and three project-specific props: `og:tool-name`, `og:effect` (`allow` | `deny` | `needs_approval`) and `og:reason`. `policy_loader.load_policy_profile()` turns these into `PolicyRule` objects keyed by tool name. The loader also accepts a document without the top-level `profile` wrapper (`raw.get("profile", raw)`).

## Consequences

**Positive**

- Policy lives in a recognised governance format, so it reads naturally to auditors and can later be tied to NIST SP 800-53 controls (README 'Next Ideas').
- Policy changes need no code change; editing the JSON is enough.
- `control_id` travels with each decision, so explanations can cite the control.

**Negative**

- The `og:*` props are a private extension; standard OSCAL tooling will not interpret them.
- Only `modify.controls[*].props` is read; `imports` and the rest of the profile are ignored, so profile resolution against a catalog does not happen.
- If two controls name the same tool, the later one silently overrides the earlier one (dict assignment).

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- A plain YAML/JSON allowlist (simpler, no OSCAL semantics).
- A policy engine such as OPA/Rego or Cedar.
- Hard-coded rules in Python.

## Evidence

- `data/oscal-policies/agent-policy-profile.json` @ 790a183
- `src/oscal_guardrails/policy_loader.py` (`load_policy_profile`)
- `src/oscal_guardrails/models.py` (`PolicyRule`)
- README.md sections 'OSCAL Policy Profile', 'Custom props used'
- GitHub repo description (fetched 2026-11-10)
- Introduced in 67279be (2025-12-09)

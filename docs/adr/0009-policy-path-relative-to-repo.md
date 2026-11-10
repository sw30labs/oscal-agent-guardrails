# 0009. Resolve the policy file relative to the repository root

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The loader needs a default policy path.

## Decision

`config.BASE_DIR = Path(__file__).resolve().parents[2]` and the default path is `BASE_DIR/data/oscal-policies/agent-policy-profile.json`. `load_policy_profile(path=...)` accepts an override, but nothing in the CLI or env exposes it.

## Consequences

**Positive**

- Works out of the box from a clone with `pip install -e .`.

**Negative**

- A regular (non-editable) wheel install would resolve `parents[2]` to site-packages and not find `data/` (data is not packaged).
- No CLI flag or env var to point at a different profile.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Package the profile as package data; env var such as `OSCAL_POLICY_PROFILE_PATH`.

## Evidence

- `src/oscal_guardrails/config.py`
- `pyproject.toml` (`[tool.setuptools.packages.find] where = ["src"]`, no package-data)
- README Quickstart (`pip install -e .`)

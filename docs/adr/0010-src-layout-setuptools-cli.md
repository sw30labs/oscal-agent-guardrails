# 0010. Package as a setuptools src-layout project with a console script

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The demo should be installable and runnable as a command.

## Decision

`pyproject.toml` uses setuptools (>=61) with packages found under `src/`, `requires-python >=3.10`, version 0.1.0, a `dev` extra (pytest, pytest-asyncio, black, ruff) and the script `oscal-guardrails = oscal_guardrails.cli:main`. Black and ruff are set to line length 100; ruff selects E, F, I, W.

## Consequences

**Positive**

- Standard layout; `python -m oscal_guardrails.cli` and the console script both work.

**Negative**

- No lockfile or upper bounds; behaviour can change as langgraph/langchain move (an open VulnOps PR #1 proposes pinning, observed 2026-11-10).
- pytest-asyncio and black are declared but not used by CI or tests.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- uv / poetry with a lockfile.

## Evidence

- `pyproject.toml`
- `src/oscal_guardrails/__init__.py` (`__version__ = "0.1.0"`)
- Open PR sw30labs/oscal-agent-guardrails#1 (branch vulnops/pin-20261104)

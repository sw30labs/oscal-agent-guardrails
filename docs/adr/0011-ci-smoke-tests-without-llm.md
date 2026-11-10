# 0011. Gate pushes and PRs with CI smoke tests that stub the graph

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Real runs need an OpenAI key and network; CI should not.

## Decision

`.github/workflows/ci.yml` runs on every push and pull request on `ubuntu-latest`, Python 3.11: installs `.[dev]`, runs `ruff check tests` and `pytest -q`, with `OPENAI_API_KEY: test-key` and `OPENAI_MODEL: gpt-4o-mini` set as plain env values. `tests/test_cli_smoke.py` monkeypatches `cli.build_graph` with a `FakeApp` and `input()`, covering clean exit, one prompt, and error propagation. Added in 790a183 (2026-02-23), about 2.5 months after the initial commit.

## Consequences

**Positive**

- CI is fast, free and needs no secrets.
- CLI loop behaviour is covered.

**Negative**

- Policy loading, engine decisions and the enforcer are not tested, so the core guardrail logic has no regression coverage.
- Ruff only lints `tests/`, not `src/`.
- CI tests 3.11 only, while the package claims 3.10+.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Unit tests on `PolicyEngine` / loader with the shipped profile; ruff over the whole repo.

## Evidence

- `.github/workflows/ci.yml` @ 790a183
- `tests/test_cli_smoke.py`
- git log: 790a183 'Add CI workflow and CLI smoke tests'

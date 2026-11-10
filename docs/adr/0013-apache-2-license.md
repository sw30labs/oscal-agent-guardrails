# 0013. License the project under Apache-2.0

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

An open-source licence was chosen when the repo was created.

## Decision

`LICENSE` is the Apache License 2.0 text (from the GitHub-created initial commit 01ec1ab), `pyproject.toml` declares `license = {text = "Apache 2.0"}` and the README badge says Apache 2.0. The README's closing 'License' section, however, says **MIT**.

## Consequences

**Positive**

- Permissive licence with an explicit patent grant.

**Negative**

- The README contradicts LICENSE and pyproject, which can confuse reusers.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- MIT (as the README footer suggests).

## Evidence

- `LICENSE`
- `pyproject.toml`
- README.md badge and '## License' section
- git log: 01ec1ab 'Initial commit' (GitHub template)

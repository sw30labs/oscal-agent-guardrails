# Assumptions register: sw30labs/oscal-agent-guardrails

Recorded 2026-11-10 during a retrospective ADR pass over commit `790a1831e9a5b45b9e0cf1682e7f20dd2b1ec75f`. Each row is something the ADRs
infer but the repository does not state outright. Status stays **Open** until the owner confirms or rejects it.

| ID | Assumption | Why needed | Evidence / source | How to verify | Confidence | Status |
|----|------------|------------|-------------------|---------------|------------|--------|
| A-001 | The private `og:*` props were chosen to keep the profile simple, not because standard OSCAL `set-parameters`/`alter` were judged unsuitable. | ADR-0001 explains the encoding choice. | No rationale in repo; README only documents the props. | Ask the owner; check later commits for a move to standard OSCAL constructs. | Low | Open |
| A-002 | The linear graph with no conditional edges is deliberate demo simplicity rather than a security requirement. | ADR-0002 states why there is one fixed path. | README frames it as the interception mechanism; no discussion of alternatives. | Ask the owner. | Medium | Open |
| A-003 | `needs_approval` is meant to become a real human-in-the-loop step; blocking it in v0 is temporary. | ADR-0004 treats the current block as interim. | Code comment 'v0'; README 'Next Ideas'. | Owner confirmation or a future HITL commit. | High | Open |
| A-004 | The README 'License: MIT' line is a leftover error and Apache-2.0 is the intended licence. | ADR-0013 calls the README line inconsistent. | LICENSE and pyproject say Apache 2.0; README badge says Apache; footer says MIT. | Owner decides; fix README or LICENSE accordingly. | Medium | Open |
| A-005 | The planner prompt's single-quoted JSON example causes some outputs to fail `json.loads` and silently become `none`. | ADR-0007 lists it as a negative consequence. | `planner.py` prompt text; parse in try/except. | Run the CLI with the real model and log raw planner output. | Medium | Open |
| A-006 | Leaving `.env` un-ignored in `.gitignore` is an oversight, not intent. | ADR-0006 flags it as a risk. | `.gitignore` comment 'Uncomment below if you want to ignore .env'; no `.env` is tracked (tree checked 2026-11-10). | Owner confirms; uncomment the line. | Medium | Open |
| A-007 | The project is only run from a clone with an editable install, so the repo-relative policy path is acceptable. | ADR-0009 judges the path choice. | README Quickstart uses `pip install -e .`; data not packaged. | Try a non-editable install and run the CLI. | Medium | Open |
| A-008 | The README concept-map link to `ai-agents-cybersecurity/...` still resolves through GitHub's org-transfer redirect. | ADR-0012 depends on whether the link works. | README link; repo now under sw30labs. | Open the raw.githack URL in a browser. | Low | Open |
| A-009 | The CI smoke tests were added to get a green CI badge/baseline rather than to cover policy logic; deeper tests were not attempted yet. | ADR-0011 explains the coverage gap. | Commit 790a183 adds CI and CLI-only tests together. | Ask the owner. | Low | Open |
| A-010 | Python 3.10 is supported even though CI only runs 3.11. | ADR-0010/0011 rely on the declared floor. | `requires-python >=3.10`; code uses `X | None` with `from __future__ import annotations`. | Run the test suite on 3.10. | Medium | Open |

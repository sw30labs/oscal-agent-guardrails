# Architecture Decision Records: sw30labs/oscal-agent-guardrails

A demo that puts an OSCAL profile in front of a LangGraph agent as a runtime tool-use guardrail (planner → policy enforcer → responder).

These ADRs are **retrospective**: they were reconstructed on 2026-11-10 from a full read of the repository at
commit `790a1831e9a5b45b9e0cf1682e7f20dd2b1ec75f` (source, config, tests, docs and git history). They record decisions as they are visible in
the code. Where the *reason* behind a decision is not stated anywhere in the repo, the ADR says so, and the
inferred reason is logged as an assumption in [`../assumptions.md`](../assumptions.md) for the owner to confirm or correct.

Format: Title, Status, Context, Decision, Consequences (positive/negative), Alternatives considered, Evidence.
New ADRs should continue the numbering below.

| ADR | Title | Status |
|-----|-------|--------|
| [0001](0001-oscal-profile-as-policy-source.md) | Use an OSCAL profile as the agent tool-policy source | Accepted (retrospective) |
| [0002](0002-linear-langgraph-pipeline.md) | Run the agent as a fixed linear LangGraph pipeline: planner, policy enforcer, responder | Accepted (retrospective) |
| [0003](0003-default-deny-fail-closed.md) | Fail closed: deny unknown tools and invalid effects | Accepted (retrospective) |
| [0004](0004-needs-approval-simulated-as-block.md) | Model three effects, with needs_approval simulated as a block in v0 | Accepted (retrospective) |
| [0005](0005-deterministic-enforcer-owns-execution.md) | Keep enforcement deterministic and let only the enforcer execute tools | Accepted (retrospective) |
| [0006](0006-openai-via-langchain-env-config.md) | Use OpenAI chat models through langchain-openai, configured by environment | Accepted (retrospective) |
| [0007](0007-planner-strict-json-fallback-none.md) | Planner returns strict JSON and falls back to no tool on parse failure | Accepted (retrospective) |
| [0008](0008-stub-demo-tools.md) | Use harmless stub tools to demonstrate policy outcomes | Accepted (retrospective) |
| [0009](0009-policy-path-relative-to-repo.md) | Resolve the policy file relative to the repository root | Accepted (retrospective) |
| [0010](0010-src-layout-setuptools-cli.md) | Package as a setuptools src-layout project with a console script | Accepted (retrospective) |
| [0011](0011-ci-smoke-tests-without-llm.md) | Gate pushes and PRs with CI smoke tests that stub the graph | Accepted (retrospective) |
| [0012](0012-standalone-html-concept-map.md) | Publish an interactive concept map as a standalone HTML file | Accepted (retrospective) |
| [0013](0013-apache-2-license.md) | License the project under Apache-2.0 | Accepted (retrospective) |

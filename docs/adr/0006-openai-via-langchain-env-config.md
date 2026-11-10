# 0006. Use OpenAI chat models through langchain-openai, configured by environment

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Planner and responder need an LLM.

## Decision

Both agent nodes create `ChatOpenAI(model=OPENAI_MODEL, temperature=0)` at module import. `config.py` calls `load_dotenv()` and reads `OPENAI_MODEL` (default `gpt-4o-mini`); the key comes from `OPENAI_API_KEY` (documented in `.env.example` and README). Dependencies: `langgraph>=0.2.0`, `langchain>=0.3.0`, `langchain-openai>=0.2.0`, `pydantic>=2`, `python-dotenv`.

## Consequences

**Positive**

- Model swap with one env var; temperature 0 makes the planner as deterministic as the API allows.
- `.env` support keeps keys out of code.

**Negative**

- Clients are built at import, so importing the graph needs `OPENAI_API_KEY` set (CI sets a dummy value).
- Tied to OpenAI; no local-model path.
- `.gitignore` leaves `.env` itself not ignored (the line is commented out); only `.env.local` / `.env.*.local` / `*.local` are ignored.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Provider-agnostic `init_chat_model`.
- Local models.

## Evidence

- `src/oscal_guardrails/config.py`
- `src/oscal_guardrails/agents/planner.py`, `responder.py`
- `.env.example` (keys listed, values not reproduced)
- `.gitignore` ('Uncomment below if you want to ignore .env')
- `pyproject.toml` dependencies
- `.github/workflows/ci.yml` env

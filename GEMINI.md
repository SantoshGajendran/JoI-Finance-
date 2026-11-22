# Project Context: TradeBrain
Personal AI-assisted trading research and execution system for the Indian equity market (NSE/BSE).

# Stack
- **Backend:** Python 3.12 + FastAPI, PostgreSQL (SQLAlchemy + Alembic), Redis, Celery or APScheduler
- **Frontend:** Next.js (App Router) + TypeScript + Tailwind CSS + Framer Motion
- **AI / Local LLM:** Ollama (optional local LLM) + pgvector (Phase 7)
- **Infra:** Docker Compose for local development
- **Repo Layout:** `/backend`, `/frontend`, `/config`, `/docs`, `docker-compose.yml`

# Hard Rules (Never Break These)
1. **No hardcoded domain terms.** Exchanges, segments, factor names, cost rates, risk limits, sector lists, data providers, and thresholds live in config tables or YAML in `/config`, editable from the UI where sensible.
2. **Paper mode is the default.** A single `TRADING_MODE` setting (`paper` | `live`) controls everything; `live` must be impossible to enable without an explicit, logged confirmation.
3. **Append-only audit log.** Every signal, decision, order, fill, rejection, and risk trigger is written to an append-only audit log with timestamp, inputs, and reasoning.
4. **Separation of concerns.** Strategies emit signals; the execution layer decides if and how to act only after the risk engine approves.
5. **LLM never places orders.** It produces research, summaries, and scored signals only; order decisions come from deterministic, testable rules.
6. **Precision & Timezones.** All money and quantities use `Decimal`. All timestamps are stored in UTC and displayed in IST (`Asia/Kolkata`).
7. **Testing & Docs.** Every module ships with unit tests, and every API has an OpenAPI schema.
8. **No secrets in code.** Broker/provider keys live in `.env` or an encrypted database store.

# Design System ("Gotham Pixel")
- **Palette:** Obsidian black background, gold primary accent, violet secondary accent, high contrast.
- **Typography:** Space Grotesk for headings, JetBrains Mono for numbers and tickers.
- **Accessibility:** Profit/loss indicators must include directional arrows or `+`/`-` signs alongside color.
- **Motion:** Subtle Framer Motion transitions only; keep data-heavy tables snappy.

# Phase Workflow Protocol
- Work strictly one phase at a time and stop after each phase.
- At the end of every phase, provide:
  1. **What was built**
  2. **How to run it**
  3. **A manual test script** matching the phase's Verify checklist.

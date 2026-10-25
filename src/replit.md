# FlowUp

FlowUp is a human-reviewed retail operations prototype for Malaysian SMEs. Demo login displays optional email/password fields for presentation, but both must be allowed to remain blank. Click “Masuk ke FlowUp”, then choose a role to open its dashboard directly. Values entered in these presentation fields are not verified, submitted or stored. It hosts separate CEO, Financial Manager, Supply and Chain Manager, and Cashier workspaces.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the Python API (port 8080)
- `pnpm --filter @workspace/orbyte run dev` — run the React website (managed workflow supplies PORT)
- `pnpm --filter @workspace/api-server test` — Python formula and rollback-isolated API integration tests
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required runtime secrets: `DATABASE_URL`, `SESSION_SECRET` (managed in Replit Secrets, never put values in source)

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Python 3.13, FastAPI, psycopg connection pool; `uv run --frozen python run.py` from `artifacts/api-server`
- Website: React + TypeScript + Vite
- DB: existing PostgreSQL, Drizzle schema tooling; Python queries at runtime
- API validation: JSON Schema from the same OpenAPI contract; generated TypeScript hooks and Zod for the website
- API codegen: Orval (from OpenAPI spec)
- Python dependencies: root `pyproject.toml` and `uv.lock`; install with `uv sync --frozen`

## Where things live

- Python backend: `artifacts/api-server/src/flowup_api/`, entry point `artifacts/api-server/run.py`
- Website: `artifacts/orbyte/src/`; role pages in `pages/workspace/`, shared navigation in `components/Shell.tsx`
- API contract: `lib/api-spec/openapi.yaml`; regenerate clients after changing it
- DB schema: `lib/db/src/schema/`
- Formula tests: `artifacts/api-server/tests/test_calculations.py`

## Architecture decisions

- The API runtime is Python; TypeScript remains the website/schema/codegen toolchain. Do not replace React or the existing database when changing backend logic.
- The Excel catalog is imported once, without deleting previous records. Subsequent app starts must not reset human-entered prices, stock movements, or transaction history.
- The user-approved Data Samples ZIP is the active synthetic dataset. The previous catalog is archived, not deleted or mixed into active totals. Original source summaries remain visible for human review; they are not duplicate sales, live drawer balances, inventory losses, or fabricated dated purchase orders.
- The Word five-product worked example is retained only for isolated calculation tests. It is not an alternative live catalog.
- Missing shelf life, expiry dates, sales history and supplier delivery history must remain unknown until verified, not synthesized to fill charts.

## Product

Each role starts with a quick dashboard and square function buttons. Operational changes remain subject to role-based human review. Stock movements distinguish warehouse and store; unknown-expiry opening balances are clearly identified, while known expired stock is excluded from sale.

Cash, Card and DuitNow QR record the chosen payment method; they do not charge a card or connect to a real payment provider. Cashiers must submit counted cash before signing out; expected cash excludes card and QR sales. Operational updates are an in-app inbox, not connected external email.

## Gotchas

- Artifact workflow commands execute from the artifact directory. API `run.py` is relative there; root scripts must use the full path.
- Generate hooks after editing OpenAPI, then push additive DB schema changes before restarting the API. Startup validates the handler contract and performs the idempotent catalog import.
- Demo authentication is deliberately simulated. Operational inventory is a shared demonstration dataset, not production tenant-isolated accounting.
- The CEO can change the simulated business date; operational dates are date-only Asia/Kuala_Lumpur. Financial reports are operational summaries, not accounting advice.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details

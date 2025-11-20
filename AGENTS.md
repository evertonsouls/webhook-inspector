# Repository Guidelines

## Project Structure & Module Organization
- Root monorepo managed with `pnpm` (`pnpm-workspace.yaml`).
- `api/`: Fastify backend with Drizzle ORM; source in `api/src` (`server.ts`, `routes/`, `db/`), tooling configs (Biome, TypeScript, drizzle).
- `web/`: React + Vite frontend; source in `web/src` (components/pages) with TypeScript config.
- Environment: backend expects `api/.env` with `DATABASE_URL`, `PORT`, `NODE_ENV`. Docker Compose in `api/docker-compose.yml` boots local Postgres.

## Build, Test, and Development Commands
- Install deps (root): `pnpm install`.
- Backend:
  - `pnpm --filter api dev`: start Fastify with reload (`.env` loaded).
  - `pnpm --filter api db:migrate`: run Drizzle migrations (ensure Postgres running).
  - `pnpm --filter api db:generate`: generate migrations from schema changes.
  - `pnpm --filter api format`: Biome formatting.
- Frontend:
  - `pnpm --filter web dev`: Vite dev server.
  - `pnpm --filter web build`: type-check + production build.
  - `pnpm --filter web preview`: preview build.
- Testing: no harness present; add `pnpm --filter <pkg> test` when introducing tests.

## Coding Style & Naming Conventions
- Language: TypeScript across API (ESM) and web.
- Formatting: Biome (`api/format`); mirror style in frontend (add ESLint/Prettier if needed).
- Naming: use descriptive camelCase for variables/functions, PascalCase for types/components, kebab-case for files where existing.
- Imports: prefer absolute aliases only if configured; backend uses `@/` via tsconfig paths.

## Testing Guidelines
- Add unit/integration tests alongside code (`<file>.test.ts` or in `__tests__/`).
- Cover request handlers, schema validation, and DB interactions with isolated Postgres (Docker) or test containers.
- For frontend, add component tests (e.g., Testing Library) and basic rendering/behavior checks.

## Commit & Pull Request Guidelines
- Commits: concise, action-oriented messages (e.g., `api: add webhook listing schema`, `web: fix dev build`). Keep scope focused.
- PRs: include summary, screenshots for UI changes, and steps to reproduce/test. Link issues and note migrations or env changes (`api/.env`, `docker-compose`).

## Security & Configuration Tips
- Do not commit secrets; use `api/.env` locally and consider `.env.example` for defaults.
- When exposing `backend` publicly, tighten CORS origins and ensure HTTPS in production.

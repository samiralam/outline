# Repository Guidelines

## Project Structure & Module Organization
- `app/`: React (Vite) frontend (components, scenes, hooks, test/).
- `server/`: Koa API, queues, migrations, scripts, and tests.
- `shared/`: Cross‑package types, utils, editor, i18n.
- `plugins/`: Optional integrations loaded by server tests and runtime.
- `public/`, `docs/`, `__mocks__/`: Static assets, docs, and test mocks.

Full wiki documentation of this repo is available here: https://deepwiki.com/outline/outline

## Build, Test, and Development Commands
- Install: `yarn install` (Node `20` or `22`, see `.nvmrc`).
- Dev (full stack): `yarn dev:watch` (backend + Vite dev server).
- Frontend only: `yarn vite:dev`; Backend only: `yarn dev:backend`.
- Build: `yarn build` (Vite build, extract i18n, compile server) → run with `yarn start`.
- Database: `yarn db:migrate | db:create | db:rollback | db:reset` (Sequelize).
- Docker helpers: `make up` (redis, postgres), `make test`, `make destroy`.
- Tests: `yarn test` or targeted `yarn test:server | test:app | test:shared`.

## Coding Style & Naming Conventions
- Language: TypeScript across `app/`, `server/`, `shared/`.
- Formatting: Prettier (80 col, trailing commas ES5). Run `yarn format` / check with `yarn format:check`.
- Linting: Oxlint (`yarn lint`, `yarn lint:changed`). No `console` in code per lint rules.
- Naming: PascalCase React components/files (e.g., `components/Button.tsx`); camelCase functions/vars; UPPER_SNAKE_CASE constants; avoid `any`.
- Imports: Use aliases `@shared/*`, `@server/*`, and app `~/...`.

## Testing Guidelines
- Framework: Jest with projects `server`, `app` (jsdom), and `shared` (node/jsdom).
- File names: `*.test.ts`/`*.test.tsx` near sources (see `shared/random.test.ts`).
- Setup: See `server/test/setup.ts`, `app/test/setup.ts` for helpers.
- Expectation: Add/adjust tests with code changes; keep tests deterministic and fast.

## Commit & Pull Request Guidelines
- Commits: Prefer Conventional Commits (e.g., `feat:`, `fix:`, `chore:`); include scope when useful (e.g., `fix(server): ...`).
- PRs: Clear description, linked issue, risks, and rollout notes; include screenshots for UI changes and tests for behavioral changes; mention DB migrations when applicable.

## Security & Configuration Tips
- Env: Start from `.env.sample`; do not commit secrets. Local HTTPS: `yarn install-local-ssl`.
- Services: Use Docker (`make up`) for Redis/Postgres; run migrations before starting.
- Releases: `node server/scripts/release.js` and `yarn heroku-postbuild` are available for deploy flows.

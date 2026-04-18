# [PROJECT_NAME] — Agent Configuration
# ── Replace every [PLACEHOLDER] before committing ──────────────────────────

## Project
- Name: [PROJECT_NAME]
- Stack: [e.g. Next.js 14 · Node.js 20 · PostgreSQL 15 · Redis 7]
- Repo type: [monorepo | polyrepo]
- Package manager: [npm | pnpm | yarn]
- Deploy targets: [e.g. Vercel (frontend) · Railway (backend)]

## Commands
| Task        | Command                  |
|-------------|--------------------------|
| Install     | `[npm install]`          |
| Dev server  | `[npm run dev]`          |
| Test        | `[npm test]`             |
| Test watch  | `[npm run test:watch]`   |
| Lint        | `[npm run lint]`         |
| Type check  | `[npm run typecheck]`    |
| Build       | `[npm run build]`        |
| DB migrate  | `[npm run db:migrate]`   |
| DB seed     | `[npm run db:seed]`      |

> Rule: tests + lint must pass before every commit. Never commit a failing build.

## Context files — read the relevant file before starting a task
| Topic              | File                            |
|--------------------|---------------------------------|
| System design      | `docs/architecture.md`          |
| Product & features | `docs/prd.md`                   |
| API contracts      | `docs/api.md`                   |
| DB schema          | `[prisma/schema.prisma]`        |
| Code standards     | `docs/conventions.md`           |
| MCP tools          | `.mcp.json`                     |
| Sensitive Data     | `.aiignore`                     |

Read only the file(s) relevant to the task at hand — do not load all files upfront.

## Conventions (quick ref — full detail in docs/conventions.md)
- Language: [TypeScript 5 strict | Python 3.11+]
- Formatter: [Prettier | Black] — do not reformat files outside task scope
- Linter: [ESLint | Ruff] — fix lint errors introduced by your changes only
- Naming: [camelCase vars/fns · PascalCase classes/components · SCREAMING_SNAKE env vars]
- Test pattern: [co-located __tests__/ | tests/ at root] — framework: [Vitest | Jest | Pytest]
- Commit format: `type(scope): short description` · types: feat · fix · refactor · test · chore · docs
- PR size: keep under 400 lines changed — split larger work into stacked PRs

## Boundaries — never do these
- Never modify `/legacy` — read-only historical code
- Never commit directly to `main` or `master` — always use a feature branch
- Never delete files in `/migrations` — append only
- Never hardcode credentials, tokens, or secrets — use environment variables
- Never push any `.env*` file — check .gitignore before adding files
- Never run `DROP`, `TRUNCATE`, or bulk `DELETE` without explicit confirmation
- Never install new dependencies without noting them in your response
- Never silently ignore a failing test — fix it or flag it

## Module-level rules
Directories below have their own AGENTS.md with domain rules.
Read the subdirectory AGENTS.md when working inside that path.

| Directory        | Domain rules cover                    |
|------------------|---------------------------------------|
| `src/auth/`      | Auth flows, session handling, JWT     |
| `src/payments/`  | PCI scope, Stripe integration         |
| `src/[module]/`  | [describe module scope]               |

## MCP tools
See `.mcp.json` for server config. Ask before using a tool not listed here.

## Sensitive Data
See `.aiignore` for Files AI must never touch.

| Tool        | Allowed actions                        |
|-------------|----------------------------------------|
| [GitHub]    | Read issues/PRs · Create draft PRs    |
| [Postgres]  | SELECT queries only — no mutations    |
| [Jira]      | Read tickets · Update status          |

# Coding Conventions — [PROJECT_NAME]
# ── AI applies these automatically. Update here, effects everywhere. ─────────

## Language and runtime
- Language: [TypeScript 5.x — strict mode always on]
- Runtime: [Node.js 20 LTS]
- Target: [ES2022 / Node 20]

## Formatting (automated — do not argue with the formatter)
- Tool: [Prettier] · Config: `.prettierrc`
- On save: auto-format (if IDE supports) · On commit: pre-commit hook via Husky
- AI rule: never reformat files outside the scope of the current task

## Linting
- Tool: [ESLint] · Config: `eslint.config.js`
- Fix only lint errors you introduced — do not batch-fix unrelated lint across the codebase

## Naming
| Thing               | Convention         | Example                          |
|---------------------|--------------------|----------------------------------|
| Variables           | camelCase          | `userCount`, `isLoading`         |
| Functions           | camelCase          | `getUserById()`, `handleSubmit()`|
| Classes             | PascalCase         | `UserService`, `AuthController`  |
| React components    | PascalCase         | `UserCard`, `ProjectList`        |
| Types / Interfaces  | PascalCase         | `User`, `CreateProjectInput`     |
| Constants           | SCREAMING_SNAKE    | `MAX_RETRIES`, `BASE_URL`        |
| Files (components)  | PascalCase.tsx     | `UserCard.tsx`                   |
| Files (utils/hooks) | camelCase.ts       | `useAuth.ts`, `formatDate.ts`    |
| Env vars            | SCREAMING_SNAKE    | `DATABASE_URL`, `JWT_SECRET`     |
| DB tables           | snake_case plural  | `users`, `project_members`       |
| DB columns          | snake_case         | `created_at`, `user_id`          |

## File structure
```
src/
├── [module]/
│   ├── [module].controller.ts   ← HTTP handlers only, no business logic
│   ├── [module].service.ts      ← Business logic
│   ├── [module].repository.ts   ← DB queries
│   ├── [module].types.ts        ← Types and interfaces
│   ├── [module].schema.ts       ← Zod/Joi validation schemas
│   ├── [module].test.ts         ← Unit tests
│   └── AGENTS.md                ← Module-specific AI rules (if needed)
```

## Functions and classes
- Functions: single responsibility · max ~40 lines · extract if longer
- Parameters: max 3 positional — use object param for 4+ (`createUser({ name, email, role })`)
- Return types: always explicit in TypeScript
- Async: always `async/await` — never raw `.then()/.catch()` chains
- Error handling: throw typed errors — never return `null` to signal failure

## Types
- Avoid `any` — use `unknown` if type is truly unknown, then narrow
- Prefer `type` over `interface` for unions and computed types
- Prefer `interface` for objects that may be extended
- No non-null assertions (`!`) without a comment explaining why it's safe

## Testing
- Framework: [Vitest | Jest]
- Coverage target: [80%] minimum on business logic — not on controllers or config
- Test naming: `it('should [expected behaviour] when [condition]')`
- Structure: Arrange → Act → Assert — one assertion concept per test
- Mocking: mock at the module boundary — don't mock internals
- Test files: co-located at `[file].test.ts` — not in a separate top-level `/tests` folder
- E2E: [Playwright] in `/e2e` — run in CI only, not required locally for every PR

## Git workflow
- Branching: `[type]/[ticket]-[short-description]` e.g. `feat/AUTH-42-google-oauth`
- Commits: `type(scope): imperative description` · max 72 chars
  - Types: `feat` · `fix` · `refactor` · `test` · `chore` · `docs` · `perf` · `ci`
- PRs: one concern per PR · under 400 lines changed · link the ticket
- Merge strategy: [Squash merge to main | Merge commits]
- Protected branches: `main`, `staging` — no direct push

## Dependencies
- Adding a new package: note in your PR description and explain why
- Prefer: established, maintained libraries with ≥1M weekly downloads
- Avoid: multiple libraries solving the same problem
- Dev-only tools: `devDependencies` — never in `dependencies`

## Security
- Never log passwords, tokens, or PII
- Validate all external input with [Zod | Joi] before using
- Parameterised queries only — never string-interpolate SQL
- Rate limit all public endpoints
- CORS: explicitly allowlisted origins — never wildcard `*` in production

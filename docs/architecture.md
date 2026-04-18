# Architecture — [PROJECT_NAME]
# ── Keep this file current. Outdated architecture docs mislead the AI. ──────

## System overview
[2–3 sentences. What does this system do? Who uses it? What problem does it solve?]

## Component map
```
[CLIENT]              [BACKEND]              [DATA]
Next.js 14      →     Node.js API      →     PostgreSQL 15
(Vercel)              (Railway)              (Railway)
                            ↓
                       Redis 7 (cache)
                       (Railway)
```
Replace the diagram above with your actual system. Keep it ASCII — no external tools.

## Services and responsibilities
| Service / App    | Tech            | Responsibility                        | Port  |
|------------------|-----------------|---------------------------------------|-------|
| `web`            | Next.js 14      | User-facing frontend, SSR             | 3000  |
| `api`            | Express / NestJS| REST API, business logic              | 8000  |
| `worker`         | BullMQ          | Background jobs, email, webhooks      | —     |
| `[service]`      | [tech]          | [responsibility]                      | [port]|

## Data flow
[Describe the primary happy-path data flow in 4–6 steps]
1. User authenticates via [OAuth / JWT / session]
2. Frontend calls API at `/api/v1/[resource]`
3. API validates request → applies business logic
4. Writes to PostgreSQL via [Prisma / TypeORM / raw SQL]
5. Invalidates / updates Redis cache key `[key pattern]`
6. Returns response → frontend re-renders

## Key architectural decisions
Full ADRs in `docs/decisions/`. Summary:
| Decision                    | Choice made              | Reason                          |
|-----------------------------|--------------------------|---------------------------------|
| ORM                         | [Prisma]                 | [Type safety, migration tooling]|
| Auth strategy               | [JWT RS256]              | [Stateless, multi-service]      |
| Job queue                   | [BullMQ + Redis]         | [Reliability, retries, delay]   |
| [decision]                  | [choice]                 | [reason]                        |

## Module boundaries
| Module        | Owns                              | Must not                              |
|---------------|-----------------------------------|---------------------------------------|
| `auth`        | Session, tokens, user identity    | Access payment data directly          |
| `payments`    | Stripe, invoices, subscriptions   | Store card numbers (Stripe handles)   |
| `[module]`    | [what it owns]                    | [what it must not do]                 |

> Cross-module: go through the public API of the target module. Never import internals across module boundaries.

## Infrastructure
- **CI/CD**: [GitHub Actions → deploy on merge to main]
- **Secrets**: [environment variables via platform dashboard — never in code]
- **Logs**: [Datadog | Axiom | CloudWatch] — structured JSON
- **Monitoring**: [Sentry for errors · Uptime via BetterUptime]
- **CDN**: [Cloudflare | Vercel Edge]

## Scaling considerations
- [Stateless API — horizontal scaling is safe]
- [Session data in Redis — survives pod restarts]
- [DB connection pooling via [PgBouncer | Prisma accelerate]]
- [Known bottleneck: [describe if any]]

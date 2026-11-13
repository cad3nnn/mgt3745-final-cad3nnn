# Sourcing Audit

## Audit 1, November 2026

### Prediction Stake (commit before any evidence)

The audit will find that the project currently has zero direct npm packages and that the only production dependencies that ship to users are Cloudflare Workers and D1 (plus the static page). Resolution: Tight.

### Weights (commit in their own commit, before scoring)

| Criterion              | Weight | Why this weight for this project |
|------------------------|--------|----------------------------------|
| Stability              | 35     | The system must stay up for the rest of the semester and the final package; a platform outage kills demos and evals. |
| Pricing predictability | 25     | We are on the free tier with hard daily limits. Hitting a limit is worse than a small predictable bill. |
| Institutional fit      | 20     | The course and every prior homework used Cloudflare; switching platforms now would waste the remaining calendar time. |
| Exit cost              | 20     | We already know how to export D1 and the Worker is a single file; the hours estimate must stay honest. |
| **Total**              | **100**| |

### Inventory

| Dependency                  | Kind                          | Where it is recorded                  | Ships to users? |
|-----------------------------|-------------------------------|---------------------------------------|-----------------|
| Cloudflare Workers          | platform                      | worker/wrangler.toml, docs/DEPLOY.md, context/ARCHITECTURE.md | Yes |
| Cloudflare D1               | platform                      | worker/wrangler.toml, schema (planned), ARCHITECTURE.md | Yes (data) |
| wrangler (via npx)          | dev package / CLI             | docs/DEPLOY.md, package.json scripts  | No |
| GitHub Pages / GitHub       | platform                      | README, index.html                    | Yes (static) |
| Codespaces / GitHub         | platform                      | .devcontainer                         | No |
| Node.js (built-in test runner) | runtime                    | package.json scripts                  | No |
| bolt.new                    | builder                       | context/TOOLS.md (template)           | No |
| (future model, if any)      | model                         | —                                     | No |

**Total installed npm packages (direct + transitive):** 0  
(`package.json` declares none; `npm ls --all` is empty.)

### Evidence (each fact with its source and the date you read it)

| Dependency             | Latest version and date     | Maintainers or vendor | License or terms               | Limits or price                                                                 | Other notes                                                                 | Checked on  |
|------------------------|-----------------------------|-----------------------|--------------------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------|-------------|
| Cloudflare Workers     | Platform                    | Cloudflare            | Cloudflare ToS                 | Free: 100 k requests/day, 10 ms CPU. Paid from $5/mo. Static assets free.      | Stable course platform since HW4.                                           | 2026-11-12 |
| Cloudflare D1          | Platform                    | Cloudflare            | Same                           | Free: 5 M rows read/day, 100 k writes/day, 5 GB, 10 DBs.                        | Export via `wrangler d1 export`. Synthetic data only planned.               | 2026-11-12 |
| wrangler               | Latest via npx (unpinned)   | Cloudflare            | Apache-2.0 / MIT               | Free with account                                                               | Version not pinned; risk of flag changes.                                   | 2026-11-12 |
| GitHub Pages           | Platform                    | GitHub / Microsoft    | GitHub Terms                   | Free for public repos                                                           | Serves index.html from root.                                                | 2026-11-12 |
| Node.js test runner    | Built-in                    | Node.js               | MIT                            | N/A                                                                             | Only for evals.                                                             | 2026-11-12 |
| bolt.new               | SaaS                        | StackBlitz            | Their terms                    | Free + paid tiers                                                               | Template lists it; treat as builder only.                                   | 2026-11-12 |

Sources (all read 2026-11-12):  
- https://developers.cloudflare.com/workers/platform/pricing/  
- https://developers.cloudflare.com/workers/platform/limits/  
- https://developers.cloudflare.com/d1/platform/pricing/  
- Local: package.json, worker/wrangler.toml, docs/DEPLOY.md, context/TOOLS.md, docs/ADR-001.md

### Scores and Rings

| Dependency             | Stability | Pricing | Institutional fit | Exit cost | Weighted | Ring   | Reason in one line |
|------------------------|-----------|---------|-------------------|-----------|----------|--------|--------------------|
| Cloudflare Workers     | 5         | 4       | 5                 | 4         | 4.55     | Adopt  | Core platform, free tier sufficient, team experience high, export path exists. |
| Cloudflare D1          | 5         | 4       | 5                 | 4         | 4.55     | Adopt  | Same as Workers; data will be synthetic and exportable. |
| wrangler               | 4         | 5       | 5                 | 3         | 4.20     | Trial  | Essential but unpinned; pin it. |
| GitHub Pages           | 5         | 5       | 5                 | 4         | 4.80     | Adopt  | Course default for static front-end. |
| Node.js test runner    | 5         | 5       | 5                 | 5         | 5.00     | Adopt  | Built-in, zero risk. |
| bolt.new               | 3         | 3       | 3                 | 5         | 3.40     | Hold   | Builder only; do not ship its output without rewrite. |

Weighted example (Workers): (5×0.35)+(4×0.25)+(5×0.20)+(4×0.20) = 4.55

### Exit Plans (every critical dependency + every Trial)

| Dependency             | Trigger                                      | Substitute                              | Hours to swap | Tested? (date and how) |
|------------------------|----------------------------------------------|-----------------------------------------|---------------|------------------------|
| Cloudflare Workers + D1| Free-tier limit hit, pricing or policy change | Static + external SQLite (Turso) or self-hosted Node | 8–12     | Planned: `npx wrangler d1 export` once a database exists. |
| wrangler               | Breaking change or removal of free npx       | Pin exact version as devDependency      | 1–2           | Will test after pin. |
| bolt.new               | Terms or quality change                      | Manual implementation or another builder| 0 (process)   | N/A |

### Changes Caused by This Audit
- Will pin wrangler as a devDependency in a follow-up commit and update docs/DEPLOY.md to use the local binary.
- No other packages to remove (none exist).
- ADR-001 already records the stack; this audit points back to it.
- TOOLS.md will be updated to the required columns.
- DDR entry will be added for AI assistance used on this audit.

### Prediction Stake Resolution
The prediction held (Tight). The repository currently has zero direct npm packages. The only things that will ship to users under ADR-001 are the Cloudflare Worker, D1 data, and the static page.
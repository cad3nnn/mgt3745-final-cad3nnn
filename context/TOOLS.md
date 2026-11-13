# TOOLS.md

| Tool                  | Purpose                          | Ring  | Checked on  | Limit or price                                      | Exit |
|-----------------------|----------------------------------|-------|-------------|-----------------------------------------------------|------|
| Cloudflare Workers    | Runtime for API + static assets  | Adopt | 2026-11-12 | Free 100k req/day, 10 ms CPU                        | Export + rewrite Worker |
| Cloudflare D1         | Postings database                | Adopt | 2026-11-12 | Free 5M reads / 100k writes / day                   | `wrangler d1 export` |
| wrangler              | Deploy & D1 management           | Trial | 2026-11-12 | Free with account                                   | Pin version |
| GitHub Pages          | Static front-end                 | Adopt | 2026-11-12 | Free                                                | Move files |
| Node.js test runner   | Evals                            | Adopt | 2026-11-12 | Built-in                                            | None |
| bolt.new              | Builder (probes only)            | Hold  | 2026-11-12 | Free + paid                                         | Stop using |
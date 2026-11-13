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
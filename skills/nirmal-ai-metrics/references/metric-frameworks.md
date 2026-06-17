# Metric frameworks — choosing the tree

Frameworks are lenses, not templates. Pick the one that fits the product and build a single coherent tree. Don't stack all of them.

## North-star metric (default spine)
One metric that best proxies the value customers get. Properties of a good one:
- **Reflects value**, not activity. "Weekly active teams that shipped a project" beats "logins".
- **Leads revenue** — when it rises, revenue follows (eventually).
- **Movable** by the team's work.
- **Per-unit where possible** (per account/team), so it's not just a function of total signups.

Anti-patterns: raw signups, pageviews, total registered users — they go up even as the product fails.

## Input vs. output metrics
- **Output** = the north star and revenue. Lagging, hard to move directly.
- **Inputs** = the 3–5 levers you actually pull that drive the output. Leading, controllable.
Build the tree as: north star (output) ← inputs ← sub-inputs. Teams own inputs; leadership watches the output.

## AARRR (acquisition funnel lens) — good for growth-stage
Acquisition → Activation → Retention → Referral → Revenue. Use to make sure the tree's inputs span the whole funnel, not just the core feature. Most first drafts over-weight engagement and forget activation and retention.

## HEART (UX quality lens) — good for feature-level / Mode D
Happiness, Engagement, Adoption, Retention, Task success. Pair each with a Goal → Signal → Metric. Useful when measuring whether a *feature* is good, not whether the *business* is working.

## Guardrail metrics (always)
For every metric you push, name what could degrade as a side effect:
- Performance: p95 latency, error rate.
- Health: churn, NPS/CSAT, support ticket volume.
- Economics: cost per action, infra cost per active unit.
A north star without guardrails invites local optimization that breaks the product.

## Defining a metric (do this for every node)
State all four or it will be computed inconsistently:
1. **What** it counts (the precise event/outcome).
2. **Grain** — per user? per account? per session?
3. **Window** — daily / weekly / 28-day rolling / cohort.
4. **Direction** — is up good or bad?
Put the final definition in the `nirmal-ai-context` glossary so it can't fork between teams.

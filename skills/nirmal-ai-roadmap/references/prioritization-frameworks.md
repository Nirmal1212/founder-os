# Prioritization frameworks — which, when, how

Frameworks are for forcing honesty and comparability, not for outsourcing the decision. Score, then sanity-check against judgment.

## RICE (default for a mixed backlog)
`Score = (Reach × Impact × Confidence) ÷ Effort`
- **Reach**: how many users/events per time period (real numbers, not vibes).
- **Impact**: per-user effect on the goal — use a fixed scale (3 massive, 2 high, 1 medium, 0.5 low, 0.25 minimal).
- **Confidence**: % you believe your Reach/Impact estimates (100/80/50). This is the honesty valve — low confidence rightly sinks shiny bets.
- **Effort**: person-months (or points). The only denominator — small efforts with decent value rise.
Strength: exposes the guesses. Weakness: false precision if inputs are fabricated — show the inputs.

## Value vs. Effort (fast first cut)
Plot each item on value (to user/business) × effort. Do the high-value/low-effort quadrant first; question high-effort/low-value entirely. Good for small lists and quick alignment; too coarse for a large mixed backlog.

## WSJF (when timing matters)
`Cost of Delay ÷ Job Size`. Use when items have genuine time sensitivity (a market window, a dependency others wait on, a compliance deadline). Surfaces "do this now because waiting is expensive" that RICE misses.

## Kano (MVP must-haves vs. delighters)
Classify features as Basic (absence causes pain), Performance (more is better), or Delighter (unexpected upside). For an MVP, you must cover Basics; add one Delighter for differentiation; defer Performance tuning. Good specifically for *what makes the cut*.

## Cross-checks before trusting any score
- **Dependencies** override score — a blocker ships before the thing it unblocks.
- **Strategic fit** — a high-scoring item off-strategy is still a distraction.
- **Confidence floor** — a huge score built on 50% confidence is a bet; label it as one.
- **Gut check** — if the ranking feels wrong, an input is wrong. Find it; don't just override silently (override *with* a logged reason).

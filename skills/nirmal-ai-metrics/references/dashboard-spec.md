# Dashboards, funnels & retention — spec format

A dashboard isn't a pile of charts; each view answers one question for one audience. Spec each view before anyone builds it.

## Per-view spec
For every dashboard/view, state:
- **Question it answers** — one sentence ("Are new accounts reaching first value?").
- **Audience** — exec / PM / growth / on-call. Drives altitude and refresh rate.
- **Metrics shown** — from the tree, by ID/definition (no ad-hoc metrics).
- **Breakdowns** — by ICP segment, plan, cohort, channel. The blended number usually lies.
- **Time grain & window** — daily/weekly; trailing window.

## Activation funnel (spec this explicitly)
The steps from signup to first value. Most teams measure it wrong by guessing the "aha" moment.
- List the ordered steps as events (from the tracking plan), e.g. `signup_completed → workspace_created → first_project_created → project_shared`.
- Define the **activation point** — the step that best predicts retention (validate against retained cohorts, don't assume).
- Show **conversion between each step** and **time-to-activate**.
- Break down by acquisition source and segment — activation often differs sharply by channel.

## Retention curve (spec this explicitly)
The truest health signal; the one most often shown wrong.
- **Cohort** by signup period; plot the % still active at week/month N.
- Decide the **active definition** (the metric grain + window — pull from the glossary, don't invent here).
- Look for the **flattening** of the curve — a flat tail = product-market fit signal; a curve to zero = leaky product.
- Compare cohorts over time to see whether product changes improved retention.

## Counter-metrics on every dashboard
Place the relevant guardrail next to the metric being pushed (north star beside churn/latency/cost) so a win that's secretly a loss is visible immediately.

## Keep dashboards few
One exec view, one activation view, one retention view, one or two team-owned input views. More dashboards than that and none get watched.

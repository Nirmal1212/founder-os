# Event taxonomy — the engineering contract

The tracking plan is what engineering instruments from. Precision here is permanent: bad event design corrupts data that can't be retroactively fixed.

## Naming convention — pick one, never deviate
Recommended: **`object_action`**, snake_case, past tense.
- `workspace_created`, `project_shared`, `invite_accepted`, `subscription_upgraded`.
- Object first so events group naturally (`workspace_*` sit together).
- Past tense because an event records something that *happened*.
Avoid: spaces, inconsistent tense, UI-specific names (`blue_button_clicked` — describe the outcome, not the widget), and per-screen duplicates of the same action.

**Object names come from the `nirmal-ai-context` glossary.** An event on a `Workspace` (T-002) is `workspace_*`. This keeps events, schema tables, and PRD vocabulary identical.

## Identity model — decide before any events
- **Anonymous vs. identified**: assign an anonymous ID pre-signup; on signup, alias it to the user ID so the pre-signup funnel stitches to the account.
- **Grain**: most B2B products need both a **user ID** and an **account/group ID** on every event — many metrics are per-account, not per-user. Decide and apply globally.
- **Traits vs. events**: identity traits (plan, role, account size) are *state* set on the user/account; events are *actions*. Don't encode slowly-changing state as events.

## Event schema — specify each event fully
Each row of the tracking plan:
| Field | Meaning |
|-------|---------|
| Event name | `object_action`, from glossary objects |
| Trigger | the exact moment it fires (server-side on success, not on button press, unless intent is the point) |
| Properties | typed key list (see below) |
| Identity | which IDs attach (user, account) |
| Feeds metric | the metric(s) in the tree this event computes — if none, cut the event |
| Source | client / server / backend job |

### Property rules
- Each property: **name, type, example, required?**. Types are explicit (string/int/bool/timestamp/enum).
- Prefer **server-side** events for anything that must be accurate (billing, activation) — client events drop and can be spoofed.
- Don't overload one event with conditional properties for different cases; split into distinct events if the shape differs.
- Enumerate enum values up front (`plan: free | pro | enterprise`).

## Keep it lean
Every event is instrumentation, QA, storage, and analysis cost forever. The test: *which metric node does this event feed?* No answer → no event. A 25-event plan that's correct beats a 200-event plan nobody trusts.

## Activation events — get these right first
The events along the signup → first-value path are the highest-value ones in the whole plan (they define the activation funnel). Identify the "aha" action and instrument every step leading to it before anything else.

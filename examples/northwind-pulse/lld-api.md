# LLD — API and key flow
<!-- Produced by: lld. Read context v3 (glossary terms T-001..T-004, D-003). ILLUSTRATIVE SAMPLE. -->

## Endpoints (REST, JSON, bearer auth)
| Method | Path | Purpose | Notes |
|---|---|---|---|
| GET | /v1/accounts | List Accounts (T-001) ranked by Health Score | Cursor pagination, `?risk=true` filter |
| GET | /v1/accounts/{id}/health | Score history and top Signals (T-002, T-003) | Powers the "why" panel (PRD R4) |
| GET | /v1/alerts | List Risk Alerts (T-004) | Filter by status |
| POST | /v1/alerts/{id}/actions | Log an action taken on an alert | Idempotent via `Idempotency-Key` header |
| POST | /v1/integrations/{source}/connect | Start OAuth for hubspot, stripe or segment | |

## Example: log an action
```http
POST /v1/alerts/al_123/actions
Idempotency-Key: 7f1c...
{ "action_type": "called_customer", "note": "Booked QBR" }
→ 201 { "id": "act_9", "alert_id": "al_123", "minutes_since_alert": 212 }
```
Errors use `{ "error": { "code", "message" } }`. 409 if the alert is already closed; 404 if the alert belongs to another org.

## Sequence: daily scoring and alert
1. Scheduler enqueues a scoring job per org.
2. Worker loads Signals, computes Health Score, writes `health_scores`.
3. If score is under 40 or fell 15+ points in 7 days and no open alert exists, create a Risk Alert and enqueue delivery.
4. Delivery worker posts to Slack or email, retries with backoff, and emits `risk_alert_sent`.

## Cross-cutting
Idempotency on actions and on alert creation (unique on account_id + open status). Every write logs actor, org and timestamp to the audit table (C-001). Tenancy enforced by `org_id` on every query.

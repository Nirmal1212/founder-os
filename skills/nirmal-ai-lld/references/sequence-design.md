# Sequence / flow design

A sequence diagram proves the components actually compose to satisfy a use case — and forces you to confront the failure paths. Do this for the 2–3 riskiest flows, not every CRUD call.

## What to render
Use **Mermaid `sequenceDiagram`**. Participants = the components/actors from the LLD. Messages = calls between them, in order, with sync vs. async marked.

```
sequenceDiagram
  actor U as User
  participant API as API Gateway
  participant S as Order Service
  participant Q as Queue
  participant P as Payment Svc
  U->>API: POST /orders (idempotency-key)
  API->>S: createOrder(cmd)
  S->>P: authorize(amount)
  alt payment ok
    P-->>S: authorized
    S->>Q: emit order_created
    S-->>API: 201 Created
  else payment declined
    P-->>S: declined(reason)
    S-->>API: 402 + error code
  end
```

## Mark sync vs. async
- Solid arrow `->>` = request; dashed `-->>` = response.
- A call that enqueues and returns immediately (async) must be visually distinct from one that blocks on a reply. Confusing the two is a common design error — it changes latency and failure behavior.

## Always draw the failure branches
The happy path is the easy part. For each external call, show what happens on:
- **Timeout / downstream down** — fail fast, retry with backoff, or degrade?
- **Validation failure** — reject at the boundary with which error.
- **Partial failure** — step 3 of 5 fails after side effects in 1–2; how is consistency preserved (compensating action, outbox, saga)?
Use `alt`/`opt`/`par` blocks to show these explicitly.

## Consistency across steps
- When a flow writes in multiple places, decide the consistency model: transaction (same store), outbox + event (cross-service), or saga with compensation. Show it in the diagram.
- Idempotency keys carry through the flow so a retried request re-joins safely.

## Keep each diagram to one flow
One use case per diagram, ≤6 participants. If it sprawls, the flow is doing too much or the boundaries are wrong — split it.

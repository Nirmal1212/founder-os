# HLD template

Use this structure for the final High-Level Design. Adapt depth to the problem — a small service doesn't need every subsection, a platform does. Keep it skimmable: tables and tight prose, not walls of text.

```markdown
# HLD: [System / Feature name]

## 1. Overview & goals
- One-paragraph summary of what's being built and the problem it solves.
- Key non-functional targets (the NFRs that shaped the design): scale, latency, availability, consistency, security/compliance.
- Explicitly out of scope.

## 2. Architecture diagram
[Mermaid or boxes-and-arrows visual showing the major components and request flow — client → gateway → services → data stores → async/queue → external integrations.]

## 3. Major components
For each component: responsibility · key tech · interfaces (what it talks to).

| Component | Responsibility | Tech | Talks to |
|---|---|---|---|
| API Gateway | Routing, auth, rate limiting | ... | ... |
| [Service] | ... | ... | ... |
| ... | ... | ... | ... |

## 4. Data model (high level)
- Core entities and their relationships (a quick ER sketch or list).
- Which store holds what, and why (e.g. transactional data in Postgres, sessions/cache in Redis, blobs in object storage, search index in OpenSearch).

## 5. Key flows
Walk 2–3 critical use cases end-to-end across components:
- **[Flow A — e.g. main write path]**: step-by-step across components.
- **[Flow B — e.g. high-volume read path]**: where caching/replicas come in.
- **[Flow C — async/background]**: queue → worker → result.

## 6. Cross-cutting concerns
- **Scaling**: where caching, queues, read replicas, autoscaling, and partitioning/sharding sit. What graduates to the next tier and when.
- **Security & auth**: authn/authz model, tenant isolation, encryption, secrets.
- **Observability**: logging, metrics, tracing, alerting.
- **Resilience & failure modes**: what happens when DB/queue/dependency fails; retries, circuit breakers, idempotency, backpressure; RTO/RPO.

## 7. Tech stack
| Layer | Choice | Why (requirement) | Alternative |
|---|---|---|---|
| Language / framework | ... | ... | ... |
| Primary DB | ... | ... | ... |
| Cache | ... | ... | ... |
| Async / queue | ... | ... | ... |
| Search / other | ... | ... | ... |
| Infra / cloud | ... | ... | ... |

## 8. Risks, trade-offs & open questions
- Key bets and what could go wrong.
- Trade-offs made (what was given up and why).
- Decisions still open / assumptions to validate.
```

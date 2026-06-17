# Design-shaping question bank

Pull the questions that actually change *this* design. Group related ones. Don't ask all of these — ask the smallest set that de-risks the biggest decisions. State assumptions for anything the user leaves unanswered.

## Scale & load
- How many users (total / concurrent / daily active)? Expected requests per second at peak?
- How much data today, and growth rate? (rows, GB/TB, objects)
- Is traffic steady or spiky? Predictable spikes (business hours, sales events) or unpredictable bursts? → drives caching, queues, autoscaling.
- Read-heavy or write-heavy? Rough read:write ratio?

## Latency & consistency
- Latency targets for the critical paths (p50 / p99)? Is this user-facing-interactive or background?
- Is eventual consistency acceptable, or do you need strong/transactional consistency anywhere (payments, inventory, balances)?
- Any real-time / streaming / push requirements (live updates, websockets)?

## Availability & durability
- Target uptime SLA (99.9%? 99.99%)? Cost of downtime?
- Tolerance for data loss (RPO) and recovery time (RTO)?
- Multi-region / geo-distribution needed? Disaster recovery requirements?

## Data shape & access patterns
- Is the data primarily relational, document, key-value, time-series, or graph?
- Structured, semi-structured, or unstructured (blobs, files, media)?
- Search needs — full-text, faceted, fuzzy, vector/semantic?
- Hot vs. cold data — does old data need archiving / tiering?

## Security & compliance
- Any regulated data (PII, PHI/HIPAA, PCI, financial)? Data-residency constraints (GDPR, India DPDP, region pinning)?
- Auth/authz model — who are the actors, SSO/OAuth/OIDC, RBAC/ABAC, multi-tenancy isolation?
- Audit logging / encryption-at-rest / secrets-management requirements?

## Integrations & async
- Third-party systems to integrate (payment, email, CRM, identity, internal services)?
- Webhooks / event-driven flows? Background jobs (reports, batch, ETL)?
- Idempotency / exactly-once needs on any flow?

## AI / ML (if applicable)
- LLM / RAG / agentic workflows? Which models, hosted or self-managed?
- Vector search / embeddings store needed? Volume of documents?
- Inference latency and cost budget? Streaming responses? Guardrails / eval needs?

## Team, ops & constraints
- Existing stack and team skills — any "we're a ___ shop" constraint?
- Preferred / mandated cloud (AWS / GCP / Azure / on-prem)? Managed services vs. self-host preference?
- Budget ceiling and timeline? MVP-now vs. build-for-scale?
- Build-vs-buy appetite for components (search, auth, queue, observability)?

## Multi-tenancy (for SaaS)
- Single-tenant, pooled multi-tenant, or hybrid? Per-tenant isolation / data-segregation requirements?
- Noisy-neighbor concerns? Per-tenant scaling or limits?

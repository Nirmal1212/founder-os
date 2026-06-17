# LLD — <Component name>

> Consumes: HLD (<link>). Persistence handed to nirmal-ai-data-model. Reads/writes nirmal-ai-context.

## 1. Responsibility
<the single responsibility of this component, in one or two sentences>

## 2. Public interface
```
<typed method signatures the component exposes>
```

## 3. Dependencies
| Depends on | Via interface | Direction note |
|------------|---------------|----------------|
| | | domain must not depend on transport/DB |

## 4. API contracts
<link to api-contract-template.md content, or inline the endpoint table>

## 5. Key flows
<Mermaid sequenceDiagram(s) for the 1–3 riskiest use cases, incl. failure branches>

## 6. Cross-cutting (component level)
- **Validation:** <boundary rules>
- **Errors:** <typed errors, what propagates vs. handled, retry-ability>
- **Idempotency:** <key source, window>
- **Concurrency:** <locking / optimistic version strategy>
- **Timeouts & retries:** <values, backoff>
- **Observability:** <tracking-plan events fired here, key logs/traces>

## 7. Persistence handoff
- Entities used: <glossary T-### IDs>
- Access patterns: <reads/writes this component needs — input to nirmal-ai-data-model>

## 8. Open questions / decisions to log
- <items to write back to nirmal-ai-context>

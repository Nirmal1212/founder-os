# API / interface design — the contract

The contract is the boundary other code is written against. Imprecision here costs everyone downstream. Specify enough that a client can be built without asking you a question.

## Per-operation spec
- **Identity**: method + path (REST) or method name (RPC); one-line purpose.
- **Request**: each param/body field — name, type, required?, validation rule, example.
- **Response (success)**: shape + status code; what's returned vs. referenced by ID.
- **Errors (the catalog)**: every failure — stable error code, HTTP status, trigger condition, message contract. This is the most-skipped and most-needed part.
- **Semantics**: auth + authz, idempotency, pagination, rate limits, versioning.

## Conventions (pick and apply consistently)
- **Resource naming**: nouns, plural collections (`/workspaces/{id}/projects`); from the glossary, so the URL vocabulary matches the domain.
- **Status codes**: 2xx success, 4xx caller's fault (with a typed error body), 5xx server's fault. Don't return 200 with an error inside.
- **Error body**: stable machine-readable `code` + human `message` + optional `details`. Clients branch on `code`, never on message text.

## Idempotency (writes)
- Any create/charge/side-effecting write needs an **idempotency key** so a retry doesn't double-apply. Define where the key comes from (client-supplied UUID) and how long it's honored.
- GET/PUT/DELETE are naturally idempotent; POST usually is not — that's the dangerous one.

## Versioning & compatibility
- Choose a strategy up front (URI `/v1`, header, or additive-only evolution).
- Evolve **additively**: new optional fields don't break clients; removing/retyping fields does. Never change a field's meaning in place.

## Pagination & filtering
- Prefer **cursor** pagination for large/changing sets (stable under inserts); offset is fine for small static lists. Specify page size limits.

## Concurrency on the wire
- For update races, support optimistic concurrency (ETag / `version` field, reject on mismatch) rather than last-write-wins when correctness matters.

## Boundary validation
- Validate at the edge, reject early with a precise 4xx. Never trust the caller; never let an invalid request reach the domain logic.

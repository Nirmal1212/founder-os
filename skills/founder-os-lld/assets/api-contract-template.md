# API contract — <Component / Service name>

## <METHOD> /path  — <one-line purpose>

**Auth:** <required scope/role> · **Idempotent:** <yes/no — key source if yes> · **Version:** v1

### Request
| Field | In | Type | Required | Validation | Example |
|-------|----|------|----------|-----------|---------|
| | body/query/path | | yes/no | | |

### Success response — `<2xx>`
```json
{ }
```

### Errors
| Code | HTTP | Fires when | Message contract |
|------|------|-----------|------------------|
| `invalid_request` | 400 | | |
| `not_authorized` | 403 | | |
| `conflict` | 409 | | |
| `rate_limited` | 429 | | |

### Notes
- Pagination: <cursor/offset, page size>
- Concurrency: <ETag / version field behavior>
- Entities referenced: <glossary IDs — T-###>

---
*(repeat per operation)*

# Physical design — types, keys, indexes, constraints

The physical model is where the logical model meets the engine and the query load. Decisions here determine performance and the cost of bad data.

## Types — avoid the classic foot-guns
- **Money**: integer minor units (cents) or fixed `DECIMAL`. **Never float** — rounding errors are unacceptable in financial data.
- **Timestamps**: store UTC, timezone-aware (`timestamptz`). Decide created/updated columns as a convention.
- **Bounded sets**: enum or `CHECK` constraint, not free-text strings — keeps data clean and self-documenting.
- **Identifiers**: see keys below.
- **Nullable** only when null has a real meaning ("unknown"/"not yet"). Don't use null as a lazy default; prefer NOT NULL + sensible default.

## Keys
- **Primary key**: UUID vs. auto-increment sequence — a real trade-off:
  - *Sequence/bigserial*: compact, great index locality, but reveals counts and is awkward across shards.
  - *UUID (v7 preferred)*: globally unique, shard- and merge-friendly, no enumeration leak; v7 keeps time-ordering so index locality stays decent (random v4 fragments indexes).
- **Foreign keys**: declare them, and choose `ON DELETE` behavior deliberately (restrict / cascade / set null) — it encodes a domain rule.

## Indexes — from the query patterns, nothing speculative
- Every index must serve a **stated access pattern** from the LLD. Write down which query each index is for.
- **Composite column order** matters: most-selective / equality columns first, range columns last. An index on `(account_id, created_at)` serves "this account's recent rows"; reversed, it doesn't.
- **Cover hot reads**: include selected columns so the index answers the query without a heap fetch, where it pays off.
- **Costs**: every index slows writes and uses space. The failure modes are *both* a missing index on a hot path and a pile of unused speculative ones.
- **Uniqueness**: enforce real-world uniqueness (email per account) with a UNIQUE index — it's a constraint *and* an index.

## Constraints — make invalid states impossible
- `NOT NULL`, `UNIQUE`, `CHECK`, `FOREIGN KEY` — push every invariant you can into the schema. The app forgets to validate; the database doesn't. This is the last line of defense for correctness.

## Scale (only if the table is large/hot)
- **Partitioning**: by time (range) for append-heavy logs/events; by tenant (hash/list) for multi-tenant isolation. Pick a key that spreads load — beware hot partitions (e.g. partitioning by "today").
- **Sharding**: only when a single node genuinely can't hold the load; the shard key choice is hard to reverse — tie it to the dominant access pattern.

## PII / compliance
- Flag columns holding personal/sensitive data (per context constraints). Note encryption-at-rest needs, field-level encryption for secrets, and retention/erasure requirements (e.g. GDPR delete).

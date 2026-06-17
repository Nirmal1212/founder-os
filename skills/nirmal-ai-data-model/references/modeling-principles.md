# Logical modeling principles

The logical model is about *correctness and meaning* — independent of any specific engine. Get it right before touching types and indexes.

## Entities, attributes, relationships
- **Entities** are the nouns — 1:1 with the glossary (same name, same T-### ID). If you're inventing an entity not in the glossary, add it back to the glossary.
- **Attributes** describe one entity; if an "attribute" has its own attributes or repeats, it's really its own entity.
- **Relationships** carry **cardinality** (1:1, 1:N, M:N) and **modality** (mandatory vs. optional). State both — "an order must belong to exactly one account; an account has zero or more orders".
- **M:N** always resolves to a **join entity** (e.g. `membership` between `user` and `workspace`), which often gains its own attributes (role, joined_at).

## Normalization — default to 3NF
- **1NF**: atomic values, no repeating groups.
- **2NF**: non-key attributes depend on the *whole* key.
- **3NF**: non-key attributes depend on *nothing but* the key. No transitive dependencies.
3NF is the default because it removes update anomalies — one fact lives in one place. Most OLTP schemas should be here.

## Denormalize only on purpose
Redundancy is a deliberate trade, never an accident:
- Justify it with a **named read pattern** (a hot query that can't afford the join).
- Document the **consistency cost** — now the same fact lives in two places and must be kept in sync (triggers, app logic, or accepted staleness).
- Prefer other tools first: a covering index, a materialized view, or a read replica often beats hand-denormalized tables.

## Relational vs. non-relational (if the HLD left it open)
- **Relational** when data is interconnected, transactional, and queried many ways — the default.
- **Document** when data is hierarchical, read as a unit, and access patterns are few and known.
- **Key-value** for simple lookups at extreme scale.
- **Wide-column / time-series / graph** for their specific shapes (huge writes, metrics over time, relationship traversal).
For non-relational, **model around the access pattern** — you design the shape for the queries, because you can't join your way out later.

## Soft vs. hard delete, audit
- Decide deletion semantics early (hard delete vs. `deleted_at` soft delete) — it ripples through every query and FK.
- If the domain needs history (who changed what, when), model it now (audit table / event log), not as an afterthought.

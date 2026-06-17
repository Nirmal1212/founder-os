# Migrations & schema evolution

Schemas live for years and change on running systems. The job is to change them without downtime, data loss, or breaking the currently-deployed app.

## Core rules
- **Versioned and ordered**: every change is a numbered, forward-only migration in source control. The schema's state is the sum of applied migrations.
- **Never edit a shipped migration**: once it's run anywhere, it's immutable. Fix-forward with a new migration.
- **Each migration is small and reversible-in-intent**: prefer changes you can roll back or fix forward quickly.

## Expand → migrate → contract (for breaking changes)
The pattern that keeps deploys zero-downtime, because old and new app versions run simultaneously during a rollout:
1. **Expand** — add the new structure (new nullable column / new table) without removing the old. Old code ignores it; new code can use it.
2. **Migrate** — backfill data into the new structure; start dual-writing (write both old and new) so they stay consistent.
3. **Contract** — once all app instances use the new structure and the backfill is verified, remove the old column/table in a later migration.
Rename = add new + backfill + switch + drop old. A direct rename breaks the app mid-deploy.

## Locking hazards (large tables)
- Adding an index can lock writes — use the engine's concurrent/online index build (`CREATE INDEX CONCURRENTLY`).
- Adding a `NOT NULL` column with a default, or changing a type, can rewrite the whole table and lock it — add nullable first, backfill in batches, then add the constraint.
- Always reason about table size and lock duration *before* running a migration in production.

## Backfills
- Backfill large data in **batches** (bounded by key range), not one giant transaction that locks rows and bloats the log.
- Make backfills **idempotent and resumable** — they will get interrupted.

## Safety net
- State a **rollback or fix-forward plan** per risky migration.
- Test migrations against production-like data volume — a migration that's instant on 1k rows can lock for minutes on 100M.
- Keep migrations decoupled from app deploys where possible (deploy schema first, compatible with both old and new code).

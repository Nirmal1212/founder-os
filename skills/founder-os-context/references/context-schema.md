# Context document — schema

The source of truth is one `context.md` (a single file keeps reads atomic). Sections below. Keep each section tight — this is infrastructure other skills consume, not a wiki.

## 1. Header
- `version`: integer, bump on every write-back.
- `last_updated`: date.
- `product`: name + one-line description.

## 2. Vision & thesis
- **Vision** (one sentence): the change the product makes in the world.
- **Problem**: the user problem, stated as the user would feel it.
- **Why now**: the wedge / unlock that makes this timely.
- **Non-goals**: what this product explicitly will *not* do. Prevents scope creep across skills.

## 3. ICP & personas
- **Primary ICP**: who you're building for first (firmographic + behavioral).
- **Personas**: 1–3, each with role, core job-to-be-done, and the pain that drives adoption.
- Keep this to the personas that actually shape decisions — not a demographic survey.

## 4. Glossary (canonical terms)
The most important section. Every domain noun other skills will reuse, defined exactly once.

| ID | Term | Canonical definition | Aliases / prior names |
|----|------|----------------------|------------------------|
| `T-001` | Account | A billing entity that owns one or more workspaces | Org (deprecated) |
| `T-002` | Workspace | A collaboration boundary within an account | — |

Rules: one definition per term; entities here map 1:1 to PRD entities, schema tables, and tracking-plan objects. Stable `T-###` IDs. See `protocols.md`.

## 5. Decisions log (append-only)
Lightweight ADR. Never edit a past entry; supersede with a new one.

| ID | Date | Decision | Rationale | Supersedes |
|----|------|----------|-----------|------------|
| `D-001` | 2026-01-10 | Target SMB before enterprise | Faster sales cycle, fewer compliance blockers | — |
| `D-002` | 2026-02-02 | Primary DB = PostgreSQL | Relational core data, strong consistency for billing | — |

Capture product *and* technical decisions here — this is the shared record both PM and Eng read.

## 6. Constraints
Hard boundaries every skill must design within:
- **Tech lock-ins**: cloud provider, mandated stack, existing systems to integrate.
- **Compliance**: PII/PHI/PCI, data residency, audit requirements.
- **Resource**: team size/skills, budget, timeline.

## 7. Interfaces (pointers, not copies)
Where the live artifacts are — referenced so context never holds a stale duplicate.
- `prd`: path/link + version
- `hld`: path/link + version
- `roadmap`: path/link + version
- `tracking_plan`: path/link + version
- `design_system`: path/link + version

# Protocols — read/write, IDs, conflicts

The rules that make the shared context reliable. Every other nirmal-ai-* skill is expected to honor the read-then-write protocol.

## Read-then-write protocol
Every skill that touches the project should:
1. **Read context first** (Mode B brief) before generating — so it inherits vision, ICP, glossary, constraints, and prior decisions instead of re-deriving them.
2. **Write context last** (Mode C) after finalizing — push new entities, terms, and decisions back so the next skill inherits them.

Bake this into each downstream SKILL.md as the first and last step. The architecture only holds if it's habitual.

## ID conventions
Stable IDs decouple references from names, so a rename propagates instead of forking.
- Glossary terms: `T-###`
- Decisions: `D-###`
- Personas: `P-###`
- Constraints: `C-###`

IDs are never reused or renumbered. Deleting a term means marking it deprecated (keep the ID), not removing the row.

## Glossary write rules
- **New term** → new `T-###` + one-line canonical definition.
- **Rename** → keep the existing `T-###`, update the term name and definition, move the old name into *Aliases*. Do **not** create a new ID — that forks the concept and reintroduces drift.
- **Same concept, two names spotted in artifacts** → merge under one ID, list the other as an alias, and append a decision noting the merge.
- One definition per term. If two definitions are in tension, that's a conflict (below), not two glossary rows.

## Decisions log write rules
- **Append-only.** Never edit or delete a past entry.
- **Supersede, don't overwrite.** A reversed decision gets a *new* `D-###` whose `Supersedes` field names the old ID. The old entry stays, preserving the "why".
- Every entry needs a real rationale tied to a requirement or constraint. "We chose X" without a why is not a decision worth logging.

## Conflict handling (Mode D)
When two artifacts or sections disagree, **surface — never silently resolve**. Report each conflict as:
- **What**: the two statements that disagree.
- **Where**: which artifacts/sections (by ID/pointer).
- **Recommended resolution**: the senior call, with a one-line reason.
- **Decision needed**: the user picks; the choice is then recorded as a new `D-###`.

Common drift patterns to scan for:
- Glossary term used with a different meaning in the PRD or HLD.
- Architecture/stack choice contradicting a `C-###` constraint.
- PRD requirement with no backing decision, or a decision with no requirement.
- Tracking-plan event referencing an entity absent from the glossary.

## Versioning
- Bump `version` on every write-back; update `last_updated`.
- When a skill reads context, it records the version it read against, so a later reconcile can tell whether it was working from current facts.

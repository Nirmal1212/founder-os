---
name: founder-os-context
description: Maintain the single source-of-truth context document that every other founder-os-* skill reads before it acts and writes back to after. It holds the product vision, ICP/personas, a canonical glossary, an append-only decisions log, hard constraints, and pointers to the live PRD/HLD/roadmap. Use this skill whenever the user wants to set up, read, update, or reconcile shared project context — phrases like "set up the source of truth", "what's our context", "add this decision", "update the glossary", "is the PRD consistent with the architecture", "why did we choose X", "load context before we start", or whenever a downstream skill needs a consistent brief. Also use it as the first step when kicking off a new product so vision, ICP, and terms are defined once and reused everywhere.
---

# founder-os-context (Source-of-Truth Steward)

**Depends on:** none · **Feeds:** all other skills

Operate as the keeper of the project's shared memory. Your job is not to design the product or the system — it's to make sure every other skill (`founder-os-pm`, `founder-os-architect`, `founder-os-lld`, `founder-os-metrics`, the GTM skills) is working from the *same* facts: the same vision, the same ICP, the same definition of every domain term, and the same record of decisions and why they were made. Drift between a PRD and an HLD almost always traces back to two skills quietly assuming different things. This skill stops that at write-time instead of integration-time.

This skill is **foundational**: it sits under all the others. The intended discipline is *read context first, write context last*. When kicking off a new product, run this skill before `founder-os-pm`. Whenever another skill makes a decision or introduces an entity, that decision/entity comes back here.

## Step 1 — Detect the mode

Read the conversation and figure out which of four modes the user is in. They flow naturally (init → read → update → reconcile) but the user can enter at any point.

- **Mode A — Init**: no context document exists yet, or the user wants to bootstrap one. Build it from whatever exists (a product idea, an approved use-case set, a PRD, an HLD) or from a short interview. Signals: "set up the context", "create the source of truth", "we're starting a new product".
- **Mode B — Read / brief**: another skill (or the user) needs a consistent briefing before acting. Load the relevant sections and produce a tight brief — vision + ICP + glossary + constraints + the live pointers. Signals: "load context", "brief me", "what do we know so far", a downstream skill about to start.
- **Mode C — Update / write-back**: a skill or the user produced new facts — a new entity, a renamed term, a scope cut, a stack choice. Record them in the right section following the protocols. Signals: "add this decision", "we renamed X to Y", "the PRD is final, update context", "we picked Postgres".
- **Mode D — Reconcile / audit**: check the context (and the artifacts it points to) for conflicts and drift, and surface them. Signals: "is everything consistent", "does the HLD still match the PRD", "audit our context".

Read `references/context-schema.md` for what each section holds, and `references/protocols.md` for the read-then-write rules, ID conventions, and conflict handling.

## Step 2 — Init: build the context document (Mode A)

Create the document from `assets/context-template.md`. Fill what's known; for what's missing, ask the **smallest set of questions that unblock the other skills** — vision in one sentence, the primary ICP, the top 3–5 domain terms, and the hard constraints (stack lock-ins, compliance, budget, timeline). Don't try to fill every field upfront; the document is meant to grow as skills run.

Seed the **glossary** with canonical definitions for the core domain nouns, each with a stable ID (see protocols). Seed the **decisions log** with any decisions already made (e.g. "chose to target SMB first"). Set the **interfaces** section to point at the current PRD/HLD/roadmap/tracking-plan locations (references, not copies).

## Step 3 — Read: produce a consistent brief (Mode B)

Pull only the sections relevant to the requesting skill and emit a compact brief, not the whole document:
- For `founder-os-pm`: vision, ICP/personas, glossary, non-goals.
- For `founder-os-architect` / `founder-os-lld`: constraints, NFR-relevant decisions, glossary (entities → these become components/tables), interfaces.
- For `founder-os-metrics`: vision (→ north star), ICP, the activation/retention decisions, glossary.
- For GTM skills: vision, ICP, positioning decisions, non-goals.

The point of the brief is that two skills reading it independently get **identical** facts. Keep term definitions verbatim from the glossary — don't paraphrase a definition into a new one.

## Step 4 — Update: write back (Mode C)

Apply changes following `references/protocols.md`:
- **New entity / term** → add to the glossary with a new stable ID and a one-line canonical definition. If it's a rename, update the definition under the *existing* ID and note the prior name as an alias — don't fork a new term.
- **New decision** → append to the decisions log (never overwrite). Each entry: ID, date, the decision, the rationale, and what it supersedes (if anything). Superseding is an append, not an edit.
- **Constraint change** → update the constraints section and append a decision explaining the change.
- **Artifact finalized** → update the interfaces pointer and version note.

Confirm back to the user in one line what was written and where.

## Step 5 — Reconcile: surface conflicts (Mode D)

Scan for the common drift patterns and **flag rather than silently resolve**:
- A glossary term used with a different meaning in a linked PRD/HLD.
- An architecture choice that contradicts a stated constraint (e.g. constraint says serverless-only, HLD picks a stateful cluster).
- A PRD requirement with no corresponding decision, or a decision with no requirement behind it.
- A metric in the tracking plan that references an entity not in the glossary.

Present conflicts as a short list with the two sides and a recommended resolution, then let the user decide. Once decided, record the resolution via Step 4.

## Delivery format

- The context document is the **authoritative artifact**: a single `context.md` (or the small file set in the template), kept in the repo and versioned. Deliver/update it as a file, not as a chat dump.
- **Briefs (Mode B)** are delivered inline in chat — tight and skimmable, only the requested sections.
- **Conflict reports (Mode D)** are delivered inline as a short list.
- Always end an update by stating the new document version / what changed, so downstream skills know the context moved.

## Quality bar — what makes this senior rather than junior

- **One definition per term, everywhere.** The whole value is that "account", "tenant", "user" mean exactly one thing across PRD, schema, and tracking plan. Guard the glossary jealously.
- **Append-only history.** Never delete rationale. A superseded decision still teaches *why* the current one exists. Traceability is the asset.
- **Stable IDs over names.** Names change; IDs don't. Reference entities and decisions by ID so a rename propagates instead of forking.
- **Surface, don't paper over.** When two artifacts disagree, the failure mode is silently picking one. Name the conflict and make the user decide.
- **Stay minimal.** This document is infrastructure, not a wiki. Capture only what other skills actually consume; resist the urge to document everything.
- **Read first, write last.** Reinforce the protocol with every other skill — the architecture only works if it's habitual.

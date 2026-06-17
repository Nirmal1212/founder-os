# Mode A — Brainstorming Use Cases

Goal: turn a product idea or domain into a sharp, prioritized set of personas and use cases, captured in a **structured CSV register** that can be reviewed, re-prioritized, and tracked over time. This is where most of the product thinking happens — don't rush to a feature list.

## Process

1. **Lock the thesis first.** In one or two lines: what problem, for whom, why now. If the user gave a feature list but no problem, infer the implied problem and state it back so it can be corrected.
2. **Enumerate personas.** Go beyond the obvious primary user: primary users, secondary users, internal/admin/operator personas, and edge personas worth designing for (power users, first-time users, at-risk users).
3. **For each persona, derive jobs-to-be-done, then use cases.** A use case is something the persona is trying to accomplish, not a UI feature. "Track my progress over time" is a use case; "a line chart on the dashboard" is an implementation.
4. **Cover the lifecycle.** Deliberately check each stage and add use cases the user missed — this maps to the `Lifecycle Stage` column below.
5. **Prioritize.** Tag each use case P0 / P1 / P2 and mark whether it's in the MVP. Be willing to push back: if the idea has 20 P0s, it has no P0s.
6. **Pressure-test.** Capture what's missing, risky, or unvalidated as `Open Questions / Notes` on the relevant rows, and call out the big ones in the inline summary.

## Canonical output: the use-case register (CSV)

The deliverable is a **CSV file** using this exact template. A blank header lives at `assets/use-case-template.csv` — copy it and populate it. Write the CSV with Python's `csv` module (or pandas) so commas inside descriptions are quoted correctly; never hand-concatenate strings. Save to the outputs directory and present the file.

**Columns (in this order):**

| Column | Meaning | Allowed values |
|--------|---------|----------------|
| `ID` | Stable identifier | `UC-001`, `UC-002`, … (sequential; never renumber once assigned) |
| `Persona` | Who the use case serves | one persona name |
| `Use Case` | Short capability/job title | concise noun phrase |
| `Description` | One-line detail of what the persona accomplishes | free text |
| `Lifecycle Stage` | Where it sits in the funnel | `Acquisition`, `Activation`, `Core loop`, `Retention`, `Referral / Virality`, `Monetization`, `Admin`, `Compliance` (combine with `/` if it spans two) |
| `Priority` | Scope priority | `P0`, `P1`, `P2` |
| `MVP` | In the first shippable cut | `Yes`, `No` |
| `Rationale` | Why it matters / why this priority | free text |
| `Dependencies` | What it relies on | free text (`;`-separated) |
| `Status` | Review/lifecycle state | `Proposed`, `Agreed`, `In PRD`, `Built` |
| `Open Questions / Notes` | Unresolved decisions attached to the row | free text |

**Status convention:** default new use cases to `Proposed`. Mark a row `Agreed` only for use cases the user has explicitly aligned on; as work proceeds they move `Agreed → In PRD → Built`. This is what makes the register useful for *later* review.

**MVP rule:** `MVP = Yes` should be a small set — the core loop plus the one or two mechanics that test the product's central bet. If most rows are `Yes`, the cut hasn't been made.

## What to deliver in chat alongside the file

Don't dump the whole table into chat. Instead:
1. A short **PM read** of the draft — what's strong, what's missing, what's mis-scoped (when the user supplied their own list).
2. A one-line **summary**: total use cases, how many are MVP, and any glaring lifecycle gap.
3. The **CSV file** itself (the authoritative register).
4. The big **open questions/risks** worth resolving before the PRD.

## Reacting to a user-supplied list

When the user pastes their own personas/use cases (common), don't just transcribe into the CSV. Give the PM read first, then populate the register with the improved, prioritized set. Typical gaps to look for: no activation/onboarding use case, no retention loop, no monetization path, admin/moderation underspecified, no empty/error states, no abuse or safety consideration, accessibility ignored, and (for products handling minors or regulated data) no consent/compliance use case.

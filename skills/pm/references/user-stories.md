# Mode C — Writing User Stories

Goal: decompose a PRD or feature set into multiple, well-formed user stories an engineering team can pick up, each with clear acceptance criteria, grouped into epics, prioritized, and roughly sized.

## Process

1. **Group into epics.** Cluster the PRD's functional requirements into a handful of epics (themes of work). Stories live under epics.
2. **Write one story per discrete piece of user-facing value.** Don't write one giant story per feature; split until each is independently testable and small enough to build in a sprint.
3. **Add acceptance criteria** to every story — the conditions that make it "done". Use Given/When/Then for flows, or a checklist for simpler cases.
4. **Prioritize and size.** Tag P0/P1/P2 (trace to the PRD's priorities) and give a rough size (S/M/L or points). Sizing is an estimate, flagged as such.
5. **Cover the unhappy paths.** Include stories (or criteria) for empty states, errors, permissions, and edge cases — these are where backlogs silently fail.
6. **Keep traceability.** Where useful, reference the PRD requirement ID each story implements so nothing is dropped and nothing extra sneaks in.

## Story format

Use the standard form, with acceptance criteria attached:

```markdown
### Epic: [Epic name]

**[STORY-ID] [Short title]**  — Priority: P0 · Size: M
As a [persona], I want [capability], so that [benefit].

Acceptance criteria:
- Given [context], when [action], then [outcome].
- [Edge case / error condition handled]
- [Empty/first-time state defined]

Traces to: FR-x
```

## INVEST check

Before finalizing, sanity-check each story against INVEST — it catches the common failure modes:
- **Independent** — minimal dependence on other stories
- **Negotiable** — describes the what, leaves room on the how
- **Valuable** — delivers value to a persona (not "set up the database" with no user-facing value)
- **Estimable** — the team could size it
- **Small** — fits in a sprint; split if not
- **Testable** — the acceptance criteria make "done" unambiguous

If a story fails one of these (e.g. too big, or pure tech-debt with no user value), reshape or split it and say why.

## Output

Deliver inline in chat as markdown, grouped by epic and ordered by priority. Lead with a one-line summary of how many epics/stories and the suggested MVP cut (which stories are P0).

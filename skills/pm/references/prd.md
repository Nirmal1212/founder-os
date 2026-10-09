# Mode B — Writing the PRD

Goal: turn agreed use cases into a structured, skimmable PRD that an eng + design team could build from and a stakeholder could approve. Opinionated and prioritized, not a feature dump.

## Before writing

Confirm (from context, don't interrogate) that the use cases are roughly settled. If they're not, you're still in Mode A — go back. If a critical input is genuinely missing (target platform, rough timeline, the one metric that defines success), ask one tight question rather than guessing on something load-bearing.

## PRD template

Use this structure. Drop sections that truly don't apply, but don't silently skip Goals/Non-goals, Success metrics, Requirements, or Risks — those are the spine.

```markdown
# [Product/Feature name] — PRD

## 1. TL;DR
[3-4 sentences: what we're building, for whom, and the outcome we expect. A reader should be able to stop here and get the gist.]

## 2. Problem & context
[The user problem, evidence it's real, and why now. What happens if we don't build this.]

## 3. Goals & non-goals
**Goals**
- [Outcome-oriented, not feature-oriented]

**Non-goals** (explicitly out of scope for this release)
- [What we are deliberately not doing, and why]

## 4. Success metrics
| Metric | Type | Target | How measured |
|--------|------|--------|--------------|
| [North star] | Primary | ... | ... |
| ... | Supporting | ... | ... |

## 5. Personas
[Brief — pull from the use-case work. Who, and their core job.]

## 6. User journeys / use cases in scope
[The key flows this release supports, in priority order. Reference the use cases agreed earlier.]

## 7. Functional requirements
[Grouped by feature area. Each requirement prioritized and testable.]
### [Feature area]
| ID | Requirement | Priority | Notes |
|----|-------------|----------|-------|
| FR-1 | The system shall... | P0 | ... |

## 8. Non-functional requirements
[Performance, scale, security, privacy/compliance, accessibility, reliability, localization. Only what's relevant — but check each.]

## 9. UX & design principles
[Design direction and any hard UX constraints. Reference comparable products if useful.]

## 10. Dependencies & assumptions
[External systems, teams, data, third parties; assumptions the plan rests on.]

## 11. Risks & mitigations
| Risk | Likelihood/Impact | Mitigation |
|------|-------------------|------------|

## 12. Release plan / phasing
[MVP scope vs fast-follow vs later. Map to the P0/P1/P2 from requirements.]

## 13. Open questions
[Unresolved decisions, with an owner or a "needs decision by" where possible.]
```

## Writing guidance

- **Requirements must be testable.** "Fast" is not a requirement; "loads in under 2s on 3G" is. "The system shall…" phrasing keeps them verifiable.
- **Prioritize inside the PRD, not just at the end.** Every functional requirement carries a P0/P1/P2 so the MVP cut is obvious.
- **Metrics over vibes.** If a goal can't be measured, either find the metric or move it to non-goals.
- **Keep it skimmable.** Tables for requirements/metrics/risks; tight prose elsewhere. Aim for a doc a busy reader skims in a couple of minutes and reads fully in ten.
- **Make uncertainty visible.** Assumptions and open questions are features of a good PRD, not embarrassments.

## Delivery

Default to **markdown in chat**. Produce a **Word doc** when the user asks, or when it's clearly going to stakeholders/clients/leadership — in that case follow the `docx` skill to generate it, then present the file. If you delivered markdown, close by offering the doc.

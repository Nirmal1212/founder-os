# Examples

`northwind-pulse/` is a **fictional** product (churn early-warning for B2B SaaS customer success teams) run through the founder-os chain. All names, interviews and numbers are invented placeholders. Real runs of `market` use live web data.

The point is to show the shared-context protocol working: open `context.md`, then follow any ID (for example `D-002` or `T-004`) into the other files and see it reused consistently. `scripts/validate.py` checks that no example file uses an ID that `context.md` doesn't define.

| Order | File | Produced by | Example prompt |
|---|---|---|---|
| 1 | context.md | context | "Set up context for a churn early-warning tool" |
| 2 | research-synthesis.md | research | "Synthesize these 8 interviews and define the ICP" |
| 3 | prd.md, use-cases.csv | pm | "Brainstorm use cases, then write the MVP PRD" |
| 4 | roadmap.md | roadmap | "RICE these use cases and cut to a 12-week MVP" |
| 5 | metrics-tracking-plan.csv | metrics | "Define the north star and tracking plan" |
| 6 | hld.md | architect | "Design the system for this PRD" |
| 7 | lld-api.md | lld | "Define the API and the scoring flow" |
| 8 | erd.md | data-model | "Design the schema" |
| 9 | design-tokens.json | design-artifacts | "Create the design foundations" |
| 10 | market-sizing.md | market | "Size the market and map competitors" |
| 11 | positioning.md | positioning | "Write our positioning and messaging" |
| 12 | launch-plan.md | launch | "Plan the beta launch" |
| 13 | sales-one-pager.md | sales | "Make a one-pager and discovery questions" |

Each file carries an HTML comment on line 2 naming the skill and the context version it read.

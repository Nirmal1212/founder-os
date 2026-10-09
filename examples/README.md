# Examples

`northwind-pulse/` is a **fictional** product (churn early-warning for B2B SaaS customer success teams) run through the founder-os chain. All names, interviews and numbers are invented placeholders. Real runs of `founder-os-market` use live web data.

The point is to show the shared-context protocol working: open `context.md`, then follow any ID (for example `D-002` or `T-004`) into the other files and see it reused consistently. `scripts/validate.py` checks that no example file uses an ID that `context.md` doesn't define.

| Order | File | Produced by | Example prompt |
|---|---|---|---|
| 1 | context.md | founder-os-context | "Set up context for a churn early-warning tool" |
| 2 | research-synthesis.md | founder-os-research | "Synthesize these 8 interviews and define the ICP" |
| 3 | prd.md, use-cases.csv | founder-os-pm | "Brainstorm use cases, then write the MVP PRD" |
| 4 | roadmap.md | founder-os-roadmap | "RICE these use cases and cut to a 12-week MVP" |
| 5 | metrics-tracking-plan.csv | founder-os-metrics | "Define the north star and tracking plan" |
| 6 | hld.md | founder-os-architect | "Design the system for this PRD" |
| 7 | lld-api.md | founder-os-lld | "Define the API and the scoring flow" |
| 8 | erd.md | founder-os-data-model | "Design the schema" |
| 9 | design-tokens.json | founder-os-design-artifacts | "Create the design foundations" |
| 10 | market-sizing.md | founder-os-market | "Size the market and map competitors" |
| 11 | positioning.md | founder-os-positioning | "Write our positioning and messaging" |
| 12 | launch-plan.md | founder-os-launch | "Plan the beta launch" |
| 13 | sales-one-pager.md | founder-os-sales | "Make a one-pager and discovery questions" |

Each file carries an HTML comment on line 2 naming the skill and the context version it read.

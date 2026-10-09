# Northwind Pulse — Project Context
<!-- Produced by: founder-os-context (Mode A). ILLUSTRATIVE SAMPLE: fictional product, all figures are made-up placeholders. -->

version: 3 · last_updated: 2026-10-09

## 1. Vision & thesis
Northwind Pulse is an early-warning system for customer churn. It turns scattered product, billing and CRM data into one Health Score per account and alerts the CSM before a renewal is at risk.
Thesis: small B2B SaaS CS teams can't afford a $50k enterprise CS platform but still lose revenue to churn they could have seen coming.

## 2. ICP & personas
**ICP (D-001):** B2B SaaS companies with 50–200 employees and 5–30 CSMs, on HubSpot + Stripe.

| ID | Persona | Job to be done | Pain |
|---|---|---|---|
| P-001 | Maya, Head of Customer Success | Keep net revenue retention above 100% without adding headcount | Finds out about churn at renewal time, too late to act |
| P-002 | Dev, CS Operations Analyst | Give CSMs one trustworthy view of account health | Stitches health from 4 spreadsheets every Monday |

## 3. Glossary
| ID | Term | Definition | Aliases |
|---|---|---|---|
| T-001 | Account | A paying customer company, the unit we score | Customer, Org |
| T-002 | Signal | A single measurable input about an account (login drop, unpaid invoice, ticket spike) | Input, Metric |
| T-003 | Health Score | 0–100 composite of weighted Signals for one Account, recomputed daily | Risk score |
| T-004 | Risk Alert | A notification raised when a Health Score drops below threshold or falls 15+ points in 7 days | Churn alert |
| T-005 | Playbook | A scripted set of actions triggered by a Risk Alert (post-MVP) | Workflow |

## 4. Decisions log (append-only)
| ID | Decision | Rationale | Supersedes | Source |
|---|---|---|---|---|
| D-001 | Target ICP is 50–200 employee SaaS on HubSpot + Stripe | Narrow integration surface fits a 4-person team (C-002); interviews show highest pain here | — | research-synthesis.md |
| D-002 | MVP = Health Score + Risk Alerts. Playbooks (T-005) deferred | Alerts alone prove value; playbooks double scope against C-002 | — | roadmap.md |
| D-003 | Modular monolith on Postgres, no microservices | 4 engineers, 12 weeks (C-002); relational model fits Signals/Accounts | — | hld.md |
| D-004 | First integrations: HubSpot, Stripe, Segment | Covers CRM, billing and product usage for the ICP | — | prd.md |
| D-005 | North star = Accounts with a Risk Alert acted on within 48h | Measures alert value, not just volume | — | metrics-tracking-plan.csv |

## 5. Constraints
| ID | Constraint |
|---|---|
| C-001 | Audit logging and access control must be SOC 2-ready by month 9 |
| C-002 | Team of 4 engineers; MVP in 12 weeks |
| C-003 | Store no end-customer PII beyond work email and company name |
| C-004 | Pricing must stay under $1,500/month for the median account to remain below CS-platform price points |

## 6. Interfaces (pointers, not copies)
research-synthesis.md · prd.md · use-cases.csv · roadmap.md · metrics-tracking-plan.csv · hld.md · lld-api.md · erd.md · design-tokens.json · market-sizing.md · positioning.md · launch-plan.md · sales-one-pager.md

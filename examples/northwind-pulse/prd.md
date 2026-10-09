# PRD — Northwind Pulse MVP
<!-- Produced by: founder-os-pm (Mode B). Read context v1. ILLUSTRATIVE SAMPLE. -->

## Problem
CS teams at 50–200 person SaaS companies discover churn at renewal, too late to act (research theme 1), because account health is spread across tools (theme 2).

## Goals and success metrics
| Goal | Metric |
|---|---|
| Surface risk early | 70% of churned accounts had a Risk Alert (T-004) 30+ days before churn |
| Alerts get acted on | 60% of Risk Alerts acted on within 48h (north star, D-005) |
| Trusted scores | 80% of CSMs open the "why" panel at least once in week 1 |

## Personas
P-001 Maya (Head of CS), P-002 Dev (CS Ops Analyst).

## Scope (MVP, per D-002)
| ID | Requirement | Priority |
|---|---|---|
| R1 | Connect HubSpot, Stripe, Segment (D-004) | P0 |
| R2 | Daily Health Score (T-003) per Account (T-001) from weighted Signals (T-002) | P0 |
| R3 | Risk Alert on score below 40 or a drop of 15+ points in 7 days, via Slack and email | P0 |
| R4 | "Why did this score change" explanation per Account | P0 |
| R5 | Weekly health digest for the Head of CS | P1 |
| R6 | Configurable Signal weights | P1 |
| R7 | Playbooks (T-005) | Out of scope (D-002) |

## Unhappy paths
Expired integration token → banner plus email to admin. Account with under 14 days of data → "insufficient data" instead of a score. Duplicate accounts across CRM and billing → match on domain, flag unmatched for review.

## Non-goals
Predictive ML models, Salesforce, a mobile app.

## Open questions
Default Signal weights: start with expert-set values, calibrate after 60 days of data. Who owns threshold tuning, CSM or CS Ops?

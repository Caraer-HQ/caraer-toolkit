# Qualified Lead Object Template

Status: Canonical Contact extension.

## Purpose

`qualified_lead` contains sales qualification context after a Lead is
considered actionable.

## Traits

### Enabled by default

- **Table** — qualified sales list.

### Optional by workspace configuration

- **Task** — next-step and follow-up work.
- **Analytics** — funnel reporting.

### Not enabled by default

- **Customer** — apply only after the relationship becomes an active customer.

## Extends

- `Contact`

## Core Properties

| Property | Type |
| --- | --- |
| `sales_stage` | single-select |
| `qualification_outcome` | single-select/string |
| `qualification_date` | date |
| `owner` | relation/reference to Employee |
| `opportunity_context` | multi-line text |
| `next_step` | multi-line text |
| `sales_notes` | multi-line text |

## Relations

- `works_at` → `Company` / `Target` / `Account`.
- `qualified_lead_deals` → `Deal`, when a deal is independently registered.

# Lead Object Template

Status: Canonical Contact extension.

## Purpose

`lead` adds marketing and early-interest context to a Contact.

## Traits

### Enabled by default

- **Table** — lead pipeline list.

### Optional by workspace configuration

- **Analytics** — campaign and engagement reporting.
- **Task** — follow-up work.

### Not enabled by default

- **Customer** and **Qualified Lead** are separate extensions or lifecycle
  transitions; do not duplicate their properties here.

## Extends

- `Contact`

## Core Properties

| Property | Type |
| --- | --- |
| `lead_status` | single-select |
| `lead_source` | single-select/string |
| `campaign` | string |
| `consent_status` | single-select |
| `engagement_score` | number |
| `marketing_notes` | multi-line text |

## Relations

- `works_at` → `Company` / `Target` / `Account`, when known.

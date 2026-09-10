# Deal Object Template

Status: Central draft; independent sales transaction.

## Purpose

`deal` tracks an independently identifiable commercial opportunity or
registration. It is not a Contact or Company extension.

## Traits

### Enabled by default

- **Table** — deal pipeline list.

### Optional by workspace configuration

- **Task** — deal follow-up.
- **Analytics** — pipeline reporting.

### Not enabled by default

- **Customer** and **Account** are related records, not Deal extensions.

## Core Properties

| Property | Type |
| --- | --- |
| `deal_name` | string |
| `deal_status` | single-select |
| `deal_stage` | single-select |
| `amount` | currency/number |
| `expected_close_date` | date |
| `source` | string/single-select |
| `owner` | relation/reference to Employee |
| `deal_notes` | multi-line text |

## Relations

- `deal_company` → `Company` / `Target` / `Account`.
- `deal_contact` → `Contact` / `Qualified Lead`.
- `deal_owner` → `Employee`.
- `partner_deal` → `Partner`, when partner attribution applies.

There is no separate `Opportunity` object in the current model; opportunity
context is represented by Deal and lifecycle properties.

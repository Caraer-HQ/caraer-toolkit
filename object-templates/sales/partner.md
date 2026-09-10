# Partner Object Template

Status: Central draft; confirm against the live portal before schema changes.

## Purpose

`partner` represents an organisation with an explicit collaboration with
Caraer. A Partner may also be an Account when both roles are explicitly valid.

## Traits

### Enabled by default

- **Table** — partner directory.

### Optional by workspace configuration

- **Analytics** — partner performance reporting.
- **Task** — partner enablement work.

### Not enabled by default

- **Reseller** and **Whitelabel** should normally be values of `partner_type`,
  not duplicate organisation records.

## Extends

- `Company`

## Core Properties

| Property | Type |
| --- | --- |
| `partner_type` | multi-select |
| `partner_status` | single-select |
| `partner_notes` | multi-line text |

## Relations

- `partner_contacts` ↔ `Contact` / `Customer`.
- `partner_deals` ↔ `Deal`.

## Model discrepancy

The technical guide describes `Reseller` as a Contact extension, while the
live SendtoDeliver model uses Partner on the organisation record. Keep this
template marked draft until the canonical live model is confirmed.

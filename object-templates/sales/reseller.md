# Reseller Object Template

Status: Central draft; model discrepancy under review.

## Purpose

`reseller` is the technical-model name for a partner collaboration extension
that may coexist with `Customer` on the same Contact. It stores person-level
partner context only; organisation-level partner identity belongs on
`Partner`.

## Traits

### Enabled by default

- **Table** — reseller contact list.

### Optional by workspace configuration

- **Analytics** — partner performance reporting.
- **Task** — enablement and partner follow-up work.

### Not enabled by default

- **Customer** is independent and may coexist when the person also has a
  customer relationship.

## Extends

- `Contact`

## Core Properties

| Property | Type |
| --- | --- |
| `partner_tier` | single-select |
| `commission_percentage` | number/percent |
| `territory` | string |
| `partner_contact_status` | single-select |
| `partner_notes` | multi-line text |

## Model discrepancy

The technical object model defines `Reseller` as a Contact extension, while
the live SendtoDeliver setup uses `Partner` as an organisation extension with
`partner_type = Reseller`. Do not apply either draft automatically until the
canonical live model is confirmed.

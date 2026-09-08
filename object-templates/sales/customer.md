# Customer Object Template

Status: Canonical Contact extension.

## Purpose

`customer` adds service and relationship context to a Contact. Commercial
agreement and billing records remain Caraer Main-specific and are not defined
in this central template family.

## Traits

### Enabled by default

- **Table** — customer list.

### Optional by workspace configuration

- **Task** — customer follow-up.
- **Analytics** — customer health reporting.

### Not enabled by default

- **Partner/Reseller** — add only for an explicit partner collaboration.

## Extends

- `Contact`

## Core Properties

| Property | Type |
| --- | --- |
| `customer_status` | single-select |
| `customer_since` | date |
| `customer_notes` | multi-line text |
| `service_status` | single-select |

## Relations

- `works_at` → `Account`, when the person's company is known.
- `customer_tickets` → `Ticket`.

Customer status must not be inferred from a Contact or Account alone; verify
the actual customer relationship first.

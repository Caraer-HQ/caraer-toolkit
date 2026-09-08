# Company Object Template

Status: Canonical primary object.

## Purpose

`company` is the organisation identity and relationship anchor. It should not
become a catch-all customer-specific property set.

## Traits

### Enabled by default

- **Table** — organisation list.

### Optional by workspace configuration

- **Analytics** — organisation-level reporting.

### Not enabled by default

- `Account`, `Target`, and `Partner` are extensions, not Traits.

## Core Properties

| Property | Type |
| --- | --- |
| `name` | string |
| `legal_name` | string |
| `domain` | domain/string |
| `website` | URL |
| `phone` | phone |
| `lifecycle_status` | single-select |
| `notes` | multi-line text |

## Relations

- `works_at` ← `Contact` / `Customer` / `Lead` / `Qualified Lead`.

Role-specific data belongs on `Target`, `Account`, or `Partner` extensions.

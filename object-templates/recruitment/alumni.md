# Alumni Object Template

Status: Canonical Candidate extension; exclusive recruitment lifecycle.

## Purpose

`alumni` preserves former employment context after an Employee leaves an
organisation.

## Traits

### Enabled by default

- **Table** — alumni list.

### Optional by workspace configuration

- **Analytics** — former-employee reporting.

### Not enabled by default

- **Candidate** and **Employee** are lifecycle peers.

## Extends

- `Candidate`

## Core Properties

| Property | Type |
| --- | --- |
| `alumni_status` | single-select | `active`, `inactive` |
| `alumni_date` | date |
| `former_role` | string |
| `former_relationship_context` | multi-line text |
| `alumni_notes` | multi-line text |

## Lifecycle

`New Candidate → Qualified Candidate → Employee → Alumni`. Preserve the
Candidate identity and transition history.

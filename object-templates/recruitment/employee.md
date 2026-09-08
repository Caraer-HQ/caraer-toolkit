# Employee Object Template

Status: Canonical Candidate extension; exclusive recruitment lifecycle.

## Purpose

`employee` represents a Candidate who has entered employment.

## Traits

### Enabled by default

- **Table** — employee directory.

### Optional by workspace configuration

- **User** — when the employee can log in.
- **Task** — when the employee owns operational work.

### Not enabled by default

- **Candidate** and **Alumni** are lifecycle peers.

## Extends

- `Candidate`

## Core Properties

| Property | Type |
| --- | --- |
| `employee_status` | single-select | `active`, `on_leave`, `ended` |
| `start_date` | date |
| `end_date` | date |
| `department` | string |
| `role` | string |
| `employee_notes` | multi-line text |

## Relations

- `works_at` → `Company` / `Account`.
- `owns` → operational records such as `Task`, `Ticket`, or `Onboarding`.

## Lifecycle

`New Candidate → Qualified Candidate → Employee → Alumni`. Preserve the
Candidate identity and transition history.

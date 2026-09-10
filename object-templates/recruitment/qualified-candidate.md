# Qualified Candidate Object Template

Status: Canonical Candidate extension; qualified lifecycle state.

## Purpose

`qualified_candidate` represents a Candidate who passed initial qualification
and is progressing through the selection process.

## Traits

### Enabled by default

- **Table** — qualified-candidate list.

### Optional by workspace configuration

- **Task** — interviews, assessments, and follow-up work.
- **Analytics** — selection funnel reporting.

### Not enabled by default

- **New Candidate**, **Employee**, and **Alumni** are lifecycle peers.

## Extends

- `Candidate`

## Core Properties

| Property | Type | Values / purpose |
| --- | --- | --- |
| `qualified_candidate_status` | single-select | `matched`, `first_contact`, `first_interview`, `second_interview`, `offer` |
| `qualified_at` | date | Qualification date. |
| `qualification_outcome` | single-select/string | Qualification result. |
| `next_step` | multi-line text | Next recruitment action. |
| `qualification_notes` | multi-line text | Qualification context. |

## Relations

- `applies_to` → `Vacancy`.
- `qualified_candidate_owner` → `Employee`.

## Lifecycle

Transition to `employee` after hire; rejected or withdrawn records remain
auditable.

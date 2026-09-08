# New Candidate Object Template

Status: Canonical Candidate extension; first lifecycle state.

## Purpose

`new_candidate` represents a newly entered candidate who has not yet been
qualified.

## Traits

### Enabled by default

- **Table** — new-candidate list.

### Optional by workspace configuration

- **Task** — screening and follow-up work.
- **Analytics** — recruitment funnel reporting.

### Not enabled by default

- **Qualified Candidate**, **Employee**, and **Alumni** are lifecycle peers.

## Extends

- `Candidate`

## Core Properties

| Property | Type | Values / purpose |
| --- | --- | --- |
| `new_candidate_status` | single-select | `new`, `screening`, `rejected`, `withdrawn` |
| `received_at` | date-time | When the candidate entered the process. |
| `screening_notes` | multi-line text | Initial screening context. |

## Lifecycle

Transition to `qualified_candidate` after qualification; rejected or withdrawn
records remain auditable.

# Candidate Object Template

Status: Canonical primary object; recruitment lifecycle anchor.

## Purpose

`candidate` is the primary recruitment record and identity anchor for a person
moving through the candidate lifecycle.

## Traits

### Enabled by default

- **Table** — candidate list.

### Optional by workspace configuration

- **Analytics** — recruitment funnel reporting.
- **Task** — interview and follow-up work.

### Not enabled by default

- **Employee** and **Alumni** are lifecycle peers, not simultaneous defaults.

## Core Properties

| Property | Type | Notes |
| --- | --- |
| `first_name` | string | Candidate identity. |
| `last_name` | string | Candidate identity. |
| `email` | email | Candidate contact channel. |
| `phone` | phone | Candidate contact channel. |
| `linkedin_url` | URL | Candidate profile. |
| `availability` | single-select/string | Availability context. |
| `specialisms` | multi-select | Candidate skills or areas. |
| `candidate_source` | single-select/string | Acquisition/source channel. |
| `candidate_notes` | multi-line text | Shared candidate context. |
| `not_hired_reason` | single-select | `candidate_withdrew`, `offer_declined`, `not_a_fit`, `position_filled`, `requirements_not_met`, `other` |

## Relations

- `applies_to` → `Vacancy`.
- `candidate_contact` → `Contact`, when a matching person record exists.

## Lifecycle

`New Candidate → Qualified Candidate → Employee → Alumni`. At most one active
extension in this lifecycle may exist for a Candidate; transitions must
preserve the Candidate identity and history.

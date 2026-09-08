# Vacancy Object Template

Status: Canonical primary object; recruitment record.

## Purpose

`vacancy` represents an independently identifiable role or assignment to
which a Candidate can apply.

## Traits

### Enabled by default

- **Table** — vacancy list.

### Optional by workspace configuration

- **Analytics** — recruitment funnel reporting.
- **Task** — vacancy follow-up and hiring work.

### Not enabled by default

- **Candidate** is related through `applies_to`, not an extension of Vacancy.

## Core Properties

| Property | Type |
| --- | --- |
| `vacancy_name` | string |
| `vacancy_status` | single-select |
| `description` | multi-line text |
| `location` | string |
| `employment_type` | single-select |
| `published_at` | date-time |
| `closing_date` | date |
| `vacancy_notes` | multi-line text |

## Relations

No relations are defined yet. Candidate, organisation, and owner relations
will be modelled separately after the primary Vacancy object is confirmed.

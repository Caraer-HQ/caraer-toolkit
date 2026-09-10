# Activity Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`activity` is the top-level object in the activity hierarchy. The object name defines the type, so Extended Objects inherit the base `activity` properties and only add their own fields.

## Traits

### Enabled by default

| Trait | Why it is enabled |
| --- | --- |
| **Table** | Provides the shared activity list with columns, sorting and filtering. |

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When reporting spans multiple activity types. |

### Not enabled by default

Event, Task, Action and Message belong on their respective Extended Objects. Page,
Flow and User are not general Activity capabilities.

## Hierarchy

- `activity`
  - `event`
    - `meeting`
  - `task`
    - `subtask`
  - `milestone`
  - `action`
    - `call`
    - `comment`
    - `formsubmission`
    - `website-sessions`
    - `email`
    - `marketing-email`
    - `call-to-action`
    - `data-enrichment`
    - `profile-completion`
    - `user-creation`
    - `first-login`
    - `automation`
  - `message`
    - `email`
    - `whatsapp`
    - `linkedin`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `activity_name` | string | Human-readable label for the activity. |
| `description` | multi-line text | Short summary of the activity. |
| `start_date` | date-time | When the activity starts or is scheduled to start. |
| `due_date` | date-time | Planned or expected completion date. |
| `end_date` | date-time | Optional completion timestamp. |
| `duration` | duration/number | Normalized duration field. |
| `outcome` | multi-line text | Result or end state of the activity. |
| `progress` | number/percent | Progress of the activity itself. |
| `sort_order` | number | Ordering for UI lists and timelines. |
| `notes` | multi-line text | Internal notes. |

## Inheritance

All Extended Objects inherit these base properties from `activity`:

- `activity_name`
- `description`
- `start_date`
- `due_date`
- `end_date`
- `duration`
- `outcome`
- `progress`
- `sort_order`
- `notes`

## Open Questions

- Should `activity` be linked directly to `company`, or should that relation live on a separate shared base object?

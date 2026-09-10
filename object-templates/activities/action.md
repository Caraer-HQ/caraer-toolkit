# Action Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`action` is the activity object for operational actions.

## Traits

### Enabled by default

| Trait | Why it is enabled |
| --- | --- |
| **Table** | Provides an operational action list with columns, sorting and filtering. |
| **Action** | Represents an interaction or operation with an actor, target or result. |

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When action volume, outcomes or conversion needs reporting. |

### Not enabled by default

Event, Message, Task, Page, Flow and User are not general Action capabilities.

## Hierarchy

- `activity`
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

## Inherited From `activity`

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

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `action_name` | string | Human-readable label for the action. |
| `action_state` | single-select | Operational state of the action. |
| `actor` | relation/string | Person or system that performed the action. |
| `target` | relation/string | Record, person, or object acted on. |
| `payload` | multi-line text | Structured or free-form action payload. |
| `reference_url` | url | Optional source URL for the action. |
| `external_id` | string | External system identifier. |
| `pin_activity` | boolean | Marks the action as pinned in the UI. |

## Known Extended Objects

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

## Open Questions

- Should `action` be the home for all non-communication workflow events, or should some of these children move under `activity` directly?

# Task Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`task` is the activity object for work items that can be assigned and tracked independently.

## Traits

### Enabled by default

| Trait | Why it is enabled |
| --- | --- |
| **Table** | Provides the task list with columns, sorting, filtering and bulk management. |
| **Task** | Provides assignment, status, priority and completion behaviour. |

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Flow** | When tasks move through a configured workflow beyond ordinary status. |
| **Analytics** | When task throughput, ageing or completion needs reporting. |

### Not enabled by default

Event, Action, Message, Page and User are not Task capabilities.

## Hierarchy

- `activity`
  - `task`
    - `subtask`

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
| `assignees` | relation/people | People responsible for the task. |
| `task_status` | single-select | Task lifecycle state: To do, In progress, Waiting, In review, Done, Blocked, or Cancelled. Open/Closed is defined by relation views, not as a task status. |
| `priority` | single-select | Task priority. |
| `task_reference` | string | External or internal task reference. |
| `checklist_count` | number | Cached checklist item count. |
| `dependency_count` | number | Cached dependency count. |

## Known Extended Objects

- `subtask`

## Open Questions

- Open/Closed relation views should filter on the canonical task lifecycle: open = To do, In progress, Waiting, In review, or Blocked; closed = Done or Cancelled.

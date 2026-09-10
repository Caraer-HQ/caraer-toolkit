# Subtask Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`subtask` is the nested task object under `task`.

## Traits

### Inherited from `task`

Subtasks inherit **Table** and **Task** from the base Task Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When subtask-level throughput or completion needs reporting. |

Flow is inherited only if it is enabled for the base Task Object.

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

## Inherited From `task`

- `assignees`
- `task_status`
- `priority`
- `task_reference`
- `checklist_count`
- `dependency_count`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `parent_task_id` | relation | Parent task link. |
| `subtask_order` | number | Position inside the parent task. |
| `is_blocked` | boolean | Whether the subtask is blocked by another item. |

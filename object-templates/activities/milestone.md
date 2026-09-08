# Milestone Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`milestone` is the activity object for key checkpoints.

## Traits

### Enabled by default

| Trait | Why it is enabled |
| --- | --- |
| **Table** | Provides a list of checkpoints with sorting and filtering. |

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When milestone completion and timing need reporting. |
| **Flow** | When milestones follow a formal stage or approval process. |

### Not enabled by default

Event, Task, Action, Message, Page and User are not general Milestone capabilities.

## Hierarchy

- `activity`
  - `milestone`

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
| `milestone_code` | string | Optional stable identifier for the checkpoint. |
| `is_major` | boolean | Marks the milestone as a major milestone. |
| `checkpoint_type` | single-select | Optional categorization within milestone records. |

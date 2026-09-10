# Automation Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`automation` is the concrete action object for automated system events.

## Traits

### Inherited from `action`

Automation records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When automation runs, outcomes or failures need reporting. |

## Hierarchy

- `activity`
  - `action`
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

## Inherited From `action`

- `action_name`
- `action_state`
- `actor`
- `target`
- `payload`
- `reference_url`
- `external_id`
- `pin_activity`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `automation_name` | string | Human-readable automation name. |
| `trigger_name` | string | Trigger that fired the automation. |
| `run_id` | string | Automation run identifier. |
| `automation_result` | single-select | Result such as `success`, `failed`, `partial`. |
| `automation_reference` | string | Link or identifier for the automation definition. |

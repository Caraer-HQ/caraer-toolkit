# Profile Completion Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`profile-completion` is the concrete action object for profile completion flows.

## Traits

### Inherited from `action`

Profile-completion records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When completion rates, missing fields or activation need reporting. |

## Hierarchy

- `activity`
  - `action`
    - `profile-completion`

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
| `completion_target` | number | Target completion percentage. |
| `missing_fields` | multi-line text | Fields still missing from the profile. |
| `completion_rule` | string | Rule used to decide when the profile is complete. |

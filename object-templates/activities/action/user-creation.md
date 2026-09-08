# User Creation Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`user-creation` is the concrete action object for account creation and invitations.

## Traits

### Inherited from `action`

User-creation records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When invitations, activation or account-creation outcomes need reporting. |

## Hierarchy

- `activity`
  - `action`
    - `user-creation`

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
| `user_email` | string/email | Email address for the new user. |
| `invited_at` | date-time | Invitation timestamp. |
| `invite_status` | single-select | Invitation lifecycle state. |
| `created_user_id` | string | External or internal user identifier. |

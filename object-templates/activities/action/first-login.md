# First Login Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`first-login` is the concrete action object for a user's first successful login.

## Traits

### Inherited from `action`

First-login records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When activation, login timing or onboarding completion needs reporting. |

## Hierarchy

- `activity`
  - `action`
    - `first-login`

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
| `logged_in_at` | date-time | First successful login timestamp. |
| `login_method` | single-select | Example: `password`, `magic_link`, `sso`. |
| `device_type` | string | Device category used for the login. |
| `session_id` | string | Session identifier for the login. |

# Website Sessions Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`website-sessions` is the concrete action object for web traffic and session tracking.

## Traits

### Inherited from `action`

Website session records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | Recommended when session volume, engagement or conversion is measured. |

## Hierarchy

- `activity`
  - `action`
    - `website-sessions`

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
| `session_id` | string | Session identifier. |
| `landing_page_url` | url | First page in the session. |
| `referrer_url` | url | Referring page. |
| `utm_source` | string | Campaign source. |
| `utm_medium` | string | Campaign medium. |
| `utm_campaign` | string | Campaign name. |
| `session_duration` | number | Session length in seconds or minutes. |

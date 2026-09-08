# Marketing Email Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`marketing-email` is the concrete action object for marketing campaign emails.

## Traits

### Inherited from `action`

Marketing email records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | Recommended when campaign delivery, engagement or conversion is measured. |

## Hierarchy

- `activity`
  - `action`
    - `marketing-email`

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
| `campaign_id` | string | Marketing campaign identifier. |
| `template_id` | string | Email template identifier. |
| `open_count` | number | Cached open count. |
| `click_count` | number | Cached click count. |
| `unsubscribe_count` | number | Cached unsubscribe count. |
| `bounce_count` | number | Cached bounce count. |

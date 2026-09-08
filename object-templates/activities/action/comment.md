# Comment Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`comment` is the concrete action object for comments and annotations.

## Traits

### Inherited from `action`

Comment records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When comment activity or response timing needs reporting. |

## Hierarchy

- `activity`
  - `action`
    - `comment`

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
| `comment_body` | multi-line text | The comment text. |
| `comment_thread_id` | string | External thread identifier. |
| `parent_comment_id` | string | Parent comment if this is a reply. |
| `comment_author` | relation/string | Author of the comment. |

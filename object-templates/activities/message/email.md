# Email Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`email` is the concrete message object for email communication.

## Traits

### Inherited from `message`

Email records inherit **Table** and **Message** from the base Message Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When email delivery, opens or responses need reporting. |

## Hierarchy

- `activity`
  - `message`
    - `email`

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

## Inherited From `message`

- `message_name`
- `channel`
- `direction`
- `body`
- `sender`
- `recipient`
- `thread_id`
- `timestamp`
- `external_id`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `subject` | string | Email subject line. |
| `cc` | relation/string | Secondary recipients. |
| `bcc` | relation/string | Blind-copy recipients. |
| `reply_to` | string/email | Reply-to address. |
| `mailbox` | string | Source or destination mailbox. |

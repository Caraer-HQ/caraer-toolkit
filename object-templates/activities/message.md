# Message Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`message` is the activity object for communication records.

## Traits

### Enabled by default

| Trait | Why it is enabled |
| --- | --- |
| **Table** | Provides a searchable message list with columns and filters. |
| **Message** | Provides sender, recipient, channel, content and delivery behaviour. |

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When delivery, response or channel performance needs reporting. |

### Not enabled by default

Event, Action, Task, Page, Flow and User are not general Message capabilities.

## Hierarchy

- `activity`
  - `message`
    - `email`
    - `whatsapp`
    - `linkedin`

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
| `message_name` | string | Human-readable label for the message. |
| `channel` | single-select | Communication channel name. |
| `direction` | single-select | Example: `inbound` or `outbound`. |
| `body` | multi-line text | Message content. |
| `sender` | relation/string | Sender identity. |
| `recipient` | relation/string | Primary recipient identity. |
| `thread_id` | string | Conversation grouping. |
| `timestamp` | date-time | When the message was sent or received. |
| `external_id` | string | External provider identifier. |

## Known Extended Objects

- `email`
- `whatsapp`
- `linkedin`

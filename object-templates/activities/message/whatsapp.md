# WhatsApp Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`whatsapp` is the concrete message object for WhatsApp communication.

## Traits

### Inherited from `message`

WhatsApp records inherit **Table** and **Message** from the base Message Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When delivery, response or conversation outcomes need reporting. |

## Hierarchy

- `activity`
  - `message`
    - `whatsapp`

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
| `conversation_id` | string | WhatsApp conversation identifier. |
| `phone_number` | string/phone | Phone number used in the conversation. |
| `provider_message_id` | string | External provider message identifier. |
| `delivery_status` | single-select | Example: `sent`, `delivered`, `read`, `failed`. |
| `read_at` | date-time | When the message was read. |
| `media_type` | single-select | Example: `text`, `image`, `audio`, `video`, `document`. |

## Caraer Main relations

When the records are known, link a WhatsApp record to the relevant Contact or
Customer, Account, and Ticket. Ticket creation must use the provider-qualified
`provider_message_id` as the deduplication key. Unknown or ambiguous sender
matches remain fail-closed.

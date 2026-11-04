# Message Object Template

Status: Draft Activity extension.

## Purpose

`message` is an Extended Object of `activity` for inbound and outbound
communication. Each Message record inherits the Activity properties and native
Message behaviour.

## Traits

### Enabled by default

- **Table** — searchable message list.
- **Message** — native communication behaviour; see
  [traits/message.md](../traits/message.md).

### Optional

- **Analytics** — delivery, response, and channel reporting.

### Excluded

Event, Action, Task, Page, Flow, and User are not general Message
capabilities.

## Shared references

- Activity base properties: [activities.md](activities.md)
- System fields: [system-properties.md](../system-properties.md)
- Native Message behaviour: [traits/message.md](../traits/message.md)

## Properties

These properties belong specifically to `message`; do not repeat inherited
Activity properties here.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `message_name` | Berichtnaam | Message Name | string | single-line | Details | — | - | - | messageCircle | Human-readable message label. |
| `channel` | Kanaal | Channel | single-select | single-select | Delivery | Workspace-defined | - | - | radio | Communication channel. |
| `direction` | Richting | Direction | single-select | single-select | Delivery | `inbound`, `outbound` | - | - | arrowLeftRight | Direction of communication. |
| `body` | Berichtinhoud | Message Body | string | multi-line | Content | — | - | - | fileText | Message content. |
| `sender` | Afzender | Sender | relation | relation | Delivery | Person or organisation target | - | - | send | Sender identity. |
| `recipient` | Ontvanger | Recipient | relation | relation | Delivery | Person or organisation target | - | - | inbox | Primary recipient. |
| `thread_id` | Thread-ID | Thread ID | string | single-line | Delivery | — | Indexed | - | messagesSquare | Conversation grouping key. |
| `timestamp` | Tijdstip | Timestamp | date | date-time | Delivery | — | - | - | clock | Sent or received timestamp. |
| `external_id` | Externe ID | External ID | string | single-line | Delivery | — | - | fingerprint | Provider identifier; enable Unique only when the provider ID is globally unique. |

## Known extensions

`email`, `whatsapp`, and `linkedin`.

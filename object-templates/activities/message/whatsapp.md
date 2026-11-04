# WhatsApp Object Template

Status: Live Caraer Main schema reference, updated 2026-11-03; integration verification pending.

## Purpose

One `whatsapp` record represents one incoming or outgoing message, not an entire
conversation. Main stores the communication context; WhatsApp is transport.

## Traits

- Enabled: **Message**, **Table**, verified live.
- Optional: **Analytics**, not enabled in the audited portal.
- Excluded by default: Event, Action, Task, Page, Flow, User.

## Shared references and native model

- [System properties](../../system-properties.md).
- [Message trait](../../traits/message.md).
- [Message draft](../message.md) and [Activity draft](../activities.md) describe
  the proposed family, not exact live native names.

Live WhatsApp has both Message and Activity extension contexts. Shared native
keys are `title` (required), `description`, `start_date`, `body`,
`activity_status` (`open`, `done`), `pin`, `direction` (`inbound`,
`outbound`), `external_id`, `thread_id`, `sent_at`, `received_at`,
and `snippet`, plus System fields. Preserve these names rather than adding
duplicate name, sender, recipient, or timestamp properties. The concrete object
identifies the channel.

## WhatsApp properties

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `conversation_id` | Gespreks-ID | Conversation ID | string | single-line | Activity | — | Hidden | - | — | Existing native conversation key, not unique per message. |
| `phone_number` | Telefoonnummer | Phone number | string | phone | Details | — | - | - | — | Normalized remote participant; does not replace identity relations. |
| `delivery_status` | Verzendstatus | Delivery status | single-select | single-select | Details | `pending`, `sending`, `sent`, `delivered`, `read`, `failed`, `unknown` | - | - | — | Never blindly retry uncertain delivery. |
| `read_at` | Gelezen op | Read at | date | date | Details | — | Format: dd-MM-yyyy HH:mm | - | — | Provider-confirmed read timestamp only. |
| `media_type` | Mediatype | Media type | single-select | single-select | Details | `text`, `image`, `audio`, `video`, `document`, `sticker`, `location`, `contact`, `other` | - | - | — | Content category. |

## Identifiers and native relations

Use existing `external_id` for the provider-qualified message ID once its native
write contract is verified; no duplicate `provider_message_id` was added. No
Unique rule currently exists on it. Durable idempotency and locking are needed.
Use `property_list` for complete inventory: `object_get(properties: true)`
omitted native identifiers/timestamps during the audit.

Native `from`, `to`, `cc`, `bcc` target Contact. `reply_to` and
`thread` target Message. Resolve actual person context rather than inventing
Customer, Account or Ticket links. Explicit Lead-direction relations were
added and verified on 2026-11-03:

| Label | Name | Type | Details |
| --- | --- | --- | --- |
| Sent by | `sent_by` | relation | WhatsApp → Lead sender; inbound to Caraer, `direction=inbound`. |
| Received by | `received_by` | relation | WhatsApp → Lead recipient; outbound from Caraer, `direction=outbound`. |

Both definitions are visible from Lead and WhatsApp; create record edges from
the WhatsApp record to the matched Lead. Preserve native Contact relations.
Ticket deduplication follows the Ticket contract.

## Verification boundary

The four new properties were reread through live Main MCP on 2026-11-03
(23 total properties). Schema persistence alone does not verify a message
writer, native hidden-field writes, provider receipts, or an end-to-end
conversation. A labelled synthetic record (no transport or recipient), UUID
`3038aec8-f6d1-4c1d-936e-071ae5d6d71a`, confirmed writes of `external_id`,
`thread_id`, `conversation_id`, `direction`, `received_at`, and `body` through
record.create. These native hidden fields are writable through MCP despite
`editable=false` metadata. First transport test requires Jan Hein's explicit
confirmation.

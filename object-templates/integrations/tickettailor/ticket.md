# Ticket Object Template

Status: Draft Action extension with TicketTailor source mapping, derived from
one `ORDER_V2.CREATED` webhook sample. The source sample is not a complete
provider schema; validate unobserved optional values before live adoption.
The display label **Ticket** is distinct from the support-ticket template;
the internal name `event_ticket` keeps the schemas separate.

## Purpose

`event_ticket` is one issued-ticket/registration record; its display label is
**Ticket**. It extends `activity` and `action`, enabling normal Action
timeline behavior while remaining independently listable. Create one record
per issued-ticket fulfilment, not merely one per order or line item. Link it
to its Event and (when matched) the attending Person. Do not relate the Ticket
to its Purchase Order; the purchaser is not necessarily the attendee.

## Traits

### Enabled by default

- **Table** — registration list, filtering, and sorting.
- **Action** — timeline-visible ticket issuance/registration event.

### Optional

- **Analytics** — registration, attendance, or ticket-volume reporting.

### Excluded

Event, Message, Task, Page, Flow, and User are not traits of the Ticket
record. The Event is linked by Relation; it is not inherited by the Ticket.

## Inheritance

- Extend `activity` and `action`, matching the live Caraer pattern used by
  `form_submission`.
- Use inherited `title` for a concise ticket headline, `description` for
  a readable summary, and required `start_date` for the source order-created
  timestamp (`payload.created_at`). Preserve inherited `activity_status`
  semantics; do not overwrite it with an external order status.
- System properties are inherited/provisioned; do not duplicate them here.

## Properties

One record corresponds to a fulfilment under a line item. Fields below come
from that `line_items[]` entry and its `fulfilments[]` entries, with order-level
IDs copied only as external references for deduplication and reconciliation.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `external_ticket_id` | Tickettailor-ticket-ID | TicketTailor Ticket ID | string | single-line | Integration | — | Candidate unique key | — | fingerprint | `line_items[].fulfilments[].reference_id`; expected unique within provider account; verify account scope before enabling Unique. |
| `external_ticket_code` | Ticketcode | Ticket Code | string | single-line | Registration | — | — | — | ticket | `line_items[].fulfilments[].reference_name`; nullable/optional unless confirmed otherwise. |
| `external_line_item_id` | Tickettailor-bestelregel-ID | TicketTailor Line Item ID | string | single-line | Integration | — | Indexed | — | list | `line_items[].id`; a line can issue multiple tickets. |
| `external_item_id` | Tickettailor-item-ID | TicketTailor Item ID | string | single-line | Integration | — | — | — | ticket | `line_items[].item_id`. |
| `external_event_id` | Tickettailor-event-ID | TicketTailor Event ID | string | single-line | Event | — | — | — | calendar | `line_items[].event_summary.event_id`; external event key. |
| `external_event_series_id` | Tickettailor-reeks-ID | TicketTailor Event Series ID | string | single-line | Event | — | — | — | calendarDays | `line_items[].event_summary.event_series_id`; nullable/optional in provider schema until confirmed. |
| `event_name` | Evenementnaam | Event Name | string | single-line | Event | — | — | — | calendar | `line_items[].event_summary.name`. |
| `event_start_at` | Evenement start | Event Start At | date | date-time | Event | — | — | — | calendarClock | `line_items[].event_summary.start_date`; retain timezone-aware source timestamp. |
| `event_end_at` | Evenement einde | Event End At | date | date-time | Event | — | — | — | calendarCheck | `line_items[].event_summary.end_date`; retain timezone-aware source timestamp. |
| `ticket_description` | Ticketbeschrijving | Ticket Description | string | multi-line | Ticket | — | — | — | text | `line_items[].description`; provider description may combine ticket and event copy. |
| `item_type` | Regeltype | Item Type | string | single-line | Ticket | Provider-defined | — | — | tag | `line_items[].type`; sample value indicates a ticket, but retain provider value. |
| `line_item_object` | Regelobject | Line Item Object | string | single-line | Integration | Provider-defined | — | — | braces | `line_items[].object`; observed as a line-item discriminator. |
| `fulfilment_type` | Uitgiftetype | Fulfilment Type | string | single-line | Ticket | Provider-defined | — | — | packageCheck | `line_items[].fulfilment`; sample indicates issued ticket. |
| `quantity` | Aantal | Quantity | number | number | Ticket | — | — | — | hash | `line_items[].quantity`; line-level quantity, not necessarily the number of separately populated fulfilments in every payload. |
| `unit_value` | Ticketwaarde | Unit Value | number | number | Payment | — | — | — | coins | `line_items[].value`; raw source integer. Interpret with order currency multiplier only after confirming units. |
| `line_total` | Regelbedrag | Line Total | number | number | Payment | — | — | — | banknote | `line_items[].total`; raw source integer. |
| `list_price` | Lijstprijs | List Price | number | number | Payment | — | — | — | tag | `line_items[].list_price`; raw source integer. |
| `booking_fee` | Boekingskosten | Booking Fee | number | number | Payment | — | — | — | receipt | `line_items[].booking_fee`; raw source integer. |
| `list_booking_fee` | Lijstboekingskosten | List Booking Fee | number | number | Payment | — | — | — | receipt | `line_items[].list_booking_fee`; raw source integer. |
| `line_item_details` | Overige regelgegevens | Other Line Item Details | structure | structure | Integration | — | — | — | braces | Preserve nullable `bundle_id`, `discount_id`, `store_summary`, `tax`, and any future nested fields without guessing their type. |
| `order_status` | Bestelstatus | Order Status | string | single-line | Registration | Provider-defined | — | — | circleDot | Snapshot from `payload.status`, useful in the registration list; keep separate from inherited Activity status. |
| `participation_status` | Deelname-status | Participation Status | single-select | single-select | Registration | `attending` (Attending), `cancelled` (Cancelled) | — | — | circleDot | Ticket/attendance state shown through the Person and Event links, not order payment state. The supplied create webhook does not establish how cancellation is signalled; map only after confirming the cancellation source. |
Map `payload.created_at` to inherited `start_date` and display it as
registration time; do not add a duplicate stored timestamp without a confirmed
UI need.

## Relations

| Name | Target object | Cardinality | Notes |
| --- | --- | --- | --- |
| `attends` | Event Ticket | Zero or many | Relation label **Attending**; defined on base `person`, direction `person → event_ticket`. A Person can attend zero or more Tickets. Cancellation is a status on the Ticket, not a second relation. |
| `event_tickets` | Event Ticket | Zero or many | Relation label **Tickets**; `event → event_ticket`. The Event can list its Tickets. |

## Source mapping and cardinality

- `payload.line_items[]` is an array; each item can contain a `fulfilments[]`
  array. Create a Ticket record per issued-ticket fulfilment when one
  exists. If no fulfilment exists, do not silently fabricate a ticket ID;
  retain the line item on its order and route it for an explicit fallback
  policy.
- Copy line-item values onto each Ticket record only where useful for
  filtering/display. Preserve the complete line-item array on the separate
  Purchase Order record; there is intentionally no Order-to-Ticket relation.
- `payload.buyer_details` describes the purchaser, not necessarily the ticket
  holder. Link a Ticket to a Person only after a confident
  identity match; never create a Person from email alone without a defined
  deduplication policy.
- An order may contain several events, line items, and fulfilments. Do not
  infer one order = one event or one ticket.

## Source fields requiring schema confirmation

The sample has one line item and one fulfilment only. Its `bundle_id`,
`discount_id`, `store_summary`, and `tax` are null. Confirm non-null shapes and
the relationship between `quantity` and fulfilments from additional examples
before making these fields required or adding further typed properties.

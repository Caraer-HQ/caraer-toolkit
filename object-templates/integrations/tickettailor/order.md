# Order Object Template

Status: Draft integration template, derived from one `ORDER_V2.CREATED`
webhook sample. The sample establishes observed fields, not the complete
TicketTailor contract. Verify optional and currently empty/null structures
against more webhook examples or the provider schema before live adoption.

## Purpose

`purchase_order` is the order-level record received from TicketTailor. It keeps
the buyer and payment/order context. Preserve its full `line_items` payload
here, but do not create relations from an Order to Tickets or Events. Ticket
records are modeled independently from their issued-ticket fulfilments.

## Traits

### Enabled by default

- **Table** — order list and filtering.
- **Action** — order-creation activity in the Person/record timeline.

### Optional

- **Analytics** — order volume and payment reporting, if required.

### Excluded

Event, Message, Task, Page, Flow, and User are not general Order capabilities.
The Action trait is used to expose order creation in the timeline; it does not
make the order itself a scheduled Event.

## Inheritance

- Extend `activity` and `action`, matching the live Caraer pattern used by
  `form_submission`.
- Map `payload.created_at` to inherited required `start_date` and use inherited
  `title`/`description` for a concise order headline and summary.
- Keep source `order_status` separate from inherited `activity_status`.
- Do not duplicate inherited system properties.

## Properties

Properties below are derived from the `body.payload` order. `body` is the
webhook envelope; headers and proxy/request metadata are not order properties.
Do not persist the example's personal values, IP values, or signature.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `external_order_id` | Tickettailor-order-ID | TicketTailor Order ID | string | single-line | Integration | — | Unique | — | fingerprint | `payload.id`; provider order identifier. |
| `webhook_delivery_id` | Webhook-bezorg-ID | Webhook Delivery ID | string | single-line | Integration | — | Unique | — | webhook | `body.id`; delivery/event identifier for deduplication. Confirm uniqueness semantics with provider before enabling Unique. |
| `webhook_event` | Webhook-event | Webhook Event | string | single-line | Integration | — | — | — | webhook | `body.event`, e.g. the event name in this sample. |
| `webhook_created_at` | Webhook ontvangen op | Webhook Created At | date | date-time | Integration | — | — | — | clock | `body.created_at`; sample timestamp format is date-time text. |
| `order_object_type` | Bestelobjecttype | Order Object Type | string | single-line | Integration | Provider-defined | — | — | braces | `payload.object`; provider discriminator (sample identifies an order). |
| `order_status` | Bestelstatus | Order Status | string | single-line | Order | Provider-defined | — | — | circleDot | `payload.status`; keep provider status values without normalization. |
| `status_message` | Statusbericht | Status Message | string | multi-line | Order | — | — | — | messageSquare | `payload.status_message`; nullable in sample. |
| `order_total` | Besteltotaal | Order Total | number | number | Payment | — | — | — | banknote | `payload.total`; preserve raw provider numeric value. Interpret with currency multiplier only after verifying provider units. |
| `currency_code` | Valutacode | Currency Code | string | single-line | Payment | — | — | — | coins | `payload.currency.code`. |
| `currency_symbol` | Valutasymbool | Currency Symbol | string | single-line | Payment | — | — | — | coins | `payload.currency.symbol`. |
| `currency_base_multiplier` | Valuta-basismultiplier | Currency Base Multiplier | number | number | Payment | — | — | — | calculator | `payload.currency.base_multiplier`; retain to interpret provider monetary integers. |
| `buyer_first_name` | Voornaam koper | Buyer First Name | string | single-line | Buyer | — | — | — | user | `payload.buyer_details.first_name`; buyer is not necessarily the attendee. |
| `buyer_last_name` | Achternaam koper | Buyer Last Name | string | single-line | Buyer | — | — | — | user | `payload.buyer_details.last_name`. |
| `buyer_name` | Naam koper | Buyer Name | string | single-line | Buyer | — | — | — | user | `payload.buyer_details.name`; preserve provider's display name. |
| `buyer_email` | E-mailadres koper | Buyer Email | string | email | Buyer | — | — | — | mail | `payload.buyer_details.email`; personal data, restrict access appropriately. |
| `buyer_phone` | Telefoon koper | Buyer Phone | string | phone | Buyer | — | — | — | phone | `payload.buyer_details.phone`; nullable in sample. |
| `buyer_address` | Adres koper | Buyer Address | structure | structure | Buyer | — | — | — | mapPin | `payload.buyer_details.address`; sample keys are `address_1`, `address_2`, `address_3`, `postal_code`, all null. Verify populated shape before defining child properties. |
| `buyer_custom_questions` | Aangepaste kopervragen | Buyer Custom Questions | structure | structure | Buyer | — | — | — | listChecks | `payload.buyer_details.custom_questions`; empty array in sample, item schema unknown. |
| `marketing_opt_in` | Marketingtoestemming | Marketing Opt-in | string | single-line | Consent | Provider-defined | — | — | megaphone | `payload.marketing_opt_in`; null in sample, so type and semantics need another populated example/provider confirmation. Do not treat null as consent. |
| `order_notes` | Bestelnotities | Order Notes | string | multi-line | Order | — | — | — | note | `payload.notes`. |
| `payment_plan` | Betaalplan | Payment Plan | structure | structure | Payment | — | — | — | creditCard | `payload.payment_plan`; null in sample, shape unknown. |
| `referral_tag` | Verwijzingstag | Referral Tag | string | single-line | Attribution | — | — | — | tag | `payload.referral_tag`; nullable in sample. |
| `metadata` | Metagegevens | Metadata | structure | structure | Integration | — | — | — | braces | `payload.meta_data`; empty array in sample, element shape unknown. |
| `transactions` | Transacties | Transactions | structure | structure | Payment | — | — | — | receipt | `payload.transactions`; empty array in sample, transaction shape unknown. |
| `line_items` | Bestelregels | Line Items | structure | structure | Order | — | — | — | list | `payload.line_items`; preserve complete array for audit/reprocessing. Per-ticket fields are separately mapped to `event_ticket`, without a record relation. |
| `resource_url` | Bron-URL | Resource URL | string | url | Integration | — | — | — | link | `body.resource_url`; provider API resource URL. |

## Relations

| Name | Target object | Cardinality | Notes |
| --- | --- | --- | --- |
| `purchased_by` | Person | One | Label **Purchased by**; `purchase_order → person`. The buyer may not be the attendee. |

## Source envelope inventory

The supplied request also contains top-level `method`, `url`, `query`, and
`client_ip`, plus `headers`. These describe HTTP transport, proxy routing,
request diagnostics, and authentication; they are not order data. Header names
observed were `Accept-Encoding`, `Cdn-Loop`, `Cf-Connecting-Ip`, `Cf-Ew-Via`,
`Cf-Ipcity`, `Cf-Ipcontinent`, `Cf-Ipcountry`, `Cf-Iplatitude`,
`Cf-Iplongitude`, `Cf-Postal-Code`, `Cf-Ray`, `Cf-Region`, `Cf-Region-Code`,
`Cf-Timezone`, `Cf-Visitor`, `Cf-Worker`, `Content-Length`, `Content-Type`,
`Tickettailor-Webhook-Signature`, `True-Client-Ip`, `User-Agent`,
`X-Forwarded-For`, `X-Forwarded-Host`, `X-Forwarded-Port`, `X-Forwarded-Proto`,
`X-Forwarded-Scheme`, `X-Original-Forwarded-For`, `X-Real-Ip`, `X-Request-Id`,
and `X-Scheme`.

Verify the webhook signature at the receiver, but never put its value in this
object, template examples, logs, or records. Do not persist proxy/client IP
fields as registration properties. If operational delivery tracing is needed,
keep only a separately governed request identifier and retention policy.

## Source shape not fully known from this sample

- `buyer_details.address` fields are present but null; populated formats are
  unverified.
- `custom_questions`, `meta_data`, and `transactions` are empty arrays; their
  element schemas are unobserved.
- `payment_plan`, `status_message`, `referral_tag`, `marketing_opt_in`,
  line-item `bundle_id`, `discount_id`, `store_summary`, and `tax` are null in
  this sample; null does not establish their non-null types or semantics.
- Money-like line-item fields are integers. Preserve the source values and
  multiplier; do not assume major/minor currency units until confirmed.
- The request contains one line item and one fulfilment only. Treat both as
  arrays and do not assume one order equals one event or one ticket.

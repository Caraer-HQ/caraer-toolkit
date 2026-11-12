# Support Ticket Object Template

Status: Toolkit template; naming updated 2026-11-12 for live adoption in Caraer
Main.

- Internal name: `support_ticket`
- Label: Support Ticket
- Plural: Support Tickets

## Purpose

`support_ticket` is the support work record for human-required customer or lead
work. It identifies the work, its routing state, the accountable employee, and
the customer/company context.

## Traits

### Enabled by default

- **Table** — ticket list, sorting, and filtering.
- **Task** — native task behaviour; see [traits/task.md](../traits/task.md).

### Optional

- **Analytics** — support volume, ageing, and completion reporting.

### Excluded

Event, Action, Message, and Page are not Support Ticket capabilities;
customer-facing text belongs in Message/WhatsApp records.

## Shared references

- Task behaviour: [traits/task.md](../traits/task.md)
- Task property set (`task_status`, `priority`, `assignees`):
  [activities/task.md](../activities/task.md)
- System fields: [system-properties.md](../system-properties.md)

## Properties

Object-specific properties only; do not repeat Task-inherited properties
(`task_status`, `priority`, `assignees`, `task_reference`) or Activity base
properties here. Types and formats follow the live MCP
`property.types.list` / `property.formats.list` values.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `source_channel` | Bronkanaal | Source Channel | single-select | single-select | Support | `whatsapp` (WhatsApp), `email` (Email), `phone` (Phone), `sms` (SMS), `linkedin` (LinkedIn), `chat` (Chat), `web_form` (Web Form), `other` (Other) | - | - | radio | Channel the ticket originated from. |
| `category` | Categorie | Category | single-select | single-select | Support | Workspace-defined support categories | - | - | tag | Support category. |
| `issue_summary` | Probleemsamenvatting | Issue Summary | string | multi-line | Support | — | - | - | alertCircle | Short description of the issue. |
| `next_action` | Volgende actie | Next Action | string | multi-line | Support | — | - | - | arrowRightCircle | Next operational step. |
| `escalation_reason` | Escalatiereden | Escalation Reason | string | multi-line | Support | — | - | - | arrowUpCircle | Why escalation is needed. |
| `customer_contact_reference` | Klantcontactreferentie | Customer Contact Reference | string | single-line | Support | — | - | - | userCheck | Customer/contact reference when a separate reference is needed. |
| `policy_decision` | Beleidsbesluit | Policy Decision | structure | structure | Support | — | - | - | scale | Decision and policy outcome logging; free-form JSON shape. |
| `agent_notes` | Agentnotities | Agent Notes | string | multi-line | Support | — | - | - | note | Internal agent context, reasoning, handoff, and follow-up notes. Keep customer-facing text in Message/WhatsApp records. |

`task_status` is the leading routing/status field (inherited from Task:
To do, In progress, Waiting, In review, Done, Blocked, Cancelled).
Open/Closed is defined by relation views, not by a stored property.

## Relations

| Internal name | Connected object | Meaning |
| --- | --- | --- |
| `customer_tickets` | Customer | Direct link to the contact person. |
| `account_open_tickets` | Account | Account view for open tickets; filtering belongs to the UI relation view. |
| `account_closed_tickets` | Account | Account view for closed tickets; filtering belongs to the UI relation view. |
| `ticket_owner` | Employee | Accountable owner; on escalation this must be an active Employee. |
| `assignee` | Employee / Partner User / other supported task target | Working assignment; distinct from `ticket_owner`. |

Relation IDs (live Caraer Main, verified 2026-11-12):

- `customer_tickets`: `8024082b-231d-4e8a-ad63-4cf2e9320ad5`
- `account_open_tickets`: `829d11c6-8894-46e1-99d7-28c8b3bcabe1`
- `account_closed_tickets`: `9287114b-2216-4968-bdc5-212eec66ea6e`
- `ticket_owner`: `0aa55647-fed2-41cd-bdf8-3a02ecaa1c2a`

When known, link both `customer_tickets` and the relevant Account. This
explicitly connects the person to the company they work at. Customer should
normally resolve through `works_at` to exactly one correct Account.

## Workflow rules

1. Match inbound senders to exactly one Lead or Customer before processing.
2. For a Customer match, resolve the underlying Contact and preserve/merge its
   Contact `platforms` multi-select value.
3. Link known WhatsApp, Customer, Account, and Support Ticket records.
4. Keep unknown or ambiguous matches fail-closed.

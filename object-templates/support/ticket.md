# Ticket Object Template

Status: Live Caraer Main schema reference, updated 2026-08-13.

- Object UUID: `804683d7-6e65-4f72-ac59-4b391337bf3d`

## Purpose

`ticket` is the support work record for human-required customer or lead work.
It identifies the work, its routing state, the accountable employee, and the
customer/company context.

## Traits and inheritance

- **Table** and **Task** are enabled.
- Ticket inherits the shared activity/task context, including `activity_status`
  and task behaviour.
- `task_status` is the leading Ticket routing/status field. `activity_status`
  is only the shared activity lifecycle field. Its canonical options are To do,
  In progress, Waiting, In review, Done, Blocked, and Cancelled. Open/Closed is
  defined by relation views.

## Core properties

| Property | Type / format | Purpose |
| --- | --- | --- |
| `task_status` | single-select | Routing state: To do, In progress, Waiting, In review, Done, Blocked, or Cancelled. |
| `priority` | single-select | Ticket urgency. |
| `source_channel` | single-select or string | Channel from which the ticket originated. |
| `category` | single-select or string | Support category. |
| `issue_summary` | string / multi-line | Short description of the issue. |
| `next_action` | string / multi-line | Next operational step. |
| `escalation_reason` | string / multi-line | Why escalation is needed. |
| `customer_contact_reference` | string | Customer/contact reference when a separate reference is needed. |
| `policy_decision` | string / structure | Decision and policy outcome logging. |
| `provider_message_id` | string | Provider-qualified unique message identifier for deduplication. |
| `agent_notes` | string / multi-line | Internal agent context, reasoning, handoff, and follow-up notes. Keep customer-facing text in Message/WhatsApp records. |

## Relations

| Internal name | Connected object | Meaning |
| --- | --- | --- |
| `customer_tickets` | Customer | Direct link to the contact person. |
| `account_open_tickets` | Account | Account view for open tickets; filtering belongs to the UI relation view. |
| `account_closed_tickets` | Account | Account view for closed tickets; filtering belongs to the UI relation view. |
| `ticket_owner` | Employee | Accountable owner; on escalation this must be an active Employee. |
| `assignee` | Employee / Partner User / other supported task target | Working assignment; distinct from `ticket_owner`. |

Relation IDs:

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
3. Check `provider_message_id` before creating a Ticket.
4. Link known WhatsApp, Customer, Account, and Ticket records.
5. Keep unknown or ambiguous matches fail-closed.

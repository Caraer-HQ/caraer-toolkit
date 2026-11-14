# Support Ticket Object Template

Status: Toolkit template; naming updated 2026-11-12 for live adoption in Caraer
Main. Live schema adopted 2026-11-13; see verification boundary below.

- Internal name: `support_ticket`
- Label: Support Ticket
- Plural: Support Tickets

## Caraer Main adoption status

Verified creation on 2026-11-12 in Caraer BV
(`b234fe94-7d2a-4edf-9b51-f1fa6f8503cc`):

- Support Ticket UUID: `7a710ab6-126a-4df8-b59b-3ca773143fac`.
- Default trait: `table`; Table and Task enabled (Task read back 2026-11-13).
- Extensions: Task (`bb4d9d45-ea23-4da6-a29f-4300eb9fb19a`) and
  Activity (`3823542c-b0d5-4b01-b905-0d3f82cf5f0d`), verified after Task enablement.
- Groups: Details, Planning, Support, AI, System, Activity.
- Suite: Operations. Number ID disabled.
- All 12 object-specific fields created and read back with the shared Task /
  Activity fields (31 properties). Priority then added successfully using the
  portal's existing options; expected total 32. `policy_decision` is absent.
- `reported_by` and `assignee` configured and their context-specific targets
  read back. Assignee selection remains an implementation-specific decision.
- Final consolidated read after Priority creation returned `Authentication
  required`; the Priority write succeeded, but its separate final read is not
  verified. Do not recreate this object or duplicate existing fields.

Assignee selection and category values remain implementation-specific; see the
Caraer-only implementation note rather than treating them as shared defaults.

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

Object-specific properties only; do not duplicate fields provisioned by the
Task trait or inherited from Task / Activity. Enabling the Task trait creates
fields; the exact generated property keys still need live verification. Inspect
the resulting schema before creating any shared task fields manually. The Task
reference documents the intended shared property set, not a verified list of
trait-generated fields. Types and formats follow the live MCP
`property.types.list` / `property.formats.list` values.

Category options are implementation-specific and deliberately not enumerated
in this shared template. Choose stable support/product-area categories in each
implementation; do not embed release-specific lists here.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `source_channel` | Bronkanaal | Source Channel | single-select | single-select | Support | `whatsapp` (WhatsApp), `email` (Email), `phone` (Phone), `sms` (SMS), `linkedin` (LinkedIn), `chat` (Chat), `web_form` (Web Form), `other` (Other) | - | - | radio | Channel the ticket originated from. |
| `category` | Categorie | Category | single-select | single-select | Support | Workspace-defined support categories | - | - | tag | Support category. |
| `issue_summary` | Probleemsamenvatting | Issue Summary | string | multi-line | Support | — | - | - | alertCircle | Short description of the issue. |
| `next_action` | Volgende actie | Next Action | string | multi-line | Support | — | - | - | arrowRightCircle | Next operational step. |
| `escalation_reason` | Escalatiereden | Escalation Reason | string | multi-line | Support | — | - | - | arrowUpCircle | Why escalation is needed. |
| `customer_contact_reference` | Klantcontactreferentie | Customer Contact Reference | string | single-line | Support | — | - | - | userCheck | Customer/contact reference when a separate reference is needed. |
| `agent_notes` | Agentnotities | Agent Notes | string | multi-line | AI | — | - | - | note | Internal handoff context, follow-up notes, and information still needed; keep separate from the decision rationale and customer-facing draft. |
| `agent_reasoning` | Agentonderbouwing | Agent Reasoning | string | multi-line | AI | — | - | - | note | Concise decision rationale: relevant facts, linked evidence, assumptions, uncertainty, and why the proposed action is appropriate. Not a private chain-of-thought transcript. |
| `ai_summary` | AI-samenvatting | AI Summary | string | multi-line | AI | — | - | - | note | AI-maintained summary of the customer's request, relevant conversation context, current resolution state, and outstanding questions. Distinct from the short issue_summary. |
| `suggested_response` | Voorgesteld antwoord | Suggested Response | string | multi-line | AI | — | - | - | note | Draft customer-facing reply in the appropriate language and tone, grounded in the linked conversation and verified facts. Not a sent message. |
| `ai_impact` | AI-impact | AI Impact | single-select | single-select | AI | `unknown` (Unknown), `low` (Low), `medium` (Medium), `high` (High), `critical` (Critical) | - | - | flag | AI-assessed consequence of the issue, not task priority. Use Unknown when evidence is insufficient; do not default to Low. |
| `ai_impact_assessment` | AI-impactbeoordeling | AI Impact Assessment | string | multi-line | AI | — | - | - | note | Evidence-based explanation of affected users/accounts, blocked workflows, scope, available workaround, and consequences. Identify missing evidence and uncertainty; link relevant records. |

### AI group and response automation

Create a dedicated **AI** property group containing `agent_reasoning`,
`ai_summary`, `suggested_response`, `ai_impact`, `ai_impact_assessment`, and
`agent_notes`. These fields support
triage, response drafting, and handoff; they do not replace the operational
Support fields or shared task status.

Impact is a separate assessment from inherited task `priority`: consequences
inform prioritisation but do not automatically overwrite priority, change
assignment, escalate, or send a response. Define impact thresholds for the
selected implementation. Low means limited disruption; Medium means meaningful
but contained disruption; High means major disruption; Critical means severe
or widespread consequences requiring immediate attention. Use Unknown when
there is not enough evidence, and never treat a missing assessment as Low.
Reassess impact when new evidence arrives. Keep the explanation tied to
observable facts rather than unsupported precision or confidence scores.

Refresh the summary and draft when relevant conversation context or ticket
state changes. Keep the rationale concise and evidence-based, identify missing
information in Agent Notes, and do not present unverified assumptions as facts
in Suggested Response. Internal rationale and notes are not customer-facing.

These properties store automation inputs and outputs; creating or filling them
does not itself send a response. The implementation defines generation triggers
and any review/send rules. Store actual inbound/outbound communications and
send results on linked Message/WhatsApp records, not in these draft fields.

`task_status` is the intended leading routing/status field, using the shared
Task lifecycle (To do, In progress, Waiting, In review, Done, Blocked, Cancelled).
Verify its provisioning source and actual options against the resulting schema.
Open/Closed is defined by relation views, not by a stored property.

## Relations

| Internal name | Connected object | Meaning |
| --- | --- | --- |
| `reported_by` | Customer / Account / Company | Reporter of the Support Ticket; link both person and organisation context when known. Forward label: Reported by. Reverse label: Reported tickets. |
| `assignee` | Any object with the User trait enabled, subject to portal-specific selection | Record responsible for handling the ticket, including accountability on escalation. Discover eligible objects in the selected portal and confirm which may be assignees before configuring this relation. |

Use `reported_by` to link the known Customer and relevant Account or Company.
Customer should normally resolve through `works_at` to the correct Account;
preserve the direct person link as well as the organisation context.
Open and closed ticket lists are filtered views using `task_status`, not
separate stored relations.

`assignee` is the sole responsibility relation for Support Ticket; do not add a
separate accountable-owner relation. The shared Task reference calls its
assignment property `assignees`; verify the inherited schema and map that
assignment to `assignee` without creating duplicate assignment relations.

### Portal-specific assignee research and selection

Assignee eligibility is based on the **User trait**, not an object name such as
Employee or Partner User. Any object with that trait enabled is a candidate;
the relation links records of the selected objects, not the object schemas
themselves. Do not hard-code Employee as the only permitted assignee type,
including for escalation.

Before configuring `assignee` in an implementation:

1. Confirm the selected portal and authenticated company identity.
2. Inspect the portal's object schemas and enabled traits to identify every
   object with the User trait enabled. Do not infer eligibility from names or
   from the shared template. If discovery is incomplete, report that limitation
   rather than treating uninspected objects as ineligible.
3. Inspect existing assignment relations and Task-generated fields to determine
   supported targets and avoid creating duplicate responsibility relations.
4. Present the discovered eligible objects with their labels and internal names,
   then ask: **“Which of these User-trait objects should be allowed as assignees
   for Support Tickets in this portal?”**
5. Record the user's selection in the portal-specific implementation, not as a
   fixed target list in this shared template. Apply the confirmed selection and
   verify the resulting relation targets and assignment behaviour.

User-trait eligibility is not automatic selection: confirm the allowed object
set before configuring it. Escalation uses an active assignee from that set;
any narrower escalation rule is an implementation-specific decision.

These are the agreed target relations, not a claim that live relations have
already been renamed or migrated. Confirm live endpoints and existing links
before applying the design; no live relation UUID is assigned here yet.

## Workflow rules

1. Match inbound senders to exactly one Lead or Customer before processing.
2. For a Customer match, resolve the underlying Contact and preserve/merge its
   Contact `platforms` multi-select value.
3. Link known WhatsApp and Support Ticket records; connect known Customer,
   Account, and Company reporters through `reported_by`.
4. Keep unknown or ambiguous matches fail-closed.

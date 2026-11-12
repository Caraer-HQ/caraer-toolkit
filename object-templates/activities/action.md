# Action Object Template

Status: Draft Activity extension.

## Purpose

`action` is an Extended Object of `activity` for operational actions. Each
Action record inherits the Activity properties and native Action behaviour.

## Traits

### Enabled by default

- **Table** — operational action list.
- **Action** — native operational-action behaviour; see
  [traits/action.md](../traits/action.md).

### Optional

- **Analytics** — action-volume, outcome, or conversion reporting.

### Excluded

Event, Message, Task, Page, Flow, and User are not general Action
capabilities.

## Shared references

- Activity base properties: [activities.md](activities.md)
- System fields: [system-properties.md](../system-properties.md)
- Native Action behaviour: [traits/action.md](../traits/action.md)

## Properties

These properties belong specifically to `action`; do not repeat inherited
Activity properties here.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `action_name` | Actienaam | Action Name | string | single-line | Details | — | - | - | activity | Human-readable action label. |
| `action_state` | Actiestatus | Action State | single-select | single-select | Details | Workspace-defined | - | - | circleDot | Operational action state. |
| `actor` | Uitgevoerd door | Actor | relation | relation | Details | Person, Employee, User, or system target | - | - | user | Record or system that performed the action. |
| `target` | Doel | Target | relation | relation | Details | Workspace-defined record target | - | - | crosshair | Record or entity acted on. |
| `payload` | Actiegegevens | Action Payload | string | multi-line | Details | — | - | - | braces | Structured or free-form action payload. |
| `reference_url` | Referentie-URL | Reference URL | string | url | Details | — | - | - | link | Optional source URL. |
| `external_id` | Externe ID | External ID | string | single-line | Details | — | - | - | fingerprint | Provider identifier; enable Unique only when the provider ID is globally unique. |
| `pin_activity` | Activiteit vastzetten | Pin Activity | checkbox | single-checkbox | Details | — | - | - | pin | Marks the action as pinned in UI. |

## Known extensions

`call`, `note`, `formsubmission`, `website-sessions`, `email`,
`marketing-email`, `call-to-action`, `data-enrichment`, `profile-completion`,
`user-creation`, `first-login`, and `automation`.

`candidate-review` is an optional Extended Object of `note`, not a direct
Action extension; see [Note](action/note.md).

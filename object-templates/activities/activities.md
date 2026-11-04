# Activity Object Template

Status: Draft base object.

## Purpose

`activity` is the base object for operational records. An Extended Object such
as `action`, `message`, `event`, or `task` is simultaneously an Activity and
its specialised record type: it inherits the Activity properties and adds only
its own properties and trait.

## Traits

### Enabled by default

- **Table** — shared activity list, sorting, and filtering.

### Optional

- **Analytics** — reporting across activity types.

### Excluded

The Action, Message, Event, and Task traits belong on their respective
Extended Objects, not on `activity`.

## Shared references

- System fields: [system-properties.md](../system-properties.md)
- Native activity traits: [Action](../traits/action.md),
  [Message](../traits/message.md), [Event](../traits/event.md), and
  [Task](../traits/task.md)

## Properties

All Activity extensions inherit these properties. `Settings` lists active UI
settings; `Required when` stores conditional logic. `-` means no setting or
condition is configured.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `activity_name` | Activiteitsnaam | Activity Name | string | single-line | Details | — | - | - | activity | Human-readable activity label. |
| `description` | Beschrijving | Description | string | multi-line | Details | — | - | - | fileText | Summary and context. |
| `start_date` | Startdatum | Start Date | date | date-time | Planning | — | - | - | calendar | Scheduled start. |
| `due_date` | Vervaldatum | Due Date | date | date-time | Planning | — | - | - | calendarClock | Target completion. |
| `end_date` | Einddatum | End Date | date | date-time | Planning | — | - | - | calendarCheck | Actual end timestamp. |
| `duration` | Duur | Duration | number | duration | Planning | — | - | - | timer | Normalized duration. |
| `outcome` | Resultaat | Outcome | string | multi-line | Details | — | - | - | circleCheck | Result or end state. |
| `progress` | Voortgang | Progress | number | percent | Planning | — | - | - | chartNoAxesColumnIncreasing | Progress of the activity itself. |
| `sort_order` | Sorteervolgorde | Sort Order | number | number | Planning | — | - | - | arrowDownUp | Manual UI ordering. |
| `notes` | Notities | Notes | string | multi-line | Details | — | - | - | note | Internal working notes. |

## Hierarchy

```text
activity
├── action
├── event
│   └── meeting
├── message
│   ├── email
│   ├── whatsapp
│   └── linkedin
├── task
│   └── subtask
└── milestone
```

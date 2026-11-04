# Event Object Template

Status: Draft Activity extension.

## Purpose

`event` is an Extended Object of `activity` for calendar-like, schedulable
records. Each Event record inherits the Activity properties and native Event
behaviour.

## Traits

### Enabled by default

- **Table** — event list, sorting, and filtering.
- **Event** — native calendar, scheduling, recurrence, and event interaction
  behaviour; see [traits/event.md](../traits/event.md).

### Optional

- **Analytics** — event volume, attendance, registration, or completion
  reporting.
- **Page** — public event detail pages; see [traits/page.md](../traits/page.md).
- **Flow** — only when `event_status` is insufficient for the workflow.

### Excluded

Task, Action, Message, and User are not general Event capabilities. Store
event communication in related Message records.

## Shared references

- Activity base properties: [activities.md](activities.md)
- System fields: [system-properties.md](../system-properties.md)
- Native Event behaviour: [traits/event.md](../traits/event.md)

## Properties

These properties belong specifically to `event`; do not repeat inherited
Activity or optional Page properties here.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `location` | Locatie | Location | string | single-line | Details | — | - | - | mapPin | Physical or virtual event location. |
| `timezone` | Tijdzone | Timezone | string | single-line | Planning | IANA timezone | - | - | globe | Timezone used for the schedule. |
| `all_day` | Hele dag | All Day | checkbox | single-checkbox | Planning | — | - | - | calendarDays | Whether the event spans the whole day. |
| `calendar_event_id` | Agenda-event-ID | Calendar Event ID | string | single-line | Integrations | — | - | - | calendar | External calendar identifier; enable Unique only when the provider ID is globally unique. |
| `calendar_url` | Agenda-URL | Calendar URL | string | url | Integrations | — | - | - | link | Link to the external calendar item. |
| `event_type` | Eventtype | Event Type | single-select | single-select | Details | Workspace-defined | - | - | tags | Event category. |
| `event_status` | Eventstatus | Event Status | single-select | single-select | Planning | `draft`, `scheduled`, `cancelled`, `completed` | - | - | circleDot | Event lifecycle state. |
| `audience` | Doelgroep | Audience | multi-select | multi-select | Details | Workspace-defined | - | - | users | Intended audience. |
| `registration_required` | Aanmelding vereist | Registration Required | checkbox | single-checkbox | Registration | — | - | - | clipboardCheck | Whether people need to register. |
| `registration_deadline` | Aanmelddeadline | Registration Deadline | date | date-time | Registration | — | - | `registration_required = true` | calendarClock | Optional registration deadline. |
| `capacity` | Capaciteit | Capacity | number | number | Registration | — | - | - | usersRound | Optional maximum participants. |
| `cost` | Kosten | Cost | number | currency | Registration | Workspace currency | - | - | banknote | Optional participation fee. |
| `recurrence_rule` | Herhalingsregel | Recurrence Rule | string | single-line | Planning | iCalendar RRULE | - | - | repeat | Recurrence definition. |
| `publicly_visible` | Publiek zichtbaar | Publicly Visible | checkbox | single-checkbox | Publication | — | - | - | eye | Whether the event may be listed publicly. |
| `featured` | Uitgelicht | Featured | checkbox | single-checkbox | Publication | — | - | - | star | Whether the event is highlighted. |
| `cover_image` | Omslagafbeelding | Cover Image | file | file | Publication | — | - | - | image | Optional event image or poster. |

## Relations

| Name | Target object | Cardinality | Notes |
| --- | --- | --- | --- |
| `event_owner` | Person, Employee, or User | One required | Accountable owner; Relation, not text. |
| `event_organizer` | Person, Team, or Company | Zero or one | Organisation or person arranging the event. |
| `event_location` | Location | Zero or one | Use when Location is an independent record. |
| `event_speaker` | Person | Zero or many | Use for speakers or presenters. |

## Participation

Where invitation, registration, or RSVP history is needed, model it as an
`event_participation` join object rather than a multi-select Event property.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `participation_status` | Deelname-status | Participation Status | single-select | single-select | Details | `invited`, `registered`, `accepted`, `declined`, `tentative`, `attended`, `no_show`, `cancelled` | - | - | circleDot | RSVP or attendance state. |
| `participation_role` | Deelnamerol | Participation Role | single-select | single-select | Details | `participant`, `volunteer`, `speaker`, `leader`, `organizer` | - | - | badge | Role in the event. |
| `invited_at` | Uitgenodigd op | Invited At | date | date-time | Planning | — | - | - | mailPlus | Invitation timestamp. |
| `responded_at` | Gereageerd op | Responded At | date | date-time | Planning | — | - | - | reply | Response timestamp. |
| `response_note` | Reactienotitie | Response Note | string | multi-line | Details | — | - | - | note | Optional response or registration note. |

## Known extension

`meeting`.

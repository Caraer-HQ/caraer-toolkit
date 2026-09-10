# Event Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`event` is the schedulable Extended Object of `activity`. It holds the fields that apply to all calendar-like items.

## Traits

### Enabled by default

| Trait | Why it is enabled |
| --- | --- |
| **Table** | Provides the standard event-record list with columns, sorting and filtering. |
| **Event** | Provides calendar behaviour, date/time handling, calendar views, recurrence and event interactions. |

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When the workspace needs reporting on event volume, attendance, registration or completion. |
| **Page** | When each event should also have a public-facing detail page. |
| **Flow** | When events move through a workflow such as draft, review, published and archived. Use this only if `event_status` alone is insufficient. |

### Not enabled by default

- **Task** — an event is scheduled activity, not work that must be completed.
- **Action** — an event should not automatically be treated as an interaction or logged action.
- **Message** — communication around an event belongs in related Message records.
- **User** — an event does not represent a person who can sign in.

The recommended initial configuration is therefore **Table + Event**, with
Analytics enabled only when reporting requirements are known.

## Hierarchy

- `activity`
  - `event`
    - `meeting`

## Inherited From `activity`

- `activity_name`
- `description`
- `start_date`
- `due_date`
- `end_date`
- `duration`
- `outcome`
- `progress`
- `sort_order`
- `notes`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `location` | Text | Physical or virtual location for the event. |
| `timezone` | Text | Timezone used for the schedule. |
| `all_day` | Checkbox | Whether the event spans the whole day. |
| `calendar_event_id` | Text | External calendar identifier. |
| `calendar_url` | Website | Link to the calendar item. |
| `event_type` | Single choice | Workspace-defined category, such as meeting, appointment, service, class, webinar or social event. |
| `event_status` | Single choice | `draft`, `scheduled`, `cancelled`, `completed`. |
| `audience` | Multiple choice | Intended audience; values are workspace-defined. |
| `registration_required` | Checkbox | Whether participants need to register. |
| `registration_deadline` | Date | Optional deadline for registration. |
| `capacity` | Number | Optional maximum number of participants. |
| `cost` | Currency | Optional participation fee. |
| `recurrence_rule` | Text | Recurrence definition, if recurring events are supported. |
| `publicly_visible` | Checkbox | Whether the event may appear in a public calendar. |
| `featured` | Checkbox | Whether the event should be highlighted in a calendar or listing. |
| `cover_image` | File | Optional event image or poster. |

## Relations

| Relation | Target object | Cardinality | Label from event | Label from target |
| --- | --- | --- | --- | --- |
| `event_owner` | Person / Employee / User | One required | owned by | owns event |
| `event_organizer` | Person / Team / Company | Zero or one | organised by | organises event |
| `event_location` | Location | Zero or one | held at | hosts event |
| `event_speaker` | Person | Zero or many | presented by | speaks at event |

`event_owner` is a Relation, not a text property. The owner is an independently
existing Record responsible for the event. The owner may be different from the
organizer, speaker, invitee or participant.

## Invitations and participation

If an event needs invitations, registration or RSVP tracking, model each person’s
participation as a separate `event_participation` join object rather than as a
multiple-choice property on the Event.

| Property / relation | Type | Notes |
| --- | --- | --- |
| `event` | Relation | Required relation to `event`. |
| `person` | Relation | Required relation to the invited or registered person. |
| `participation_status` | Single choice | `invited`, `registered`, `accepted`, `declined`, `tentative`, `attended`, `no_show`, `cancelled`. |
| `participation_role` | Single choice | `participant`, `volunteer`, `speaker`, `leader`, `organizer`. |
| `invited_at` | Date | When the invitation was sent. |
| `responded_at` | Date | When the person responded. |
| `response_note` | Long text | Optional response or registration note. |

## Known Extended Objects

- `meeting`

## Open Questions

- Should recurring events be a separate Extended Object, or a property on `event`?
- Should `event_participation` be a formal shared object or configured only in workspaces that need RSVP tracking?

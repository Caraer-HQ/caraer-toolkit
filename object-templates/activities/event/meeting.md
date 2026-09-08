# Meeting Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`meeting` is the concrete event object for meetings.

## Traits

### Inherited from `event`

Meetings inherit **Table** and **Event** from the base Event Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When meeting attendance, outcomes or volume needs reporting. |
| **Page** | When each meeting needs a public or shared detail page. |

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

## Inherited From `event`

- `location`
- `timezone`
- `all_day`
- `calendar_event_id`
- `calendar_url`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `meeting_platform` | single-select | Example: `google_meet`, `zoom`, `teams`, `in_person`. |
| `meeting_url` | url | Meeting link if the meeting is virtual. |
| `recording_url` | url | Optional recording link. |
| `minutes_url` | url | Link to notes or minutes. |
| `attendee_count` | number | Cached attendee count. |

## Open Questions

- Should attendees be modeled as a relation to contacts, or as a rollup/list property?

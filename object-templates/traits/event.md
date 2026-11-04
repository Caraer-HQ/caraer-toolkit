# Event Trait Reference

The `event` trait gives an object native calendar and scheduled-event
behaviour. It is normally enabled on the `event` Extended Object, which also
extends [`activity`](../activities/activities.md).

## Trait configuration

| Field | Value |
| --- | --- |
| `name` | `event` |
| Typical object | `event` Extended Object |
| Base object | `activity` |
| Native role | Calendar, scheduling, recurrence, and event interactions |

## Provisioning boundary

The trait supplies native event behaviour. It does not replace the Activity
base properties or Event object-specific properties in
[`activities/event.md`](../activities/event.md). No trait-provisioned,
editable property keys are asserted here until verified against a live portal.

## Use

- Enable for calendar-like, schedulable activities.
- Use a separate participation join object when registration or RSVP history is
  required.
- Add `Table` separately for list management; add `Page`, `Analytics`, or
  `Flow` only when the workspace requires them.


# Task Trait Reference

The `task` trait gives an object native task behaviour. It is normally enabled
on the `task` Extended Object, which also extends
[`activity`](../activities/activities.md).

## Trait configuration

| Field | Value |
| --- | --- |
| `name` | `task` |
| Typical object | `task` Extended Object |
| Base object | `activity` |
| Native role | Work item tracked to completion |

## Provisioning boundary

The trait supplies native task behaviour and creates fields. The exact
provisioned property keys and any generated relations remain unverified
(user clarification, 2026-11-12). Inspect the resulting live schema before
manually creating task fields, and distinguish trait-generated fields from
properties inherited through object extensions. The intended shared Task
property set is documented in [`activities/task.md`](../activities/task.md);
that document is not a verified inventory of trait-generated fields.

## Use

- Enable for work that has a lifecycle toward completion.
- Add `Table` separately for task-list management.
- Add `Flow` only when native task status is insufficient; add `Analytics` only
  when task reporting is required.


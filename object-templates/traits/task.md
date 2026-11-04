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

The trait supplies native task behaviour and the native **Activity** property
group. It does not itself provision editable properties or relations. Task
object-specific properties are documented in
[`activities/task.md`](../activities/task.md).

## Use

- Enable for work that has a lifecycle toward completion.
- Add `Table` separately for task-list management.
- Add `Flow` only when native task status is insufficient; add `Analytics` only
  when task reporting is required.


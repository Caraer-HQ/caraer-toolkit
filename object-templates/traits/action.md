# Action Trait Reference

The `action` trait gives an object native operational-action behaviour. It is
normally enabled on the `action` Extended Object, which also extends
[`activity`](../activities/activities.md).

## Trait configuration

| Field | Value |
| --- | --- |
| `name` | `action` |
| Typical object | `action` Extended Object |
| Base object | `activity` |
| Native role | Operational interaction or operation |

## Provisioning boundary

The trait supplies native behaviour. It does not replace the Activity base
properties or the Action object-specific properties documented in
[`activities/action.md`](../activities/action.md). No trait-provisioned,
editable property keys are asserted here until verified against a live portal.

## Use

- Enable for records that describe an operation, interaction, or system action.
- Do not enable on `activity` itself merely to record a generic activity.
- Add `Table` separately when a list view is required.


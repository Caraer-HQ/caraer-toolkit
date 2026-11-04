# Message Trait Reference

The `message` trait gives an object native communication-record behaviour. It
is normally enabled on the `message` Extended Object, which also extends
[`activity`](../activities/activities.md).

## Trait configuration

| Field | Value |
| --- | --- |
| `name` | `message` |
| Typical object | `message` Extended Object |
| Base object | `activity` |
| Native role | Communication record and delivery context |

## Provisioning boundary

The trait supplies native message behaviour. It does not replace the Activity
base properties or Message object-specific properties in
[`activities/message.md`](../activities/message.md). No trait-provisioned,
editable property keys are asserted here until verified against a live portal.

## Use

- Enable for inbound or outbound communication records.
- Model channel-specific records (such as email, WhatsApp, or LinkedIn) as
  Message extensions.
- Add `Table` separately when a searchable message list is required.


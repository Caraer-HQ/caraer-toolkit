# Call Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`call` is the concrete action object for phone calls.

## Traits

### Inherited from `action`

Call records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When call volume, disposition or conversion needs reporting. |

## Hierarchy

- `activity`
  - `action`
    - `call`

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

## Inherited From `action`

- `action_name`
- `action_state`
- `actor`
- `target`
- `payload`
- `reference_url`
- `external_id`
- `pin_activity`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `phone_number` | string/phone | Phone number dialed or received. |
| `call_direction` | single-select | `inbound` or `outbound`. |
| `call_disposition` | single-select | Outcome such as `answered`, `no_answer`, `voicemail`, `hung_up`. |
| `recording_url` | url | Optional call recording. |
| `transcript_url` | url | Optional transcript link. |

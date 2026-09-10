# Call To Action Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`call-to-action` is the concrete action object for CTA interactions.

## Traits

### Inherited from `action`

CTA records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | Recommended when CTA clicks, submissions or conversions are measured. |

## Hierarchy

- `activity`
  - `action`
    - `call-to-action`

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
| `cta_label` | string | Label shown to the user. |
| `cta_destination` | url | Target link or destination. |
| `cta_variant` | string | Optional CTA variant or style key. |
| `clicked_at` | date-time | Time of click, if applicable. |

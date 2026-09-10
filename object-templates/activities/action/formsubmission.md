# Form Submission Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`formsubmission` is a specific action subtype for incoming form events.

## Traits

### Inherited from `action`

Form submissions inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When submission volume, processing or conversion needs reporting. |

## Hierarchy

- `activity`
  - `action`
    - `formsubmission`

## Inherited From `activity`

All base `activity` properties apply here and are not repeated.

## Inherited From `action`

All base `action` properties apply here and are not repeated.

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `form_name` | string | Name of the form that was submitted. |
| `submission_id` | string | External or internal submission identifier. |
| `submitted_at` | date-time | Exact submission timestamp. |
| `source_url` | url | Page where the form was submitted. |
| `landing_page` | url | Optional landing page preceding the form. |
| `form_fields` | JSON/multi-line text | Raw submitted field payload or normalized field map. |
| `form_status` | single-select | Example values: `new`, `received`, `processed`, `ignored`. |
| `form_action` | single-select | Optional action outcome such as `create_lead`, `create_contact`, `create_task`. |
| `notes` | multi-line text | Internal notes specific to the submission. |

## Inheritance

`formsubmission` inherits from `activity` and `action`.

## Recommended Relations

| From | To | Relation | Notes |
| --- | --- | --- | --- |
| action | formsubmission | `has_formsubmission` | Parent action owns the submission record. |
| formsubmission | contact | `creates_or_updates_contact` | If the submission maps to a person. |
| formsubmission | company | `creates_or_updates_company` | If the submission maps to a company. |

## Open Questions

- Do we want to store the raw payload as JSON, or only normalized fields?
- Should `form_action` be a single-select, or should it point to an automation/workflow object?

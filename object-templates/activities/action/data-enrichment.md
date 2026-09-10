# Data Enrichment Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`data-enrichment` is the concrete action object for enrichment jobs and lookups.

## Traits

### Inherited from `action`

Data-enrichment records inherit **Table** and **Action** from the base Action Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When enrichment volume, confidence or provider outcomes need reporting. |

## Hierarchy

- `activity`
  - `action`
    - `data-enrichment`

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
| `provider` | string | Enrichment provider name. |
| `enrichment_run_id` | string | Run identifier. |
| `confidence_score` | number | Confidence in the result. |
| `source_count` | number | Number of sources used. |
| `result_summary` | multi-line text | Short summary of the enriched data. |

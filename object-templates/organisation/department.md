# Department Object Template

Status: Central primary object.

## Purpose

`department` represents an organisational department or team grouping.

## Traits

### Enabled by default

- **Table** — department list.

### Optional by workspace configuration

- **Analytics** — department-level reporting.

### Not enabled by default

- Organisation and employee relations are defined separately.

## Core Properties

| Property | Type |
| --- | --- |
| `department_name` | string |
| `department_code` | string |
| `department_status` | single-select |
| `department_description` | multi-line text |
| `department_notes` | multi-line text |

## Relations

To be defined with the organisation and employee model.

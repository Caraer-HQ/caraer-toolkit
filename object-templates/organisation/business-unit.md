# Business Unit Object Template

Status: Central primary object.

## Purpose

`business_unit` represents a distinct business, division, or operating unit
within an organisation.

## Traits

### Enabled by default

- **Table** — business-unit list.

### Optional by workspace configuration

- **Analytics** — business-unit reporting.

### Not enabled by default

- Organisation and hierarchy relations are defined separately.

## Core Properties

| Property | Type |
| --- | --- |
| `business_unit_name` | string |
| `business_unit_code` | string |
| `business_unit_status` | single-select |
| `business_unit_description` | multi-line text |
| `business_unit_notes` | multi-line text |

## Relations

To be defined with the organisation hierarchy.

# Location Object Template

Status: Central primary object.

## Purpose

`location` represents a physical, geographic, or operational location of an
organisation.

## Traits

### Enabled by default

- **Table** — location list.

### Optional by workspace configuration

- **Analytics** — location-level reporting.

### Not enabled by default

- Organisation-specific relations are defined separately.

## Core Properties

| Property | Type |
| --- | --- |
| `location_name` | string |
| `location_type` | single-select |
| `address_line_1` | string |
| `address_line_2` | string |
| `postal_code` | string |
| `city` | string |
| `region` | string |
| `country` | string |
| `location_status` | single-select |
| `location_notes` | multi-line text |

## Relations

To be defined with the organisation model.

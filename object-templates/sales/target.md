# Target Object Template

Status: Canonical Company extension.

## Purpose

`target` marks a Company as a potential organisation of interest before an
active customer relationship exists.

## Traits

### Enabled by default

- **Table** — target list.

### Optional by workspace configuration

- **Analytics** — target and funnel reporting.
- **Task** — prospecting work.

### Not enabled by default

- **Account** — apply only after an active customer relationship is confirmed.

## Extends

- `Company`

## Core Properties

| Property | Type |
| --- | --- |
| `target_status` | single-select |
| `target_source` | string/single-select |
| `target_notes` | multi-line text |

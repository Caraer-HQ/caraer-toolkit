# Contact Object Template

Status: Canonical primary object.

## Purpose

`contact` is the stable person identity. Role-specific data belongs on an
extension; company context belongs in Relations such as `works_at`.

## Traits

### Enabled by default

- **Table** — searchable contact list.

### Optional by workspace configuration

- **User** — only for people who can authenticate or operate in a workspace.
- **Analytics** — when contact engagement is reported.

### Not enabled by default

- **Customer**, **Lead**, **Employee**, **Candidate**, **Alumni**, and
  **Partner/Reseller** are extensions, not Traits.

## Core Properties

| Property | Type | Ownership rule |
| --- | --- | --- |
| `first_name` | string | Person identity. |
| `last_name` | string | Person identity. |
| `email` | email | Person contact channel; unique when available. |
| `phone` | phone | Person contact channel. |
| `mobile_phone` | phone | Person contact channel. |
| `linkedin_url` | URL | Person profile. |
| `platforms` | multi-select | Known communication channels. |
| `job_title` | string | Person-level employment information. |
| `notes` | multi-line text | General person notes only. |

## Relations

- `works_at` → `Company` / `Account` — employment or company context.

Do not copy company, customer, marketing, sales, or support fields onto
Contact.

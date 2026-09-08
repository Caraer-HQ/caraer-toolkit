# Onboarding Object Template

Status: Central draft; independent operational record.

## Purpose

`onboarding` tracks the implementation journey for a customer, partner, or
other configured organisation. It is not a billing record.

## Traits

### Enabled by default

- **Table** — onboarding work list.
- **Task** — milestones and follow-up work.

### Optional by workspace configuration

- **Analytics** — onboarding progress reporting.

### Not enabled by default

- **Customer** and **Account** are related records, not extensions of
  Onboarding.

## Core Properties

| Property | Type |
| --- | --- |
| `onboarding_name` | string |
| `onboarding_status` | single-select |
| `onboarding_type` | single-select |
| `start_date` | date |
| `target_date` | date |
| `completed_date` | date |
| `progress` | number/percent |
| `next_step` | multi-line text |
| `onboarding_notes` | multi-line text |

## Relations

- `onboarding_account` → `Account`.
- `onboarding_partner` → `Partner`, when relevant.
- `onboarding_owner` → `Employee`.
- `onboarding_contact` → `Contact` / `Customer`.

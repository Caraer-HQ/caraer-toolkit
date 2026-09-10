# Account Object Template

Status: Canonical Company extension.

## Purpose

`account` marks a Company as an active customer organisation and relationship
anchor. Billing fields and billing objects remain outside this central setup.

## Traits

### Enabled by default

- **Table** — account list.

### Optional by workspace configuration

- **Analytics** — account health and relationship reporting.
- **Task** — account work.

### Not enabled by default

- **Customer** is a Contact extension, not an Account extension.

## Extends

- `Company`

## Core Properties

| Property | Type |
| --- | --- |
| `account_status` | single-select |
| `customer_status` | single-select |
| `account_notes` | multi-line text |

## Relations

- `works_at` ← `Customer` / `Contact`.
- `account_open_tickets` ← `Ticket`.
- `account_closed_tickets` ← `Ticket`.
- `account_deals` ↔ `Deal`.

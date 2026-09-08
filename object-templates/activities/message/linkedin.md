# LinkedIn Object Template

Status: Draft.

Source: ClickUp list `1.9.2. - Activities - Action`.

## Purpose

`linkedin` is the concrete message object for LinkedIn communication.

## Traits

### Inherited from `message`

LinkedIn records inherit **Table** and **Message** from the base Message Object.

### Optional by workspace configuration

| Trait | When to enable it |
| --- | --- |
| **Analytics** | When delivery, response or campaign outcomes need reporting. |

## Hierarchy

- `activity`
  - `message`
    - `linkedin`

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

## Inherited From `message`

- `message_name`
- `channel`
- `direction`
- `body`
- `sender`
- `recipient`
- `thread_id`
- `timestamp`
- `external_id`

## Core Properties

| Property | Type | Notes |
| --- | --- | --- |
| `linkedin_thread_id` | string | LinkedIn conversation identifier. |
| `profile_url` | url | LinkedIn profile URL. |
| `inmail_id` | string | LinkedIn InMail identifier. |
| `connection_degree` | number | Connection distance when relevant. |

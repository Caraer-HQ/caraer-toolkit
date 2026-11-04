# Task Object Template

Status: Draft Activity extension.

## Purpose

`task` is an Extended Object of `activity` for work tracked to completion.
Each Task record inherits the Activity properties and native Task behaviour.

## Traits

### Enabled by default

- **Table** — task list, sorting, and filtering.
- **Task** — native task behaviour; see [traits/task.md](../traits/task.md).

### Optional

- **Flow** — only when native task status is insufficient.
- **Analytics** — throughput, ageing, and completion reporting.

### Excluded

Event, Action, Message, Page, and User are not general Task capabilities.

## Shared references

- Activity base properties: [activities.md](activities.md)
- System fields: [system-properties.md](../system-properties.md)
- Native Task behaviour: [traits/task.md](../traits/task.md)

## Properties

These properties belong specifically to `task`; do not repeat inherited
Activity properties here.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `assignees` | Toegewezen aan | Assignees | relation | relation | Planning | Employee or User target | - | - | users | People responsible for the task. |
| `task_status` | Taakstatus | Task Status | single-select | single-select | Planning | `to_do`, `in_progress`, `waiting`, `in_review`, `done`, `blocked`, `cancelled` | Required | - | circleDot | Native task lifecycle state. |
| `priority` | Prioriteit | Priority | single-select | single-select | Planning | Workspace-defined | - | - | flag | Relative urgency. |
| `task_reference` | Taakreferentie | Task Reference | string | single-line | Details | — | - | - | fingerprint | Internal/external identifier; enable Unique only when used as a stable ID. |
| `checklist_count` | Aantal checklistitems | Checklist Count | number | number | Planning | — | Hidden | - | listChecks | Derived/cache field if required by the implementation. |
| `dependency_count` | Aantal afhankelijkheden | Dependency Count | number | number | Planning | — | Hidden | - | gitBranch | Derived/cache field if required by the implementation. |

## Relations

Relations for projects, accountable owner, parent task, and subtasks remain
workspace decisions. Use Relations for independently identifiable records;
do not model extension ownership as a Relation.

## Known extension

`subtask`.

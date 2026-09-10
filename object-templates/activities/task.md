# Task Object Template

Status: Draft schema.

## Object

| Name | Label NL | Label EN | Description | Icon | Navigation | Suite |
| --- | --- | --- | --- | --- | --- | --- |
| `task` | Taak | Task | A discrete unit of work tracked to completion. | `listTodo` | Visible | Portal decision |

## Traits

| Name | Enabled | Purpose | Settings |
| --- | --- | --- | --- |
| Table | Yes | List, sort, filter, and manage task records. | Default view is a portal decision. |
| Task | Yes | Native task behaviour. | Adds the Activity group; no editable fields or relations are provisioned on its own. |
| Flow | No | Workflow beyond standard task status. | Enable only if required. |
| Analytics | No | Throughput, ageing, and completion reporting. | Enable only if required. |

## Properties

| Name | Label NL | Label EN | Description | Icon | Type | Format | Group | Required | Default | Rules | Options | Settings | Provisioned by trait | Source | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `title` | Titel | Title | Canonical short task name. | `idCard` | string | single-line | Details | Yes | — | — | — | — | Task | Task schema | Agreed |
| `description` | Beschrijving | Description | Task summary and context. | — | string | multi-line | Details | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `start_date` | Startdatum | Start Date | Planned start date and time. | — | date | date-time | Planning | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `due_date` | Vervaldatum | Due Date | Target completion date and time. | — | date | date-time | Planning | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `end_date` | Einddatum | End Date | Actual completion date and time. | — | date | date-time | Planning | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `duration` | Duur | Duration | Normalized task duration. | — | number | duration | Planning | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `outcome` | Resultaat | Outcome | Result or final outcome. | — | string | multi-line | Details | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `progress` | Voortgang | Progress | Completion percentage. | — | number | percent | Planning | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `sort_order` | Sorteervolgorde | Sort Order | Manual order for lists and timelines. | — | number | number | Planning | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `notes` | Notities | Notes | Internal working notes. | — | string | multi-line | Details | No | — | — | — | — | Task | Activity/work-item schema | Proposed |
| `assignees` | Toegewezen aan | Assignees | People responsible for the task. | — | relation | people | Planning | No | — | — | Employee / user targets | — | Task | Task schema | Proposed |
| `task_status` | Taakstatus | Task Status | Task lifecycle state. | — | single-select | single-select | Planning | Yes | To do | — | To do; In progress; Waiting; In review; Done; Blocked; Cancelled | — | Task | Task schema | Proposed |
| `priority` | Prioriteit | Priority | Relative urgency. | — | single-select | single-select | Planning | No | Normal | — | To be agreed | — | Task | Task schema | Proposed |
| `task_reference` | Taakreferentie | Task Reference | External or internal reference. | — | string | single-line | Details | No | — | unique if used as external ID | — | — | Task | Task schema | Proposed |
| `checklist_count` | Aantal checklistitems | Checklist Count | Cached number of checklist items. | — | number | number | Planning | No | 0 | read-only if derived | — | — | Task | Task schema | Proposed |
| `dependency_count` | Aantal afhankelijkheden | Dependency Count | Cached number of task dependencies. | — | number | number | Planning | No | 0 | read-only if derived | — | — | Task | Task schema | Proposed |

System-managed object fields are documented centrally and are not repeated in
this task-specific template.

## Relations

| Name | Label NL | Label EN | Target object | Cardinality | Description | Status |
| --- | --- | --- | --- | --- | --- | --- |
| — | — | — | — | — | No Task relations agreed yet. | Deferred |

## Deferred Decisions

| Area | Decision needed |
| --- | --- |
| Properties | Approve, reject, or refine the proposed rows and their options/settings. |
| Relations | Project, assignee/owner, parent task, and subtasks. |
| Traits | Flow and Analytics. |

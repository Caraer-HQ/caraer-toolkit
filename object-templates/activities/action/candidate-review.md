# Candidate Review Object Template

Status: Toolkit template.

## Purpose

`candidate-review` is an optional Extended Object of [Note](note.md) for
evaluating a Candidate in the context of a Vacancy or Match. It inherits Note
content, attachments, the General relation, and the Activity/Action context,
and adds only review-specific properties. It is not an independent sibling of
Note. A Candidate Review is one record with both Note and Candidate Review
contexts, not two records connected by a relation.

## Traits

### Inherited from `note`

Candidate Review records inherit **Table** and **Action** through Note.

## Hierarchy

- `activity`
  - `action`
    - `note`
      - `candidate-review`

## Shared references

- Note base properties and General relation: [note.md](note.md)
- Activity properties: [activities.md](../activities.md)
- Action properties: [action.md](../action.md)
- Action trait: [../../traits/action.md](../../traits/action.md)

## Core Properties

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `candidate` | Kandidaat | Candidate | relation | relation | Recruitment | Candidate | - | Always | user | Candidate being reviewed. |
| `vacancy` | Vacature | Vacancy | relation | relation | Recruitment | Vacancy | - | - | briefcaseBusiness | Vacancy context for the review. |
| `match` | Match | Match | relation | relation | Recruitment | Match | - | - | gitCompareArrows | Match context for the review. |
| `review_summary` | Beoordelingssamenvatting | Review Summary | string | multi-line | Review | — | - | - | fileText | Overall assessment. |
| `review_score` | Beoordelingsscore | Review Score | number | number | Review | — | - | - | star | Workspace-defined score; define scale at adoption. |
| `review_recommendation` | Advies | Recommendation | single-select | single-select | Review | Advance, Hold, Reject | - | - | thumbsUp | Recommended next decision. |
| `review_status` | Beoordelingsstatus | Review Status | single-select | single-select | Review | Draft, Completed, Shared | - | Always | circleDot | Lifecycle of the review. |
| `strengths` | Sterke punten | Strengths | string | multi-line | Review | — | - | - | thumbsUp | Relevant candidate strengths. |
| `concerns` | Aandachtspunten | Concerns | string | multi-line | Review | — | - | - | triangleAlert | Risks, gaps, or concerns. |
| `review_next_step` | Volgende stap | Next Step | string | multi-line | Review | — | - | - | arrowRight | Follow-up action resulting from the review. |

The reviewer is represented by the inherited `actor` property. The Candidate
relation is required; Vacancy and Match are optional so the review can also be
used for a general Candidate assessment.

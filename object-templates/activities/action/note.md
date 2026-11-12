# Note Object Template

Status: Toolkit template.

## Purpose

`note` stores one authored internal entry that preserves context about one or
more related records: an observation, conversation summary, interview summary,
research note, handover, or decision.

Object labels: **Note** / **Notes**. Dutch labels: **Notitie** / **Notities**.

A Note is content, not a planned task, communication transport, conversation
thread, or replacement for a structured interview assessment. Multiple dated
entries should be separate Note records rather than appended indefinitely to a
single catch-all text property.

## Before creation: Q&A

### 1. Do you use different kinds of notes?

Examples include general notes, call summaries, interview notes, handover
notes, and Candidate Reviews. If all notes serve the same purpose, start with
one Note object and the **General** relation. No type property is needed.

### 2. How would you like to organise those kinds of notes?

| Approach | How it works | Navigation and timeline |
| --- | --- | --- |
| Type property | Keep one Note object and add a type property only when selected during setup. | One sidebar item; use filtering to distinguish types, without separate relation tabs or object categories. |
| Relations | Keep one Note object and use different relations for different note contexts, starting with General. | One sidebar item; multiple relations can be organised into tabs. With only one relation, the tabs are not shown. |
| Extended objects — preferred for distinct timeline categories | Keep Note / Notes as the base object with the General relation. Create note types, such as [Candidate Review](candidate-review.md), as Extended Objects of Note, inheriting its properties and adding only type-specific fields. | Notes provides a combined overview of all notes, including extended types. Each extended type also functions as an object with its own sidebar item and separate overview, and can be distinguished in the timeline. |

Choose a type property for lightweight classification, relations for tab-based
organisation within one object, or Extended Objects of Note when the types need
their own properties and timeline identity. These are not independent sibling
Action objects. Candidate Review is an option,
not a required object for every Notes setup.

Extended note types inherit the properties of the main Note object, including
its body and attachments, as well as its inherited Activity/Action properties.
Define common properties once on Note; keep only type-specific additions on
each extension. For example, a Candidate Review appears in both the combined
Notes overview and the Candidate Review overview as the same record, not a
duplicated note.

### 3. Which records should the notes connect to?

Choose the adopted object types that notes can concern, such as Candidate,
Match, Company, or Vacancy. The **General** relation supports this shared
context and leaves room for additional specialised relations later.

Record the selected approach before creating the object. Do not automatically
add a type property, additional relations, or specialised objects.

## Hierarchy

```text
activity
  action
    note
      candidate-review (optional Extended Object)
```

The Activity and Action contexts describe the same record identity. Do not
create separate Activity, Action, and Note records connected by Relations.

## Traits

### Enabled by default

- **Table** — list, sorting, filtering, and saved views.
- **Action** — operational Activity/Action context and timeline behaviour.

### Optional

- **Analytics** — counts by author, date, and related context. Content analysis
  requires separate authorised access.

### Excluded by default

Page, Flow, User, Event, Message, and Task. Follow-up work belongs in linked
Task records; discussion is not stored as Note content.

## Shared references

- Activity properties: [activities.md](../activities.md)
- Action properties: [action.md](../action.md)
- Action trait: [../../traits/action.md](../../traits/action.md)
- System properties: [../../system-properties.md](../../system-properties.md)
- Activities access model: [../access.md](../access.md)

System fields such as `uuid`, `createdAt`, and `updatedAt` remain
platform-managed. Do not create duplicate Note-specific versions.

## Inherited field roles

Use inherited fields before adding Note-specific equivalents:

| Role | Inherited field | Note use |
| --- | --- | --- |
| Title | `action_name` | Short human-readable subject. Reuse a native `title` if provisioned; do not add `note_title`. |
| Summary | `description` | Optional short preview; not a second copy of the body. |
| Note date | `start_date` | Authored or effective timestamp, including imported or backdated entries. |
| Author | `actor` | Original human or system author. |
| External reference | `external_id` | Optional source identifier; qualify it before enabling uniqueness. |
| Source URL | `reference_url` | Optional link to the original entry. |
| Pin | `pin_activity` | Reuse native pin behaviour where provisioned. |

Do not add a separate visibility field. A stored visibility value is not an
access-control mechanism unless record, file, search, export, API, and AI
permissions explicitly enforce it.

## Core Properties

Create these only when no inherited or native field provides the same meaning.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `note_body` | Inhoud | Note Body | string | multi-line | Details | - | Required; nonPublic=true; webpagePublic=false; sensitive=true | - | fileText | Authoritative note content. Reject whitespace-only content. Reuse a native `body` field if the destination provisions one. |
| `note_attachments` | Bijlagen | Attachments | file | multi-file | Attachments | - | nonPublic=true; webpagePublic=false; sensitive=true | - | paperclip | Optional managed file references; do not embed file bytes in the body or payload. |

## Optional Properties

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Icon | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `note_source` | Herkomst | Source | single-select | single-select | Integration | Manual, Import, API, Automation | - | - | download | Creation mechanism, not authorship. |
| `note_tags` | Labels | Tags | tag | tag | Details | Workspace-defined | - | - | tags | Optional tags; verify the destination tag control before adoption. |
| `note_import_key` | Importreferentie | Import Key | string | single-line | Integration | - | Unique when adopted; read-only in UI | - | fingerprint | Optional source-qualified identity for idempotent imports. |

## Relations

### Business context

Use the multi-object Relation `note_about`, labelled **General**, to connect a Note to the records
its content concerns. A Note may link to several object types and several
records of the same type. Store the body once; each associated record displays
the same Note.

| Setting | Value |
| --- | --- |
| Internal name | `note_about` |
| Origin | `note` |
| English label | General |
| Dutch label | Algemeen |
| Reverse list | Notes / Notities |
| Cardinality | Many-to-many; at least one linked subject when saving a local Note |

When this is the only relation in the Notes relation view, relation tabs are
not shown. Multiple relations can be presented as separate tabs. General is
the default relation; add specialised relations only if the setup Q&A selects
the relation-based approach.

Reusable target object types include Candidate, Match, Contact, Company,
Vacancy, Meta Campaign, Meta Ad Set, and Meta Ad. Register only object types
that the destination portal actually adopts; do not create missing objects as a
side effect of installing Notes.

Do not automatically link ancestors or related people. Each `note_about` link
should express a deliberate context. Reuse a compatible native context relation
only after confirming its meaning, target types, and multi-record behaviour.

The inherited `actor` identifies the author. It is separate from ownership and
modification audit and should not be duplicated as a Note-specific property.

## Access and content handling

- Notes are internal by default; do not enable Page or generate public URLs.
- Use the Activities team's least-privilege model and destination record/file
  permissions.
- Multi-line text does not by itself provide rich-text or safe HTML rendering.
- Do not silently overwrite an author's body with AI-generated text.

## Adoption checks

1. Resolve native Activity/Action fields, traits, and Relations in the target
   portal before creating properties.
2. Reuse native equivalents instead of creating duplicate Note fields.
3. Verify backdated/imported Note dates without changing system creation time.
4. Verify author attribution, multi-object linking, duplicate-edge prevention,
   attachments, reverse Notes views, and access enforcement.
5. Read back schema metadata and representative authorised record writes.

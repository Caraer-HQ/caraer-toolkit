---
name: "caraer-cms"
description: "Create, edit, verify, and optionally publish Caraer CMS pages with native-first styling and safe staging workflows."
---

# Caraer CMS

## Purpose

Use this skill for creating, editing, restructuring, verifying, and optionally publishing Caraer CMS webpages in the Caraer portal. Treat local Markdown in `/home/janhein/Codex/caraer` as the content source and the Caraer portal as the live CMS target.

## Scope and portal safety

- Confirm the active portal from the current workspace and `access.md` before any portal call. The Caraer workspace uses the CaraerBV token; never guess between Caraer and a customer portal.
- Read the relevant local source files before editing. Preserve the user's existing content and page structure unless the request explicitly asks for a rewrite.
- Do not delete records. Do not publish or unpublish unless the user explicitly requests it.
- Keep pages in staging while editing and verifying.

## Native-first styling and text-module contract

For every visual, layout, responsive, animation, or CSS change, choose the earliest layer that both owns and can express the requirement:

1. brand and company digital-identity defaults;
2. company-wide default component styling;
3. unique component/module settings and responsive StyleSet fields;
4. generic Main CSS plus a reusable class;
5. page or template CSS plus a scoped class;
6. component Custom CSS only as a documented last resort.

Before writing, record the selected layer and why earlier applicable layers are unsuitable. Do not duplicate the same declaration across layers. Do not manually add a component UUID selector inside Component Custom CSS when the renderer scopes it automatically. If a native field is ignored by the renderer, record that capability gap before using a unique CSS fallback.

Caraer text components are Markdown-only: do not put HTML, inline styles, or class attributes in the text value. Split separately styled blocks into sibling text modules in visual order, put classes in `styling.*.customClass`, and preserve semantic headings and any parent/context classes that still scope the siblings.

After styling writes, read back the exact native/style/CSS fields, confirm later layers do not override them, and visually verify affected desktop, tablet, and mobile breakpoints. Reuse a class/CSS rule only at the generic or page/template layer that owns its scope.

## Standard workflow

### 1. Inspect

1. Identify the source files and intended page slugs.
2. Discover the target object and schema with `object_get`, then find existing records with `record_list`, `record_search`, or `record_get_by_unique`.
3. For an existing page, preserve its UUID, slug, environment, existing metadata, CSS, and publication state unless the request says otherwise.
4. Read the existing webpage with `webpage_get` when the page-read scope is available. If it is unavailable, inspect the page fields through `record_get` or `record_list`.
5. Inspect both `staging_is_published` and `production_is_published` before editing; do not infer publication state from the requested environment or from a previous handoff.

### 2. Convert source content to CMS-native content

Build a CMS PageContent tree:

```
root column
└── section per top-level source chapter
    └── column
        └── text component containing Markdown
```

- Use stable deterministic UUIDs derived from the page slug and section index, so reruns are idempotent.
- Treat `#` and `##` headings as chapter boundaries; keep deeper headings inside the chapter's Markdown text unless the user requests deeper nesting.
- Put the chapter heading and all chapter body content in the text component.
- Keep the source Markdown; do not replace text components with HTML blobs.
- Use empty compatibility styling buckets (`all`, `mobile`, `tablet`, `desktop`) and follow the native-first styling contract below; put visual CSS in `customCss` on the relevant node only when it is the documented last resort.
- Preserve Markdown links, lists, emphasis, email links, and escaped heading punctuation.
- Remove Markdown horizontal rules or divider nodes when the requested design is continuous text.
- For a single-column layout, use one section containing one column and place all text elements sequentially in that column.
- Add a short excerpt and use a URL-safe unique staging slug.

### 3. Write

- Prefer `webpage_upsert` for existing and new Page-trait records.
- For new pages, provide `objectName`, `record.properties`, and `createRecordIfMissing=true`; use the environment-specific title and slug fields when creating a nonstandard Page object such as `terms`.
- For bulk idempotent work, use `record_create_or_update` keyed by the object's unique staging slug.
- If `webpage_upsert` is blocked by a missing page-write scope but record write access exists, use `record_update` or `record_create_or_update` with `staging_content` as a JSON string. Include all required production and staging title/slug fields when the backend validates both environments. Record this fallback in the handoff.
- Never set published flags accidentally. Staging content is the default target.
- Treat staging and production content as separate fields/environments; updating staging content does not automatically update production content.

### 4. Verify

After every write:

1. Read back the record.
2. Parse the content JSON.
3. Check that the root is a column, every requested section/column relationship is correct, and every text component contains non-empty Markdown.
4. Check title, slug, excerpt, link preservation, section count, content byte size, and absence of unwanted divider lines.
5. Re-check both environment publication flags and confirm which environment changed.
6. When page-read scope is available, run `webpage_html_snapshot` with `fetchWerkenBij=true` and `includeDesignAudit=true`, or run `webpage_design_audit`. Fix empty-render or structural errors before publication.
7. For bulk updates, report a manifest containing source file, record UUID, slug, section count, and verification status.

### 5. Publish only on request

Before publishing, verify staging again and run the design audit. Use `webpage_publish` only after explicit user approval. Report the production URL and whether the publish succeeded. If the user asks only to create or fill pages, leave them unpublished.

- If the native publish tool is blocked by missing page-read/page-write/publish scopes, but the user explicitly authorized publication and record-level production writes are available, copy the verified `staging_content` JSON string to `production_content` with `record_update`. Include required production and staging title/slug fields, preserve publication flags, and verify the production tree afterward. Clearly report that this record-level fallback was used and that native publish/audit scopes are still missing.

## Bulk-edit conventions

- Make the source file the content authority; rerun the conversion rather than hand-editing generated CMS JSON.
- Use a deterministic file-to-slug mapping and check for collisions before writing.
- Start with one existing record as a canary, verify it, then process the remaining pages.
- Avoid overwriting custom CSS, metadata, images, or existing page settings when only text content is requested.
- On partial failure, stop and report successful and failed records; reruns must safely update only the intended slugs.

## Maintenance and learning loop

- Treat every CMS editing task as feedback for this skill.
- After a task, record reusable discoveries such as API behavior, schema quirks, rendering requirements, permission gaps, reliable tool sequences, and failure recovery.
- Update this skill proposal with a concise rule or example when a lesson is likely to recur; do not add one-off customer content or secrets.
- Prefer general fixes that improve future CMS work, such as better idempotency, validation, source parsing, or publish safety.
- Keep a short changelog in the skill's proposal history through Skill Workshop revisions. Re-read the current proposal before revising it so existing guidance is preserved.
- When a pattern is uncertain, capture it as a verification step or known limitation instead of presenting it as a guaranteed rule.

## Common failure handling

- Missing `records.<object>.page-read` or `page-write` scopes: report the exact missing scope; use record-level read/write only when supported, and do not claim HTML snapshot or design-audit verification if those tools are unavailable.
- Missing `records.<object>.publish` scope: use the explicit-approval record-level production-content fallback only when record-level writes are available; verify production afterward and report the limitation.
- Invalid structure JSON: pass `staging_content` as a serialized JSON string for record-level writes.
- Required production fields on an update: include the existing production title and slug along with staging fields.
- Duplicate slug: stop and inspect the existing record instead of creating a second page.
- Publish/audit failure: keep the page in staging, report the error, and do not bypass the audit without explicit approval.

---
name: "caraer-object-schema"
description: "Design, audit, and maintain the reusable Caraer Object Templates Toolkit, then selectively apply templates to individual Caraer portals."
---

# Caraer Object Templates Toolkit

Use this skill to maintain the reusable toolkit at `/home/janhein/Codex/caraer/caraer-toolkit/public/object-templates/`, or to choose and adapt its patterns for one identified Caraer portal.

The toolkit is a cross-portal catalogue of best-practice object, property, relation, and trait patterns. It is not a prescribed Caraer Main schema and it does not create a requirement that every portal use every template.

## Library principles

- Treat each template as an independent, composable module. Select only the objects, traits, properties, and relations that the portal needs.
- Keep reusable patterns generic: no customer records, branding, credentials, or customer-specific overrides belong in the central toolkit.
- Keep a portal’s selected templates, implementation decisions, and approved overrides in that portal’s workspace.
- Prefer the smallest stable object model that preserves ownership, reporting, and integration needs.
- Preserve provider field names and values where the template imports external data; document any normalization or aliases.
- Use a Relation for an independently identifiable record; do not use Relations to simulate extension ownership.

## Common ownership patterns

Use these patterns when they fit the portal; they are guidance, not mandatory toolkit-wide objects.

- `Contact`: person identity, contact channels, platforms, and person-level employment details such as `job_title`.
- Contact extensions: `Lead` for marketing, `Qualified Lead` for sales qualification, `Customer` for contract/onboarding/support, and `Alumni` for former-relationship context.
- `Company`: relationship anchor. Avoid a central customer-specific property set.
- Company extensions: `Target` and `Account` where appropriate.
- Keep company association and role-at-company metadata in Relations such as `works_at`; do not copy company fields onto Contact without a defined reason.

## Workflow

1. Identify the target portal and whether the work concerns a primary object, extension, property, trait, relation, or provider-import template.
2. Check the toolkit for the smallest applicable template set; preserve existing user changes.
3. Check the live target portal as a naming and behaviour reference when access is available.
4. Decide what the portal adopts, excludes, or overrides. Keep the choice and rationale in that portal’s workspace, not in the central template.
5. Assign every property to the narrowest correct owner and document object hierarchy, relations, traits, type, format, options, and provider mappings in the selected template.
6. Keep every object template’s `## Traits` section non-empty, covering enabled, optional, and excluded traits.
7. Audit the selected templates and report differences between the toolkit and the live portal; never silently rewrite live data.
8. After an authorized live write, verify the persisted response and update the portal documentation.

## Shared-property reuse and change approval

Before creating, attaching, or updating a property, look up its existing portal-wide definition by key; absence from the target object does not mean the property is new.

1. Compare the proposed and existing definitions: type/format, label, required/default/validation settings, option names/values, labels, colours, icons, disabled flags, and other settings. If nothing changes, reuse or attach within the authorized task without additional approval.
2. If anything changes, enumerate every object already using the shared property before any write, including a create/attach call that could update its definition. If usage cannot be fully established, report the gap and keep the change pending.
3. Show affected objects and an exact current → proposed change table. Explain the impact on those objects and existing values, especially required-field changes and renamed/removed options. Obtain explicit approval for that concrete shared change; general template-application approval does not authorize undisclosed cross-object effects.
4. Apply only approved differences and preserve unrelated settings and values. Without approval, leave the shared definition unchanged; propose a separate namespaced property when different semantics are needed.
5. Read back the definition and verify settings/attachments across affected objects; record the approved change in the portal workspace.

## Property types, formats, and UI handoff

- Treat `type` and `format` separately. A `string` property can use formats such as `single-line` or `multi-line`.
- The MCP `property_update` contract documents type and format as immutable after creation. Do not assume MCP can switch formats.
- For a format change within the same type, guide the user in the Caraer UI: **Objecten → [object] → Properties → [property] → Format → [desired format]**.
- Explain: “Type bepaalt welk soort data de property opslaat, bijvoorbeeld `string` voor tekst. Format bepaalt hoe die tekst wordt ingevoerd of weergegeven, bijvoorbeeld `single-line` of `multi-line`.”
- Do not create a duplicate replacement merely because MCP cannot change a format without approval; duplicates can fragment existing records and downstream mappings.
- After a UI change, re-read the live property and affected forms/templates. Verify that the name and type stayed the same and only the intended format changed.
- If the UI changes the underlying type or cannot switch the format, stop and propose a migration.

## Safety

- Ask before mutating live schema, relations, permissions, or publishing changes.
- Do not create inverse extensions merely because an API does not support the intended direction.
- Keep customer-specific properties and data out of the central toolkit.

---
name: "caraer-cms-components"
description: "Create, find, inspect, update, and reuse Caraer CMS components/modules; verify their tree and placement before publishing."
---

# Caraer CMS Components

Use this skill for reusable CMS components, modules, saved sections, headers, hero blocks, and component-library operations. Treat a page-content node and a reusable module as different targets: a page node belongs to a webpage tree; a module is discoverable through the modules API and can be reused across pages.

## Workflow

### 1. Establish the target

1. Identify the organization, site, environment, component/module name, and requested operation (list, inspect, create, update, reuse, or delete). Confirm the active Caraer portal and available authorization before calling the API; completion means the target and scope are explicit.
2. Read the relevant page or module before changing it. Preserve the existing UUIDs, child order, settings, responsive StyleSet values, custom classes, and custom CSS unless the request changes them; completion means the current tree is recorded as the baseline.
3. Decide whether the request targets page content or the reusable module library. Do not infer library membership from a page node's `scope` or `moduleKind`; completion means the target is identified from its owning endpoint.

### 2. Discover reusable modules

1. List company modules with `POST /api/v2/modules/index` or personal modules with `POST /api/v2/modules/personal/index`. Send pagination fields such as `{"page":1,"limit":100}`; completion means the response is parsed for module UUID, name, label, category, scope, module kind, and child count.
2. Fetch a selected module with `GET /api/v2/modules/{moduleId}` or the corresponding personal endpoint; completion means the full reusable content tree is available before reuse or update.
3. If native module tools are unavailable, use the documented Caraer API through the configured authenticated route. Keep bearer credentials out of prompts, files, URLs, logs, and output; completion means the API response is obtained without exposing the credential.

### 3. Create or update a component

1. Build the module from the smallest complete reusable subtree. Keep its root and descendants structurally valid, retain native component settings, and remove page-specific references that would make reuse unsafe; completion means the tree is self-contained and has a stable name/slug.
2. For a new company module, use the documented company-module create endpoint `POST /api/v2/modules/`; for a personal module use the personal create endpoint. For an existing company module, read first and update with `PUT /api/v2/modules/{moduleId}`; use the personal equivalent for personal scope. Completion means the API acknowledges the intended module and scope.
3. When adapting a saved module for a page, copy or reference the module according to the CMS operation supported by the active connector. Do not overwrite page content until the destination and merge/replace behavior are explicit; completion means the destination page tree is changed only in the requested location.

### 4. Verify persistence and rendering

1. Re-list or re-fetch the module after every write and compare the name, scope, root, child UUIDs/order, settings, StyleSet values, classes, and custom CSS with the intended result; completion means the persisted module matches.
2. If the module was placed on a page, read the page back and verify the exact parent/child relationship and absence of duplicated or empty nodes; completion means placement is confirmed in the requested environment.
3. Use the CMS HTML snapshot or design audit when available to verify rendered output and layout across relevant breakpoints. Record audit errors as findings; completion means the result is either clean or the remaining limitations are reported.

### 5. Publish only on explicit request

Keep component and page changes in staging while editing and verifying. Publish only after the user explicitly requests it, then report the production URL/state and whether the published module placement was verified. If audit or publish scopes are missing, report the exact limitation and do not silently bypass it.

## Safety and recovery

- Never create a second module when a matching name/slug already exists; inspect and update the existing target instead.
- Never delete a module or replace a page subtree without explicit confirmation of the exact target and scope.
- If a request to update a module fails, leave the existing module unchanged when the API supports atomic failure, re-fetch it, and report the error and current persisted state.
- A successful page save does not prove that a reusable module was created; verify through the modules index/detail endpoint.

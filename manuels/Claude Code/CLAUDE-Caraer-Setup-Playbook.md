# Caraer × Claude — Assistant Playbook (2026-v1)

This document is meant to be **fed to Claude** (pasted into a chat, added as a project/skill file, or included in a CLAUDE.md) so it can guide any user through connecting their Caraer account to Claude — on whatever surface they use, including chat-only users without the CLI.

---

## 1. Facts you need (the knowledge base)

| Fact | Value |
|---|---|
| Integration type | Remote MCP server (streamable HTTP) |
| Endpoint | `https://v2.api.caraer.com/api/v2/mcp` |
| Authentication | OAuth in the browser: Caraer login → **Select a company** → **Choose a private app** |
| "Select a company" screen | Dropdown of the user's companies + Continue button — the connection is scoped to one company |
| "Choose a private app" screen | Radio: pick an existing OAuth private app, or **Create a new private app** with a free-text Label (suggest: `Claude Code` or `Claude`) + Continue |
| What Caraer is | Recruitment platform: vacancies, campaigns, candidate journeys (caraer.com) |
| Entry-point tool | `schema_help` — explains Caraer's Object / Property / Relation / Record model; call it first in a new working session |
| CLI config location | User scope in `~/.claude.json` under `mcpServers.<name>` |
| Naming default | **Always `caraer-<portalname>`** (e.g. `caraer-gartenlux`) — a Caraer account can span multiple portals (like HubSpot), and each connection is bound to one. The name itself is only a label: the "Select a company" OAuth choice is what actually binds the portal, so it must match the name. One connection per portal, all on the same URL |
| Claude Code install (Windows) | `irm https://claude.ai/install.ps1 | iex`, then open a **new** PowerShell window |
| Known Windows pitfall | Installer may put `claude.exe` in `%USERPROFILE%\.local\bin` without adding it to PATH → "claude is not recognized" |

## 1b. What the connection gives you (verified against the live server, 2026-09-04)

The caraer MCP server exposes ~75 tools (prefixed `mcp__caraer__`), in these groups:

- **Schema**: `object_*`, `property_*`, `relation_*`, `trait_*` — create and manage record types, their fields, relations between types, and traits (e.g. the Page trait). Helper tools list valid property types, formats, and value shapes.
- **Records**: `record_create/update/delete/restore`, `record_bulk_edit`, `record_get(_by_unique)`, `record_list` (filters/sort/pagination), `record_search` (free text), and `record_query` — a graph-aware query tool preferred for multi-hop, semantic, fit, and temporal questions. `record_*_relation` tools manage edges between records. Schema/example helpers: `record_filter_examples`, `record_filter_operators_list`, `record_query_schema`, `record_pagination_schema`.
- **Forms**: `form_create/get/index/update` — form layouts on objects (grids, fields, one submit button).
- **Previews**: `preview_*` — preview layout schemas for objects.
- **Webpages / CMS**: `webpage_*` — full CMS: get/upsert pages on records with a Page trait, targeted node edits of the PageContent tree, image upload, HTML snapshots, a design audit, templates, publish/unpublish (staging → production).
- **Company**: `company_digital_identity_get/update` (brand colors, typography), `company_website_settings_get/update` (domain, header, footer).
- **Access**: `access_scopes_get` — the caller's granted scopes for the selected company; useful when a tool call is denied.

Everything is scoped to the **company chosen during OAuth**. Publishing tools (`webpage_publish`, `*_update` on live settings) change production — confirm with the user before using them.

## 2. First, ask the user two questions

1. **Where do you use Claude?** — claude.ai in the browser / Claude Desktop chat / Claude Code (terminal or Code tab).
2. **Do you have your Caraer login ready?** (e-mail + password for caraer.com — the user types these in Caraer's own browser page, never in chat).

Then pick ONE path below. Give the user one step at a time and wait for confirmation before the next.

## 3. Path A — No CLI: claude.ai or Claude Desktop (chat only)

Remote MCP servers can be added as a **custom connector** — no terminal needed.

1. Open **Settings → Connectors** (on claude.ai: profile menu → Settings → Connectors; in the desktop app: Settings → Connectors).
2. Scroll down, click **Add custom connector**.
3. Name: `Caraer — <portalname>` (e.g. `Caraer — GartenLux`) — URL: `https://v2.api.caraer.com/api/v2/mcp` → **Add**.
4. Click **Connect** on the new Caraer connector. The browser opens Caraer's login: log in → **Select a company** → **Create a new private app** (label e.g. `Claude`) → Continue.
5. Back in a chat: open the search-and-tools (sliders) menu and make sure Caraer is enabled, then test with e.g. *"List my Caraer vacancies."*

Notes:
- Custom connectors require a paid Claude plan; on Team/Enterprise an admin may need to add it for the organization.
- If "Add custom connector" is missing, the plan/role doesn't allow it → fall back to Path B, or ask the org admin.

## 4. Path B — Claude Code CLI (terminal)

1. Check install: `claude --version`. If not installed or "not recognized" → section 6 first.
2. Add the server (once per machine, per portal) — always named `caraer-<portalname>`:
   ```
   claude mcp add --transport http caraer-<portalname> https://v2.api.caraer.com/api/v2/mcp
   ```
3. Authenticate: run `claude`, then `/mcp`, select the **caraer-<portalname>** entry → browser opens → Caraer login → **Select a company matching the portal name** → Create a new private app (Label matching the name, e.g. `Claude Code — GartenLux`) → Continue.
4. Verify: `/mcp` shows the connection as **connected**.

Extra portals: repeat steps 2–3 with each portal's name (same URL). Tools then arrive prefixed per portal (`mcp__caraer-<portalname>__…`), so it is always unambiguous which portal a call targets. There is no rename: to fix a name, `claude mcp remove <name>`, re-add, re-authenticate.

## 5. Path C — Claude Code desktop app (Code tab)

The Code tab shares `~/.claude.json` with the CLI, but a **running session cannot authenticate or pick up new MCP auth**. Guide:

1. Do Path B in a terminal (add + `/mcp` login).
2. Start a **new** session in the app — the Caraer tools load automatically.
- If the app session says the server "requires authentication", that's expected until steps 1–2 are done and a fresh session is started.

## 6. Windows install + PATH fix (for Path B/C)

1. `irm https://claude.ai/install.ps1 | iex` in PowerShell; wait for it to finish.
2. Close PowerShell, open a new window, `claude --version`.
3. If "claude is not recognized":
   ```powershell
   [Environment]::SetEnvironmentVariable('Path', "$env:USERPROFILE\.local\bin;" + [Environment]::GetEnvironmentVariable('Path','User'), 'User')
   ```
   then again: new window → `claude --version`.

## 7. Troubleshooting quick reference

| Symptom | Cause → fix |
|---|---|
| `claude` not recognized after install | PATH missing `~\.local\bin` → section 6 step 3 |
| caraer-… not in `/mcp` list | Server never added → section 4 step 2 |
| "requires authentication" in a running session | Sessions don't hot-reload auth → finish `/mcp` login, start a new session |
| OAuth page shows no companies | User's Caraer account has no company access → check with Caraer admin |
| Wrong company connected | Re-run `/mcp` → caraer → re-authenticate and pick the right company (or reconnect the custom connector) |
| Connection name doesn't match the portal it's authenticated to | The name is just a label — `claude mcp remove <name>`, re-add under the right name, re-authenticate |
| Existing private app vs. new | Reusing an existing OAuth private app is fine; create a new one when in doubt |

## 8. How to behave while guiding

- One step per message; wait for the user's confirmation or screenshot before continuing.
- Never ask for or handle the user's Caraer password — they enter it only on caraer.com's own page.
- On errors, ask for a screenshot of the exact window (PowerShell or browser).
- Close by verifying: connector shows **connected** (CLI: `claude mcp list` prints `caraer-<portalname>: … - √ Connected`), and a test prompt returns data — good first prompts: *"Call Caraer's schema_help tool and summarize my data model"* or *"List my Caraer objects."*

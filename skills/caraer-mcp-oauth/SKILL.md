---
name: "caraer-mcp-oauth"
description: "Guide reliable Caraer OAuth + PKCE customer MCP setup from app creation through token exchange, secure config, consent, and validation."
---

# Caraer MCP OAuth

## Identify the target portal first

1. If the current workspace unambiguously identifies a portal, state that portal and ask the user to confirm it. Otherwise ask: **“Which Caraer customer or portal should I connect?”**
2. Wait for a customer or portal name. Never search accounts, guess from a company list, or start OAuth until the user confirms the target.
3. Normalize the confirmed name to a lowercase slug and create or use exactly one connection named `caraer-<portalname>`.
4. Read the target portal's `access.md`. If no customer workspace exists, ask for confirmation before creating one or follow the customer-onboarding workflow when applicable.
5. Complete this phase only when the user-confirmed portal, connection name, endpoint, credential source, and authentication path are known.

## Choose the connection path

Use the same ordered workflow for Claude and Codex. Use the client adapter only to open the MCP connection or OAuth browser; do not change the confirmed portal, app approval, credential handling, scope review, refresh, or validation.

- Claude: add a custom remote MCP connector named `Caraer — <portalname>` (or the host client's equivalent) using `https://v2.api.caraer.com/api/v2/mcp`; start Connect and use the browser flow when Claude opens it.
- Codex: configure the same remote endpoint for the server named `caraer-<portalname>` and start the configured OAuth flow when Codex offers it.
- In either client, start a fresh session after successful connection if authentication does not hot-reload.
- Installed Caraer App provider: use app-installation endpoints only with a confirmed `appUuid`; never assume it is an OAuth `client_id`.

## Discover and isolate

1. Inspect the confirmed portal's configuration and credential presence without printing values.
2. Before a new integration, GET `https://v2.api.caraer.com/.well-known/oauth-authorization-server`; require authorization-code, refresh-token, `code`, and PKCE `S256` support.
3. The company selected during OAuth must match the user-confirmed portal.
4. Complete this step only when endpoint, portal, credential source, and authentication path are confirmed.

## Browser-mediated OAuth

1. Add a custom remote MCP connector named `Caraer — <portalname>` (or the host client's equivalent) with the MCP endpoint.
2. Start Connect after the target portal and OAuth endpoints are confirmed, then let Caraer open its own browser pages. The operator enters login and MFA only there.
3. On **Select a company**, choose the company matching the target portal and continue.
4. On **Choose a private app**, select an existing OAuth private app or create one with a factual label such as `MCP — <portalname>`; do not enter secrets in chat.
5. Before the user clicks **Allow**, show the selected permissions, distinguish read, write, delete, and admin access, and obtain approval for that exact set.
6. Wait for the client to report a successful callback and durable credential registration—not merely for a browser success page. Start a fresh client session if it does not hot-reload MCP authentication.
7. Complete this step only when the connection is shown as connected and the company choice matches the target portal.

## Exchange and store

1. Exchange the code at `https://v2.api.caraer.com/oauth/token` with a browser-like HTTP client, `grant_type=authorization_code`, exact redirect URI, client ID, and verifier.
2. Treat HTTP 200 containing access and refresh tokens as success. If Cloudflare returns Error 1010/browser_signature_banned, start a fresh transaction and use the browser-like client; never retry the same code.
3. Store only in the untracked customer credential file with mode 0600: `CARAER_PORTAL_<SLUG>_OAUTH_CLIENT_ID`, `..._OAUTH_ACCESS_TOKEN`, and `..._OAUTH_REFRESH_TOKEN`.
4. Configure the customer MCP server to use the OAuth access-token variable. Preserve the legacy API key until OAuth validation succeeds and the operator approves retirement.
5. For client-managed OAuth, verify the MCP credential store now contains an entry for `caraer-<portalname>` without displaying credential values. If the callback completed but the current session does not expose the connection, start a fresh client session and re-check registration before retrying OAuth.
6. Complete this step only when credentials are stored atomically, protected, registered against the confirmed portal, and no secret appeared in logs, chat, tracked files, or screenshots.

## Every customer MCP session

1. Load the untracked OAuth environment file. Decode a JWT locally without logging it; use it if its `exp` is more than five minutes away.
2. If opaque, undecodable, expired, or within five minutes of expiry, follow refresh rules. On MCP 401, refresh once and retry the original request; do not loop.
3. Refresh at `https://v2.api.caraer.com/oauth/token` using refresh token and confirmed client ID; atomically replace rotated credentials and retain mode 0600.
4. Complete this step only when the request uses the exact customer credential and no credential value is exposed.

## Validate and report

1. Run read-only MCP `initialize`, then `tools/list`; require HTTP 200, JSON-RPC results, and a non-empty tool list.
2. Run one small read-only schema/object query, preferably `schema_help` first in a new working session or `object_list` with a small limit.
3. Report only target, timestamp, status, tool count, non-sensitive tool names, and non-secret errors. Do not infer scopes, plan, business-data, task, or meter access from `tools/list`.
4. Report **Succeeded** only after exchange plus all validations pass; otherwise report **Blocked** or **Failed**, the exact non-secret blocker, whether credentials were stored, and whether portal data changed.
5. After OAuth validation, compare local templates with the live schema and request explicit approval before schema mutations or production publishing.

## Installed-App provider OAuth

1. With the confirmed customer bearer credential, GET `/api/v2/apps/{appUuid}/installation/connections`.
2. Use returned `data.name` as provider identifier, not display-only `data.label`.
3. POST `/api/v2/apps/{appUuid}/installation/oauth/{provider}/start`, re-read connections, and require `connected: true`.

## Security

Never log, chat, commit, screenshot, or store in tracked files passwords, MFA codes, client secrets, authorization codes, access tokens, refresh tokens, PKCE verifiers, or state values. Never reuse another customer's credential or portal. Never revoke or retire legacy credentials automatically.

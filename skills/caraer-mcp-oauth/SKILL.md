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

1. Identify the client or host currently in use before configuring or opening OAuth. The supported choices are OpenClaw, Hermes or a comparable agent host, Codex, Claude, Cursor, or another client explicitly confirmed by the operator. Use the selected client's native MCP connector, callback listener, credential store, and login action; do not substitute another client's CLI or callback flow.
2. Configure Caraer MCP with the streamable HTTP transport in every client. Do not select SSE for `https://v2.api.caraer.com/api/v2/mcp`.
3. When OpenClaw, Hermes, or a comparable agent host is in use, ask which runtime/client should perform the MCP connection—its native runtime, Codex, or another supported client—because these hosts can run more than one. Continue only after that preference is clear. Do not start a Codex CLI OAuth flow merely because the task is running inside an agent host.
4. OpenClaw, Hermes, or comparable agent host: configure the confirmed remote MCP server in the selected host, scoped to the confirmed agent, with streamable HTTP, and use that host's own OAuth action when its native runtime is selected.
5. Codex: configure the same remote endpoint with streamable HTTP for the server named `caraer-<portalname>` and start the configured OAuth flow when Codex is the selected runtime.
6. Claude: add a custom remote MCP connector named `Caraer — <portalname>` (or the host client's equivalent) using `https://v2.api.caraer.com/api/v2/mcp` over streamable HTTP; start Connect and use the browser flow when Claude is the selected runtime.
7. Cursor: configure the same remote endpoint in Cursor over streamable HTTP and start Cursor's native OAuth flow when Cursor is the selected runtime.
8. Record the selected client/runtime and streamable HTTP transport in validation. Start a fresh session after successful connection if authentication does not hot-reload.
9. Installed Caraer App provider: use app-installation endpoints only with a confirmed `appUuid`; never assume it is an OAuth `client_id`.

## Discover and isolate

1. Inspect the confirmed portal's configuration and credential presence without printing values.
2. Before a new integration, GET `https://v2.api.caraer.com/.well-known/oauth-authorization-server`; require authorization-code, refresh-token, `code`, and PKCE `S256` support.
3. The company selected during OAuth must match the user-confirmed portal.
4. Complete this step only when endpoint, portal, credential source, and authentication path are confirmed.

## Browser-mediated OAuth

1. Add a custom remote MCP connector named `Caraer — <portalname>` (or the host client's equivalent) with the MCP endpoint, then start its OAuth transaction so the **current client's** callback listener is running.
2. Before opening or sending an authorization URL, check whether the browser completing OAuth runs on the same host as that listener. If it does not, establish a callback route first—for example, a user-managed SSH/Tailscale port forward from the browser's localhost port to the client's host localhost port—and verify the route reaches the listener. Do not open the authorization page or begin consent until this check passes.
3. Only after the callback listener and route are verified, prefer opening the authorization page in a user-accessible browser on the client host. Tell the user: “I’ve opened the OAuth page in the browser. You can complete the connection yourself with these steps.” Never enter credentials, MFA codes, authorization codes, or the final consent action for the user.
4. The authorization URL may include the client's configured/default scopes. Do not add, infer, or alter scopes yourself. The user must still be able to review and change the selection in the Caraer consent flow, including choosing **Enable all scopes** or only specific scopes. Do not instruct the user to configure scopes manually in Settings or in the private-app configuration. Give this exact guidance:
   1. Log in via Google, Microsoft, or your email credentials.
   2. Select the company you want to connect from the dropdown list. It must be the confirmed target portal.
   3. Select your private app, or create one with a name such as `MCP — <your name>`.
   4. Enable all scopes, or only the specific scopes you want to grant access to, in the consent flow.
   5. Review the selected permissions and click **Allow** / **Done** to finish.
5. Do not modify the selected scope set. If the user asks for help deciding, explain the scope categories and let them choose; do not approve, consent to, or alter permissions on their behalf.
6. If an authorization URL must be sent to the user's browser, send the exact URL generated by the OAuth client only through the private conversation. Never add, remove, reorder, or edit its `scope`, `state`, `code_challenge`, redirect URI, or other parameters. A URL with client-provided scopes is valid; the user chooses whether to keep, change, or expand them in the consent flow.
7. Wait for the client to report a successful callback and durable credential registration—not merely for a browser success page. Start a fresh client session if it does not hot-reload MCP authentication.
8. Complete this step only when the connection is shown as connected and the company choice matches the target portal.

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

1. Confirm the configured transport is streamable HTTP, then run read-only MCP `initialize` and `tools/list`; require HTTP 200, JSON-RPC results, and a non-empty tool list.
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

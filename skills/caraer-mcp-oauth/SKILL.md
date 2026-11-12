---
name: "caraer-mcp-oauth"
description: "Guide Caraer MCP setup across AI clients with native authentication, clear approval, browser/link handoff, verified connection, and optional developer/CLI onboarding."
---

# Caraer MCP OAuth

## Guided setup: start here

Guide the user through the connection; do not present a technical runtime questionnaire or leave them with unexplained Settings instructions.

Connecting an MCP does **not** imply the user is a developer. Complete and verify company access first; CLI installation is not a prerequisite. After success, follow **Finish onboarding: choose the next path** below. Apply this separation in every supported AI client, not only OpenClaw.

### Universal guidance for every MCP client

These user-guidance rules apply to every MCP/AI client, not just OpenClaw. This skill's endpoint, company selection, private-app instructions, and schema checks are Caraer-specific; do not apply those details to an unrelated MCP service.

1. Identify the intended service/account and AI client from the request and context. Recommend that client's **native connector and authentication**. If the client is ambiguous (for example, Claude web versus Claude Code, or a host with several runtimes), ask only the missing distinction; do not choose a different runtime just because its tools are available.
2. Give one plain-language explanation and approval question: **“Shall I connect <service/account> to <client> using its native connection? <Explain who can use this authorization.> I’ll start the login and open the authorization page when supported; you review and approve access.”** For OpenClaw, use the native + shared wording below. Reuse approval already given; do not repeat it at every technical step.
3. Inspect the selected client's installed capabilities/help or official documentation before giving exact commands or UI paths. Native OAuth support, account-sharing options, callback mechanisms, and settings labels vary by client and version. Do not assume that another client has OpenClaw's `shared`/`per-requester` settings or its Settings path.
4. Determine the service's actual transport and authentication. For OAuth, start the client's native transaction, then open its generated authorization link in a user-accessible browser whenever possible; otherwise share the exact generated link privately with a supported callback route. For device authorization, open the client-generated verification page and privately provide its short-lived code. For API-key/token authentication, use the client's supported masked entry or secret store, not an invented OAuth flow. For unauthenticated servers, explain that there is no login page to open. For local stdio servers, check the server’s documented credential requirements; stdio itself does not determine whether login is needed. Do not force OAuth, HTTP, or browser consent onto every MCP server.
5. Do the supported setup yourself. If user interaction is necessary, give the exact next action for **that client**, explain what the user should see, and remain available through completion. A settings page is a fallback entry point, not an authorization link; label it honestly.
6. Verify the connection inside the intended client with a small read-only capability check. A browser success page, saved config, or successful connection in a different AI client is not enough. Report what was verified and any exact remaining blocker, without generalizing one failed invocation into a platform-wide restriction.

### OpenClaw default

- In OpenClaw, recommend **OpenClaw native + shared OAuth** by default. Native means OpenClaw manages the connection, callback, and credentials; shared means the connection uses the operator's authorization rather than a separate login for each sender. Shared does not mean public: normal agent/tool access restrictions still apply.
- Ask one direct confirmation question, combining the target and setup choice: **“Shall I connect <portal> using OpenClaw native + shared OAuth? OpenClaw will manage the login and credentials, and permitted users of this connection will use your authorization. I’ll open the authorization page; you choose the company and permissions and approve access.”** If the portal is unknown, ask which portal in this same question. Wait for approval before configuring or starting OAuth. Existing explicit approval for this target and mode counts; do not ask again.
- Offer other runtimes or per-requester login only when requested or when the intended use requires separate sender identities. Do not silently replace an existing connection's identity mode.
- After approval, do the technical setup yourself where supported. Keep updates short and distinguish **configured**, **awaiting your consent**, and **verified connected**.
- Always open a user-accessible browser when possible and start the selected client's native OAuth flow. Open its exact generated authorization link directly; do not use screenshots to hunt for a URL. If direct opening is unavailable, share that exact generated link privately. Never invent an authorization URL or claim a flow started before the client starts it.
- If no auth link can be generated through the available paths in OpenClaw, guide the user through **Settings → MCP → <connection> → Connect**, opening that page when possible. Clearly say this opens Settings, not an active authorization flow. Explain the next action, then continue with consent guidance and verification. For other clients, use their verified native connect entry point instead. Do not send the user back through setup if they already completed it.

## Identify the target portal first

1. Use the combined target/client confirmation above for every client, with the OpenClaw-specific wording only in OpenClaw. If the target is unknown, ask which Caraer customer or portal to connect within that question. Do not repeat a confirmation already given.
2. Wait for a customer or portal name. Never search accounts, guess from a company list, or start OAuth until the user confirms the target.
3. Normalize the confirmed name to a lowercase slug and create or use exactly one connection named `caraer-<portalname>`.
4. Read the target portal's `access.md`. If no customer workspace exists, ask for confirmation before creating one or follow the customer-onboarding workflow when applicable.
5. Complete this phase only when the user-confirmed portal, connection name, endpoint, credential source, and authentication path are known.

## Fast preflight

1. Keep discovery target-specific. Read the confirmed portal's `access.md` and inspect only the named connection; do not list accounts, enumerate all MCP servers, or read an entire host configuration.
2. For OpenClaw native runtime, inspect `mcp.servers.caraer-<portalname>` directly. Treat a legacy Codex connection name in local access notes as evidence only; do not reuse it for the OpenClaw connection.
3. Fetch the authorization-server metadata once and report only whether it advertises authorization-code, refresh-token, `code`, and PKCE `S256`. Do not print the scopes catalog or unrelated metadata.
4. For every client, check whether a user-accessible browser can be opened and which callback mechanism the client uses. Prefer a compatible browser for consent; otherwise use the client's supported remote callback route and private-link handoff. Browser availability alone does not verify a callback route; do not declare OAuth unavailable merely because one browser tool fails.
5. Consult the OpenClaw configuration schema only if a targeted configuration read or write fails validation. Complete preflight when the endpoint, transport, target-specific connection status, metadata capabilities, and browser-route status are known.

## Choose the connection path

1. Identify the client or host currently in use before configuring or opening OAuth. The supported choices are OpenClaw, Hermes or a comparable agent host, Codex, Claude, Cursor, or another client explicitly confirmed by the operator. Use the selected client's native MCP connector, callback listener, credential store, and login action; do not substitute another client's CLI or callback flow.
2. Configure Caraer MCP with the streamable HTTP transport in every client. Do not select SSE for `https://v2.api.caraer.com/api/v2/mcp`.
3. In OpenClaw, use the approved native + shared default above, unless the user selected another path. For Hermes or comparable hosts, establish the intended native client before proceeding. Do not start a Codex CLI OAuth flow merely because this agent runs on Codex.
4. Configure the confirmed server in the selected host with streamable HTTP and the intended agent access. Use that host's own OAuth action. In OpenClaw, `shared` uses the operator's authorization; `per-requester` requires each sender's own connect flow.
   - **OpenClaw chat-driven configuration:** hand off the exact server definition to the central OpenClaw system-setup tool, requesting live `config.set` at `mcp.servers.<name>`. This route has successfully configured a server without restarting the Gateway even when `openclaw mcp add` refused live state ownership. Include `url`, `transport: streamable-http`, `auth: oauth`, and `oauth.identity: shared` or the confirmed alternative. A parent tool exposing only config reads does not imply the central handler cannot write; a generic failed handoff is not evidence that its live `config.set` path is unavailable. Verify the exact persisted entry with a targeted config read. Configuration is not OAuth authorization; initiate native login separately.
   - **Other OpenClaw configuration paths:** Control UI **Settings → MCP** writes through the Gateway; the composer’s **+ → Plugins → Add MCP server…** is another supported path. The `openclaw mcp add <name> ...` CLI is supported too, but depending on the environment it may require exclusive offline state ownership rather than writing through the live Gateway. Use `openclaw mcp status --verbose` / `openclaw mcp doctor <name>` to inspect and `openclaw mcp login <name>` for shared OAuth. MCP configuration supports Gateway hot reload; do not stop/restart the Gateway as a routine prerequisite and do not edit its config file directly to work around a rejected write.
   - **CLI refusal is not a platform limitation:** if add/login reports exclusive offline state ownership, report only that this invocation failed. Use the central OpenClaw setup handler or Settings instead; do not make stopping the Gateway the next routine step. Discover the current native login capabilities or hand off their discovery to the central handler before claiming an action is unavailable. Do not infer that chat OAuth is unsupported, administrator-browser-only, or broken from missing parent tools or a failed CLI command. Record only the exact observed error and affected invocation; leave general product documentation unchanged unless verified against the installed implementation or authoritative documentation.
   - For OAuth-protected servers, if the add command cannot probe before credentials exist, use its documented no-probe/save option (or Settings → MCP), then run `openclaw mcp login <name>` and verify with doctor/status. Do not bypass the selected host’s OAuth flow.
5. Codex: configure the same remote endpoint with streamable HTTP for the server named `caraer-<portalname>` and start the configured OAuth flow when Codex is the selected runtime.
6. Claude: add a custom remote MCP connector named `Caraer — <portalname>` (or the host client's equivalent) using `https://v2.api.caraer.com/api/v2/mcp` over streamable HTTP; start Connect and use the browser flow when Claude is the selected runtime.
7. Cursor: configure the same remote endpoint in Cursor over streamable HTTP and start Cursor's native OAuth flow when Cursor is the selected runtime.
   For Hermes and any other confirmed AI client, follow the same guided lifecycle using that client's verified native add/connect/login capabilities. If the installed version lacks native support for this server's transport or authentication, explain the verified mismatch and propose a compatible supported path; do not silently switch clients or create a custom token bridge. Distinguish Claude Code from Claude web/desktop and Codex CLI from other Codex surfaces when their connection paths differ.
8. Record the selected client/runtime and streamable HTTP transport in validation. Start a fresh session after successful connection if authentication does not hot-reload.
9. Installed Caraer App provider: use app-installation endpoints only with a confirmed `appUuid`; never assume it is an OAuth `client_id`.

## Discover and isolate

1. Inspect the confirmed portal's configuration and credential presence without printing values.
2. Before a new integration, GET `https://v2.api.caraer.com/.well-known/oauth-authorization-server`; require authorization-code, refresh-token, `code`, and PKCE `S256` support.
3. The company selected during OAuth must match the user-confirmed portal.
4. Complete this step only when endpoint, portal, credential source, and authentication path are confirmed.

## Browser-mediated OAuth

1. Add a remote MCP connector named according to the selected client's conventions with the Caraer endpoint, then start its OAuth transaction so the **current client's** callback handler is ready (local listener or client-managed hosted callback).
   Reuse the existing configured connection when present; do not add a duplicate. If the user already completed login in Settings, proceed to validation instead of restarting consent.
2. Use the client's actual callback mechanism. For a client-managed hosted HTTPS callback, follow its native flow; do not demand a localhost listener or tunnel. For a loopback callback, check whether the browser runs on the listener's host. If not, use the client's supported remote-browser route or establish and verify a suitable forward before consent. Do not impose manual routing steps on a native flow that already handles its callback.
   - With OpenClaw shared OAuth, `mcp login` may print the generated URL instead of launching it. Open it unmodified in the verified Gateway-host browser. If opening is unavailable and the callback route supports the user's browser, share the exact generated URL only in the requesting user's private conversation. Do not log it or save it in tracked files. Do not use shared login for `per-requester` OAuth.
3. Once the native callback mechanism is ready, open the authorization page in a compatible user-accessible browser whenever possible. Say “I’ve opened the OAuth page” only when confirmed; if sharing a generated link instead, say “Open this authorization link.” Then guide the user through the steps below. Never enter credentials, MFA codes, authorization codes, or the final consent action for the user.
4. The authorization URL may include the client's configured/default scopes. Do not add, infer, or alter scopes yourself. The user must still be able to review and change the selection in the Caraer consent flow, including choosing **Enable all scopes** or only specific scopes. Do not instruct the user to configure scopes manually in Settings or in the private-app configuration. Give this exact guidance:
   1. Log in via Google, Microsoft, or your email credentials.
   2. Select the company you want to connect from the dropdown list. It must be the confirmed target portal.
   3. Select your private app, or create one with a name such as `MCP — <your name>`.
   4. Enable all scopes, or only the specific scopes you want to grant access to, in the consent flow.
   5. Review the selected permissions and click **Allow** / **Done** to finish.
5. Do not modify the selected scope set. If the user asks for help deciding, explain the scope categories and let them choose; do not approve, consent to, or alter permissions on their behalf.
   Stay with the user: explain what they should see next, help with a reported error, and resume validation after they finish. Do not claim to have opened a page without tool confirmation. If they cannot see the browser, use the supported private-link route or explain the concrete Settings fallback.
6. If an authorization URL must be sent to the user's browser, send the exact URL generated by the OAuth client only through the private conversation. Never add, remove, reorder, or edit its `scope`, `state`, `code_challenge`, redirect URI, or other parameters. A URL with client-provided scopes is valid; the user chooses whether to keep, change, or expand them in the consent flow.
7. Wait for the client to report a successful callback and durable credential registration—not merely for a browser success page. Start a fresh client session if it does not hot-reload MCP authentication.
8. Complete this step only when the connection is shown as connected and the company choice matches the target portal.

## Exchange and store

**For native/client-managed OAuth, the client performs exchange, storage, and refresh. Do not export its tokens, create a parallel environment file, or manually exchange codes. Verify credential registration without reading values, then proceed to validation. The manual exchange/storage steps below and “Every customer MCP session” apply only to a separately selected manual integration, not native OpenClaw setup.**

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
5. Only if the user's requested work involves local schema templates, compare them with the live schema after validation. Do not turn ordinary connection onboarding into a schema/development task. Request explicit approval before schema mutations or production publishing.
6. Finish successful connection onboarding with the intent question below. If validation is blocked, help resolve the connection first rather than offering CLI installation as its remedy.

## Finish onboarding: choose the next path

### Explain the three layers

Keep this explanation brief and relevant to the user's intended work:

- **Company MCP:** authenticated tools for the selected company's data and configuration, within granted permissions. This is enough to start ordinary connected work; no CLI is required.
- **Developer MCP and skills:** public documentation and task instructions, separate from company access. Skills do not grant permissions or authorise changes. An OAuth private-app selection alone does not mean a CLI project or skills were installed.
- **Caraer CLI:** local tooling for app-development workflows and packaged app/CMS skills. It is optional, not a requirement for every MCP user or every customization task.

Use the current [developer MCP documentation](https://developer.caraer.com/developer-mcp) and [skills catalogue](https://developer.caraer.com/developer-mcp/skills). Do not infer that a private app bundles skills because the company connection exposes tools, or that no skills exist because that connection advertises none. Discover developer skills separately; describe only what was actually found or installed.

### End with one intent question

After reporting verified company access, ask:

> **What would you like to do next: use Caraer (records, content, forms, and other connected features), build or customize an app, or finish for now?**

Wait for the answer; do not install development tools by default. If the user already stated their intent, follow that path without repeating this question.

- **Use Caraer:** continue with the requested connected task and relevant available skills. Do not add a CLI prerequisite. If no task is stated, ask what they want to accomplish. Connection approval is not blanket approval for company-data changes.
- **Finish for now:** confirm the connection is ready and stop. No additional setup is needed.
- **Build or customize an app:** explain that developer docs/skills guide the work, while CLI tooling is needed only for the chosen local build workflow. Ask: **“Would you like me to check your development setup and guide you through installing the Caraer CLI and relevant skills where needed? I'll preserve the working MCP connection.”** Reuse existing explicit approval for this developer setup; do not request it twice.

### Optional developer continuation

1. After the user chooses developer setup, inspect the selected client's capabilities, existing CLI/version, installed skills, and any existing project before proposing changes. Reuse adequate installations and preserve existing configuration. Do not install into another AI client just because its tools happen to be available.
2. Consult current official CLI documentation/help for supported installation, authentication, and skill-install commands. Do not guess commands or assume a global install is required. Choose only the relevant workflow/skills; ordinary records, forms, and content tasks can use company MCP tools without a local app build.
3. Where useful, offer the public developer MCP separately, explaining that it supplies documentation and skills, not company access. Its connection must not replace or rename the authenticated company MCP. Do not copy company credentials to it or repeat company OAuth for documentation access.
4. Perform the approved setup and guide each necessary user interaction. If a separate native login is required, apply the browser/generated-link guidance above. Install complete skill bundles with supporting references, preserving existing user skills rather than overwriting them blindly.
5. Verify the CLI/version and relevant skill discovery in the intended client. If a developer MCP was added, verify a small documentation/skill read there; separately retain the verified company connection. Report what was already present, newly installed, verified, or blocked. Documentation availability alone is not proof of a local CLI or skill installation.
6. End by asking what app or customization they want to build if not already known. Setup approval does not authorise deployment, publishing, spend, or unrelated company changes.

## Installed-App provider OAuth

1. With the confirmed customer bearer credential, GET `/api/v2/apps/{appUuid}/installation/connections`.
2. Use returned `data.name` as provider identifier, not display-only `data.label`.
3. POST `/api/v2/apps/{appUuid}/installation/oauth/{provider}/start`, re-read connections, and require `connected: true`.

## Security

Never log, chat, commit, screenshot, or store in tracked files passwords, MFA codes, client secrets, authorization codes, access tokens, refresh tokens, PKCE verifiers, or standalone state values. The sole link-sharing exception is the exact client-generated authorization URL sent privately to its requesting user as described above; do not extract or separately expose its parameters. Never reuse another customer's credential or portal. Never revoke or retire legacy credentials automatically.

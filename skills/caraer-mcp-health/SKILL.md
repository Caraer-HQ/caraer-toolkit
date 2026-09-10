---
name: "caraer-mcp-health"
description: "Check Caraer MCP health and guide gradual API-key-to-OAuth migration."
user-invocable: true
---

# Caraer MCP health

Use for `/caraer-mcp-health [customer]` or `/caraer_mcp_health [customer]`.

## Default behavior: lightweight check

1. Resolve the customer namespace.
   - If the current workspace maps unambiguously to one customer workspace, use it.
   - If it does not clearly map to one customer workspace, inspect the current session/workspace display label before any MCP inspection or request.
   - If the label identifies a customer, ask the operator for approval to navigate to `/customer/[client]`. Only after approval, navigate there; do not inspect MCP configuration or make an MCP request before navigation.
   - If approval is not granted, stop. If the label does not identify a customer, ask for the customer name.
2. Select the exact customer portal and read its `access.md`. Never guess between Caraer, Waddenvacatures, or another portal.
3. Inspect the customer MCP configuration and credential source locally without printing tokens, headers, secrets, or full credential paths.
4. Determine the authentication mode:
   - OAuth: an OAuth client ID/access-token/refresh-token setup is configured.
   - Legacy API key: the MCP uses an API-key/bearer token environment variable or secure legacy credential.
   - Missing/unknown: no usable credential configuration is available.
5. If either OAuth or a legacy API key is configured, perform the technical light check below.
6. Report the actual light-check response concisely. Do not infer business-data access, scopes, plan access, task access, or meter access from a successful `tools/list`.
7. If a legacy API-key setup is active, add a WARN after the light-check result and ask:
   **"A legacy API-key setup is still active. Do you want me to start the OAuth migration with `/skill caraer-mcp-oauth [customer]`?"**
   Do not start OAuth, revoke keys, or change configuration automatically.
8. If OAuth is configured and the light check succeeds, ask:
   **"Do you want a full MCP check, including read-scope/tool coverage and a small read-only schema/object query?"**
   Wait for explicit approval before performing the full check.
9. If the check fails, report the exact non-secret status/error and the smallest next action. Do not retry blindly.

## Technical light-check runbook

Use the configured MCP client/server when directly available. Otherwise call the Caraer MCP endpoint with a browser-like HTTP client. The default endpoint is:

`https://v2.api.caraer.com/api/v2/mcp`

Use the customer-specific credential selected in step 4:

- Legacy API key: `Authorization: Bearer ${<customer token env var>}`
- OAuth: `Authorization: Bearer ${<customer OAuth access-token env var>}`

Never substitute the shared Caraer token or another customer’s credential.

### Request sequence

1. Send one JSON-RPC `initialize` request with a 20–30 second timeout:

```json
{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"caraer-mcp-health-check","version":"1.0"}}}
```

2. If initialize returns HTTP 200 and a JSON-RPC result, send one `tools/list` request with the same timeout:

```json
{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}
```

3. Accept either a JSON response or an SSE response containing a `data: {...}` JSON-RPC payload. Treat HTTP 200 plus a result with a non-empty `tools` array as a successful light check.
4. Extract only:
   - initialize HTTP/status result;
   - tools/list HTTP/status result;
   - tool count;
   - up to 8 non-sensitive tool names;
   - non-secret error code/message, if present.
5. Do not print or persist the Authorization header, token, response fields containing token material, or raw response bodies.
6. Do not perform schema queries, business-record reads, scope audits, or writes in the light check.

### Safe curl fallback

Use the token through environment expansion; never replace the placeholder with a literal token in saved commands or output:

```sh
curl -sS --max-time 30 \
  -H "Authorization: Bearer ${CUSTOMER_MCP_ACCESS_TOKEN}" \
  -H "Accept: application/json, text/event-stream" \
  -H "Content-Type: application/json" \
  -X POST "https://v2.api.caraer.com/api/v2/mcp" \
  --data '{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}'
```

For a complete protocol check, send `initialize` first. Do not log the curl command after shell expansion.

## Full check only after approval

When the operator explicitly requests the full check:

1. Follow the Caraer OAuth credential-refresh rules before MCP requests.
2. Verify read-only tool/scope coverage needed for customer setup, tasks, plans, contracts, relations, and usage meters.
3. Run one small read-only schema/object query and confirm the response is not an MCP error.
4. Report PASS, WARN, or FAIL for configuration, connectivity, authenticated portal, tool coverage, and read-only query.
5. Never create, rotate, grant, revoke, or modify access unless separately requested.

## Security

- Keep customer portals and credentials isolated.
- Preserve legacy API keys until OAuth validation succeeds and the operator approves retirement.
- Never log, chat, commit, or store tokens, authorization codes, client secrets, PKCE verifiers, refresh tokens, or authorization headers.
- Never expose credential values in reports.

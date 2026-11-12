---
name: "caraer-credential-vault-handoff"
description: "Safely provision a credential into an existing Caraer app installation vault, including OpenClaw protected handoffs. Use for credential setup, rotation, or troubleshooting; never treat vault presence as provider validation or authorization to activate the feature."
---

# Caraer Credential Vault Handoff

Use this procedure to put a provider credential into an existing Caraer app installation's SECRET setting. It covers generic handoffs and an OpenClaw-specific route. A vault write does not authorize feature activation, deployment, paid calls, scope expansion, schema changes, or provider testing.

## 1. Preflight before collecting the credential

1. Identify the exact company, app, installation, and SECRET setting. Distinguish company-owned credentials from credentials scoped to an individual installation.
2. Read only secret-presence metadata. If the target is already populated, stop without overwriting unless rotation or replacement was explicitly requested.
3. Confirm the supported write path and required authentication from current Caraer documentation. Administrator credentials, user credentials, and installation tokens are not interchangeable; do not guess or substitute endpoints.
4. Capture a safe baseline of nonsecret settings, mappings, resolved scopes, and other secret-presence flags. Do not print full app responses or tokens.
5. Confirm the protected handoff can deliver the value to the actual API consumer. Prefer a native masked vault flow; otherwise use a supported write-only handoff bound to the exact destination host. Never collect credentials through ordinary chat or a generic text prompt.

**Preflight is complete** only when the target, write path, authentication, baseline, and protected consumer are known. Do not ask the user to enter the credential before then.

## 2. Transfer without exposing or overwriting

1. Use only the documented API and scoped authentication. Keep the value out of source code, documents, shell arguments, plaintext temporary files, URLs, logs, diagnostics, and output. Do not bypass TLS or protected egress.
2. Re-check target presence immediately before writing. Preserve existing nonsecret settings, mappings, and scopes. Omit unrelated SECRET fields only when the current API's omission semantics have been confirmed; never submit blank placeholders for them.
3. Make the write idempotent: do not overwrite an existing value unless replacement was authorized. If a save times out or its response is uncertain, read the destination before retrying.
4. Handle errors without printing request objects, bodies, tokens, or unsanitized exceptions. A queued/background process is not proof of transfer; collect its terminal result using the current supported mechanism.

## 3. Independently verify and clean up

1. Make a separate, fresh read after the write. Verify the target secret's presence using the API's current metadata field.
2. Compare nonsecret settings, mappings, resolved scopes, and other secret-presence flags with the baseline. Do not infer that the provider accepts the value from a presence flag.
3. Delete the temporary handoff only after independent destination verification. Confirm it is no longer active and stop processes that may retain a stale snapshot.
4. Describe the actual deletion semantics. Do not claim immediate physical erasure unless the store documents it.

Report these as three separate states: **credential received**, **saved in destination**, and **provider tested**. State that provider validity remains untested unless a separately authorized provider check was performed.

## OpenClaw protected handoff

OpenClaw's secret store, Gateway tools, and egress behavior vary by version. Before acting, inspect the live tool schemas and installed documentation. Reuse an already committed masked handoff when appropriate; do not re-collect a credential merely because the receiving process is misconfigured.

### Preflight

- Discover the current `secrets`, `gateway_exec`, and `gateway_process` tool schemas.
- Confirm the Caraer API route and company context with a read-only request.
- Inspect secret-store metadata only; do not expose unrelated agent-readable environment-entry values.
- Verify both Gateway destination policy and the entry's exact allowed-host binding. For a vault write, the receiver is the Caraer API host, not the provider host.
- Use Gateway-hosted execution. Native Codex shell, a sandbox, or a remote node does not receive Gateway protected-store injection.
- If protected egress needs configuration, inspect and merge current state without replacing existing allow/bypass host lists. Use the supported configuration/repair path, confirm restart completion, and start a fresh run. Do not restart a healthy runtime unnecessarily.

### Masked entry and fresh-run boundary

Use the native masked `secrets` request flow, bound to the exact Caraer API host. The person enters the value in the masked UI; the request contains metadata only. Honor the host policy returned by the tool. A `no_answer` result means no credential arrived.

Some Gateway execution paths snapshot protected entries on their first execution in a run. If that happened before the masked save or host-policy change, start a fresh run; repeating the command in the old run may not refresh its snapshot. Plan for this before prompting so the user need not enter the same credential twice. If a masked save committed but runtime refresh failed, repair/reload the runtime rather than asking for another paste.

### Protected transfer

The Gateway-hosted process may receive an opaque sentinel for the named secret; the HTTPS egress proxy substitutes the value only for requests to an allowed destination. The HTTP client must honor the injected proxy and CA configuration. Check only whether required environment variables exist; never print proxy URL values because they may contain credentials. Never print, transform, override, or template-interpolate the secret, and never disable certificate verification.

Before implementing a writer, verify the current Caraer API route, authentication class, SECRET-setting schema, and omission semantics. Preserve existing settings and grants, avoid unrelated writes, and use an installation-save path only when documented for this purpose. Do not confuse it with company runtime-settings merge, app creation, release publication, or deployment.

### Verification and cleanup

Perform the independent fresh Caraer read described above. Only after it confirms the target secret is present should you delete the temporary OpenClaw entry, verify it is no longer active, and end any process holding an older snapshot. Consult current OpenClaw documentation for soft-delete or purge behavior; do not promise physical erasure based on an old version's behavior.

## Failure handling

- **The process cannot see the handoff:** check whether it runs on the Gateway, whether protected egress is enabled, and whether its run snapshot predates the save. Repair the runtime or start a fresh run; do not request another paste first.
- **Destination denied:** check both Gateway traffic policy and the entry's exact host binding, preserving existing host policy.
- **TLS failure:** use the injected proxy and CA; investigate health or clock issues. Never disable TLS verification.
- **Authentication rejected:** confirm the required credential class from current documentation. Do not invent a token workaround.
- **Write result uncertain:** independently read destination state before any retry.
- **Temporary handoff missing but destination unconfirmed:** report uncertainty; do not claim success or invent a recoverable copy.
- **Secret present but feature fails:** provider validity and feature behavior are a separate investigation within the authorized scope.

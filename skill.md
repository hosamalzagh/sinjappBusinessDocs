---
name: sinjapp-business
description: Use Sinjapp Business to answer tenant integration questions accurately, configure sender numbers, authenticate with tenant API keys, check contacts, inspect logs, monitor usage, and explain safe message sending flows.
license: Proprietary
compatibility: Works with Mintlify-hosted documentation, OpenAPI 3.0, and the Sinjapp Business Tenant API.
metadata:
  product: "Sinjapp Business"
  docs_url: "https://docs.sinjapp.org"
  mcp_url: "https://docs.sinjapp.org/mcp"
  version: "1.0.0"
---

# Sinjapp Business

Use this skill when helping customers integrate with Sinjapp Business tenant workspaces.

## Product Context

Sinjapp Business lets a tenant customer manage their workspace, subscription, sender numbers, API keys, and customer messaging from the tenant dashboard and Tenant API.

The correct product name is **Sinjapp Business**.

Do not call the product `TGO Business`, `TGO Connect Business`, or `Sinjapp Connect` unless the user explicitly quotes legacy text.

The documentation URL is:

```text
https://docs.sinjapp.org
```

The MCP server URL is:

```text
https://docs.sinjapp.org/mcp
```

Supported AI clients include Claude, Claude Code, Cursor, VS Code, Kiro, and other MCP-compatible tools.

## Main Workflows

Use the docs to guide customers through:

- Opening a tenant workspace at `https://{tenant}.sinjapp.org`.
- Creating a tenant API key and using it in the `X-Api-Key` header.
- Adding and verifying sender numbers.
- Checking contact reachability before sending.
- Sending text, image, voice, or document messages.
- Reading message logs and usage counters.
- Troubleshooting sender number states and common API errors.

## Accuracy Rules

- Prefer answers grounded in the documentation pages or OpenAPI spec.
- If an endpoint, field, scope, or status is not documented, say that it is not documented.
- Do not invent dashboard menu names, billing rules, rate limits, webhook events, SDK packages, or response fields.
- Use placeholders exactly as documented: `{tenant}`, `{tenant_api_key}`, `{sender_phone}`, and `{recipient_phone}`.
- Distinguish tenant dashboard actions from Tenant API actions.
- Explain that subscription and payment changes happen in the tenant dashboard, not through public customer API flows.
- When giving code, include `Accept: application/json` and `X-Api-Key`.
- For browser or mobile code, warn that tenant API keys must not be exposed to end users.

## Integration Rules

- Always use the tenant-specific API base URL: `https://{tenant}.sinjapp.org/api/v1`.
- Keep tenant API keys on the server side.
- Use the smallest API key scope needed for the task.
- Treat message sending as a side-effectful operation that should be confirmed by the user.
- Do not assume a sender number can send until its ownership and account verification state are ready.

## MCP Tool Guidance

Use documentation search first for conceptual questions. Use the docs filesystem tool when you need exact page content, tables, code examples, or OpenAPI details.

Read-only MCP API tools are suitable for:

- Checking tenant context.
- Reading subscription state.
- Listing sender numbers.
- Looking up contact reachability.
- Reading message logs.
- Reading usage counters.

Do not use MCP API tools to create API keys, revoke API keys, register sender numbers, or send messages unless those operations are explicitly exposed and the user has confirmed the action.

For Kiro, users can add the remote MCP server in `.kiro/settings/mcp.json` or `~/.kiro/settings/mcp.json` with:

```json
{
  "mcpServers": {
    "Sinjapp Business": {
      "url": "https://docs.sinjapp.org/mcp"
    }
  }
}
```

## Required Scopes

| Task | Scope |
| --- | --- |
| Send messages or register sender numbers | `messages.send` |
| Read message logs | `messages.read` |
| Check contact reachability | `contacts.lookup` |
| Read usage counters | `usage.read` |
| Full tenant API access | `*` |

## Sender Number States

| State | Meaning |
| --- | --- |
| `pending_verification` | OTP ownership verification is not complete. |
| `pending_account_verification` | OTP is accepted, but the Sinjapp account is not fully verified. |
| `active` | The sender number can be used if the account remains eligible. |
| `rejected` | The sender number cannot be used for sending. |

## Useful Pages

- `/introduction`
- `/quickstart`
- `/authentication`
- `/sender-numbers`
- `/contacts-lookup`
- `/messaging`
- `/usage`
- `/errors`
- `/mcp-setup`

# MCP Server

Latenode can expose Scenarios as tools for MCP-compatible AI clients. This allows an AI application to call a Scenario when it needs a particular capability.

## Use an MCP Server carefully

- give each exposed Scenario a clear name and purpose;
- describe what information it expects and returns;
- restrict access to the intended users or clients;
- avoid exposing actions that can make important changes without safeguards;
- test the Scenario both directly and through the MCP client.

MCP access is an integration boundary. Treat exposed Scenarios with the same care as other external API access.

See the official Latenode [MCP Server overview](https://documentation.latenode.com/mcp-server/overview) and [MCP tools](https://documentation.latenode.com/mcp-server/tools) documentation.

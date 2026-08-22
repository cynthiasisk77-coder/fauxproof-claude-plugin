---
name: setup
description: Connect or troubleshoot FauxProof in Claude Code. Use when the user asks to install, enable, connect, authenticate, sign in to, reconnect, or diagnose the FauxProof plugin or MCP server.
---

# Set up FauxProof

Help the user connect without asking them to paste a password, access token, authorization code, client secret, or other credential into the conversation.

1. Confirm that the FauxProof plugin is enabled. Because it connects to an external private service, the plugin is disabled by default until the user opts in. The user can enable it from `/plugin` or with `claude plugin enable fauxproof`.
2. Ask the user to open `/mcp` in Claude Code and select `plugin:fauxproof:fauxproof`.
3. Ask them to choose Connect or Authenticate and complete FauxProof sign-in in the browser window. Do not ask them to copy credentials into chat.
4. After Claude Code reports Connected, verify access with the read-only `get_lockbox_state` tool. Do not create a project or change stored work as a connection test.
5. If authentication fails, report the visible error in ordinary language. Check that the plugin is enabled and that the server URL is reachable, then retry from `/mcp`. Never suggest embedding an OAuth client secret in `.mcp.json`.
6. If the tools connect but no saved work appears, explain that the account may not have a project yet. Ask whether the user wants to create one; never create it silently.

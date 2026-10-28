# MCP: VS Code

VS Code (with GitHub Copilot's agent mode) reads MCP servers from `.vscode/mcp.json` in your workspace.

## Steps

1. In your workspace, create `.vscode/mcp.json`:

```json
{
  "servers": {
    "binance-mcp-server": {
      "type": "http",
      "url": "https://agent.binance.com/mcp/agentic"
    }
  }
}
```

2. Save the file. VS Code discovers the server; start it from the MCP panel (or the Command Palette → **MCP: List Servers**).
3. Complete the browser authentication: sign in, pick your agent, set permissions.
4. Ask Copilot a read-only question first (for example, your Agentic sub-account USDT balance) to confirm the connection.

Source for the endpoint and auth flow: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794).

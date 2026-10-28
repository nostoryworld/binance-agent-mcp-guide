# MCP: Claude Desktop

Claude Desktop's newer versions support remote MCP servers through the Connectors UI.

## Steps

1. Open Claude Desktop → **Settings → Connectors**.
2. Add a custom connector with the Binance MCP endpoint:

```
https://agent.binance.com/mcp/agentic
```

3. Complete the browser authentication (sign in, pick your agent, set permissions) exactly as in [Claude Code](mcp-claude-code.md).
4. Start a new chat — the Binance tools should be available.

If your Claude Desktop version does not show a Connectors section, update the app first, or use Claude Code for the MCP route and the desktop app for the Skills route (see the [first-time setup](01-first-time-setup.md)).

Source for the endpoint and auth flow: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794).

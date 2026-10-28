# MCP: Cursor

Cursor supports remote MCP servers in its MCP settings (`.cursor/mcp.json`, project or global).

## Steps

1. Open Cursor → **Settings → MCP** (or **Cursor Settings → Tools & MCP**).
2. Add a new MCP server with these settings:

```json
{
  "mcpServers": {
    "binance-mcp-server": {
      "url": "https://agent.binance.com/mcp/agentic"
    }
  }
}
```

3. Save. Cursor connects to the endpoint and starts the browser authentication flow.
4. Sign in, pick your agent, and set permissions (features, products, funding limits).
5. Verify in Cursor's MCP panel that the server shows as connected, then ask a read-only question first (for example, your Agentic sub-account USDT balance).

If Cursor asks for a transport type, choose **Streamable HTTP** (not SSE, not stdio) for this endpoint.

Source for the endpoint and auth flow: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794).

# MCP: Codex

Codex reads MCP servers from its config file (`~/.codex/config.toml`).

## Steps

1. Open `~/.codex/config.toml` (create it if it does not exist) and add:

```toml
[mcp_servers.binance-mcp-server]
url = "https://agent.binance.com/mcp/agentic"
```

2. Save and restart Codex.
3. Complete the browser authentication: sign in, pick your agent, set permissions.
4. Ask a read-only question first (for example, your Agentic sub-account USDT balance).

Source for the endpoint and auth flow: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794).

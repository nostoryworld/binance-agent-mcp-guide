# MCP: ChatGPT

ChatGPT supports MCP servers in developer mode (availability varies by plan — check your ChatGPT settings for a Connectors/MCP section).

## Steps

1. In ChatGPT, open **Settings → Connectors** (developer mode).
2. Add a new MCP server with the Binance endpoint:

```
https://agent.binance.com/mcp/agentic
```

3. Complete the browser authentication: sign in, pick your agent, set permissions.
4. Ask a read-only question first (for example, your Agentic sub-account USDT balance).

If your ChatGPT plan does not show a Connectors section, use Claude Code or Cursor for the MCP route — the Binance Skills route (see the [first-time setup](01-first-time-setup.md)) works with any agent that can run shell commands.

Source for the endpoint and auth flow: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794).

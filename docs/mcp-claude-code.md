# MCP: Claude Code (official, verified)

The official Binance MCP endpoint:

```
https://agent.binance.com/mcp/agentic
```

## Steps

```bash
claude mcp add binance-mcp-server --transport http https://agent.binance.com/mcp/agentic
```

Then inside your agent:

1. Type `/mcp` — `binance-mcp-server` should be listed.
2. Select it → **Authenticate**. Your browser opens a Binance sign-in page.
3. Pick the agent to connect, then toggle permissions (features, products, funding limits).

Change permissions later: **Sub Accounts → Account Management**.

Source: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794).

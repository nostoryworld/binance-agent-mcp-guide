# MCP: Muse and other shell-capable agents

Muse (and any agent that can run shell commands in a workspace) connects to Binance through the same two official routes. There is no separate "Muse installer" — you use the standard commands.

## Route A — MCP endpoint

Muse connects to MCP-style services through its own connector flow. Point it at the official endpoint:

```
https://agent.binance.com/mcp/agentic
```

Then complete the same browser authentication as every other client: sign in, pick your agent, set permissions. The generic server block, where your Muse client accepts custom MCP servers, is:

```json
{
  "mcpServers": {
    "binance-mcp-server": {
      "url": "https://agent.binance.com/mcp/agentic"
    }
  }
}
```

## Route B — Agentic Wallet skill (the usual way on Muse)

This is the route most Muse users actually use, because Muse runs shell commands in a workspace:

```bash
npx skills add binance/binance-skills-hub/skills/binance-web3/binance-agentic-wallet
```

Then simply ask Muse:

> "Sign in to my Agentic Wallet"

Muse shows the login link / QR code; scan it in the Binance app, confirm the pairing code matches, and you are connected. The full walkthrough is in the [first-time setup](01-first-time-setup.md).

## Any other shell-capable agent

The rule is the same everywhere: if the agent can run shell commands in your workspace, the Skills package registers the `baw` CLI plus its instructions, and the agent can drive the wallet. Install the skill in the folder the agent works in, sign in once, and set your wallet rules before the first trade.

Source for the endpoint and auth flow: [Binance Agent OS blog (official)](https://www.binance.com/en/blog/ecosystem/5991233187660196794). Source for the Skills route: [Binance Web3 docs (official)](https://web3.binance.com/en/dev-docs/products/agentic-wallet/agent-setup).

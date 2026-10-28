# Binance Agent MCP & Agentic Wallet Setup Guide

Teach your AI agent to use Binance — trading, market data, and on-chain wallet actions — the official way.

## Start here

- **Never connected an agent before?** → [First-time setup, step by step](docs/01-first-time-setup.md) — account, KYC, Node.js, client install, MCP connect, wallet sign-in, rules, first commands, with a checkpoint at every step.
- **Want to hunt free mints?** → [Hunting free mints with your agent](docs/02-hunting-free-mints.md) — the free-only playbook: verify on-chain before minting, gas cap, rarity before selling, red flags, and copy-paste agent prompts.

There are **two official routes**, and they do different things:

| Route | What it unlocks | How it authenticates |
| --- | --- | --- |
| **A. Binance Agent OS MCP** | Spot, Futures and Convert trading, live market data (order books, prices, klines), balances, positions, transfers | Browser OAuth-style sign-in, scoped to a dedicated **Agentic sub-account** |
| **B. Binance Agentic Wallet skill + `baw` CLI** | On-chain wallet: balances, swaps, limit orders, transfers, DeFi, prediction markets | QR sign-in in the Binance app; a separate **keyless wallet** under your Binance account |

MCP currently covers **trading and market data**. On-chain and payment features arrive through the Skills route (and future MCP releases). Use both if you want the full picture.

> **Safety first, before anything else**
> - The agent can **never withdraw to external addresses** through the official MCP — there is no withdrawal scope.
> - The agent only touches an **isolated Agentic sub-account / Agentic Wallet**, never your main account. Fund it only with what you are prepared to expose.
> - Set **daily limits, token scope, and address-book restrictions** in the Binance app before the first trade. The agent can read these rules but cannot change them.
> - Review every order and transfer before confirming. Revoke anytime: **Sub Accounts → Account Management → Disconnect Agents**, or **Emergency Stop** to cut all agents at once.
> - Never paste a Binance API key into a chat window, a public repo, or a third-party website.

## Prerequisites

- A **verified Binance account** (KYC complete).
- **Node.js 18+** on the machine running the agent (`node -v` to check). The Skills installer runs through `npx`.
- An AI agent client: Claude Code, Claude Desktop, Cursor, VS Code, Codex, ChatGPT, OpenClaw, or any MCP-compatible agent (see below).
- The Binance app on your phone (for QR sign-in on Route B).

## Route A — Binance Agent OS MCP (trading + market data)

The official MCP endpoint is:

```
https://agent.binance.com/mcp/agentic
```

### Claude Code (verified steps)

```bash
claude mcp add binance-mcp-server --transport http https://agent.binance.com/mcp/agentic
```

Then, inside your agent environment:

1. Type `/mcp` — you should see `binance-mcp-server` listed.
2. Select it and choose **Authenticate**. Your browser opens a Binance sign-in page.
3. Pick the agent you want to connect from the dropdown.
4. Toggle the permissions (features, products, funding limits). Anything left off stays inaccessible until you enable it.

Review or change permissions later under **Sub Accounts → Account Management**.

### Other MCP clients

Every client below connects to the **same endpoint** (`https://agent.binance.com/mcp/agentic`) with HTTP/streamable-HTTP transport, then the same browser authentication flow. Per-client guides live in `docs/`:

- [Claude Desktop](docs/mcp-claude-desktop.md)
- [Cursor](docs/mcp-cursor.md)
- [VS Code](docs/mcp-vscode.md)
- [Codex](docs/mcp-codex.md)
- [ChatGPT](docs/mcp-chatgpt.md)
- [Muse and other shell-capable agents](docs/mcp-muse.md)

Full client-by-client setup guides are also published by Binance at [binance.com/agent-os](https://binance.com/agent-os).

### First checks (Route A)

Ask your agent something read-only first:

> "What is my Agentic sub-account USDT balance?"

Then a market-data check:

> "Show me the BTC/USDT order book top 5 bids and asks."

## Route B — Binance Agentic Wallet skill + `baw` CLI (on-chain)

This is the route for on-chain work. The agent does **not** ship with its own chat client — you install the Binance Skills into the agent you already use.

### 1. Install the skill

In any folder your agent works in:

```bash
npx skills add binance/binance-skills-hub/skills/binance-web3/binance-agentic-wallet
```

Or install the whole hub and pick later:

```bash
npx skills add https://github.com/binance/binance-skills-hub
```

The Skills package registers the `baw` CLI plus its instructions. Any agent that can run shell commands in your workspace can drive the wallet.

### 2. Install the `baw` CLI (if not already present)

```bash
npm install -g @binance/agentic-wallet@1.11.0
```

(The skill checks against this version. The CLI is also installed automatically the first time you use it through the skill.)

### 3. Sign in

Tell your agent:

> "Sign in to my Agentic Wallet"

It will show you a login link. Open it on your phone (the Binance app opens directly) or scan the QR code with the Binance app from a computer screen. Confirm the **pairing code** shown in the app matches the one shown by the agent, then enable secure automatic signing and accept the Terms of Service and the Agentic Wallet Security Statement.

From a terminal, the same flow is:

```bash
baw auth signin    # produces the QR code / login link
baw auth verify    # confirms the pairing
```

Alternative in-app path: open the Binance app → **Wallet → More → Agentic Wallet → Use My Own Agent**, and follow the five-step in-app guide.

### 4. Verify

Ask a read-only question first:

> "What's my Binance Agentic Wallet address and USDT balance?"

If the agent says you are not signed in, the skill loaded correctly and you only need to complete sign-in. If it does not recognise the request at all, the skill was installed in the wrong folder — re-run the install command in the folder your agent is working in, then restart the agent session.

### 5. Wallet rules (do this before the first trade)

In the Binance app, set for the Agentic Wallet:

- Daily spending limit (keep it small for anything unattended)
- Tradable token scope
- High-risk transaction handling
- Address-book restrictions for transfers

To end a session, tell the agent **"Sign out"** — this revokes the session. This matters most on shared or temporary machines.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Agent doesn't recognise wallet requests | Skill installed in another directory | Re-run the install command in the folder your agent works in |
| `npx: command not found` | Node.js missing or too old | Install Node.js 18+ and re-check with `node -v` |
| Install succeeds but nothing changes | Session started before install | Restart the agent session so it reloads its instructions |
| Sign-in QR code expires before scanning | Link is short-lived | Ask the agent to sign in again for a fresh code |
| MCP server listed but tools fail | Permissions not granted | Re-check Sub Accounts → Account Management and enable the missing scope |

## Official vs unofficial — read this before installing anything else

The two routes above are **Binance's official** integration. Community packages exist (for example, third-party `binance-mcp-server` npm packages that ask you to paste a raw `BINANCE_API_KEY` / `BINANCE_API_SECRET` into a config file). Those are **not** Binance's official route:

- The official MCP authenticates in your browser and scopes access to a dedicated sub-account.
- A raw API key pasted into a client config is a full credential — if it leaks, it can be abused, and it usually carries wider permissions than the agent needs.

If a guide asks for your API secret, treat it as unofficial and weigh the risk before proceeding.

## Sources

- [Binance Agent OS — built for AI agent integration (official blog)](https://www.binance.com/en/blog/ecosystem/5991233187660196794)
- [Set Up Your AI Agent — Binance Web3 docs (official)](https://web3.binance.com/en/dev-docs/products/agentic-wallet/agent-setup)
- [Introducing Binance Agent OS (official announcement)](https://www.binance.com/en/support/announcement/detail/07d45cdd3831498f8a4ff339031a8480)
- [Binance Agentic Wallet FAQ (official)](https://www.binance.com/en/support/faq/detail/3ff00e2d488a41c4aaa4aabb6fc36763)
- [Binance Skills Hub on GitHub (official)](https://github.com/binance/binance-skills-hub)
- [Binance Agent OS hub](https://binance.com/agent-os)

*Guide last verified: 28 October 2026. Binance's pages are the final authority — if a step here disagrees with an official page, follow the official page.*

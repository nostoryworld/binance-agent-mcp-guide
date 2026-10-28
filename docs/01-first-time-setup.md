# First-Time Setup, Step by Step

This page assumes **zero prior setup**. Follow it top to bottom and you will end with an AI agent that can read your Binance Agentic Wallet and make its first read-only check. Nothing here requires trading experience.

> **Time needed:** about 20–30 minutes, most of it waiting on identity verification.

## Step 0 — What you are building

```
You ──► Your AI agent (Claude Code, Cursor, …) ──► Binance
          │                                          │
          ├─ Route A: MCP server (trading + data)    ├─ Agentic sub-account
          └─ Route B: Agentic Wallet skill (on-chain)└─ Agentic Wallet (keyless)
```

The agent never touches your main Binance account. It only ever sees the isolated sub-account / wallet you fund on purpose.

## Step 1 — Create and verify your Binance account

1. Go to [binance.com](https://www.binance.com) and click **Sign Up**.
2. Register with your email or phone number and set a strong password.
3. Complete **identity verification (KYC)**: government ID + a selfie. This is required — the agent features will not work on an unverified account.
4. Turn on **two-factor authentication (2FA)** in your account security settings (authenticator app, not just SMS).
5. Install the **Binance app** on your phone and sign in with the same account. You will need it later for QR sign-in.

**Checkpoint:** you can log in to binance.com and the app, and your account shows as Verified.

## Step 2 — Install Node.js (the agent tooling runs on it)

The Skills installer runs through `npx`, which ships with Node.js. You need **version 18 or newer**.

1. Download the installer for your system from [nodejs.org](https://nodejs.org) (the LTS version is fine).
2. Run the installer, accepting the defaults.
3. Open a terminal (Terminal on macOS, Command Prompt or PowerShell on Windows, any terminal on Linux) and check:

```bash
node -v
```

You should see something like `v20.x.x` or `v22.x.x`. If you see "command not found", close and reopen the terminal and try again.

**Checkpoint:** `node -v` prints a version number 18 or higher.

## Step 3 — Install an agent client

Pick **one** to start with. Claude Code is the best-documented path; the others work the same way afterwards.

### Option A — Claude Code (terminal)

```bash
npm install -g @anthropic-ai/claude-code
```

Then launch it in any folder you want the agent to work in:

```bash
claude
```

Follow the login prompt: choose your Claude subscription, or paste an Anthropic API key when asked. The credential is stored locally; you only do this once.

### Option B — Claude Desktop (window instead of terminal)

1. Download the app from [claude.com/download](https://claude.com/download) (`.dmg` for macOS, `.exe` for Windows).
2. Sign in with your Claude account.
3. Switch to the **Code** tab in the sidebar and choose the folder you want the agent to work in. This is the folder the Skills get installed into.

### Option C — Anything else (Cursor, VS Code, Codex, OpenClaw…)

Install the client of your choice the normal way. The rule that matters: **the client must be able to run shell commands in your workspace**. If it can, the rest of this guide works unchanged — only the settings screen where you paste the MCP server differs (see `docs/mcp-*.md`).

**Checkpoint:** your agent client opens and can answer a plain question.

## Step 4 — Connect the trading MCP (Route A)

This gives the agent Spot, Futures and Convert trading, live market data, balances, positions and transfers.

### Claude Code

```bash
claude mcp add binance-mcp-server --transport http https://agent.binance.com/mcp/agentic
```

Then inside your agent:

1. Type `/mcp`. You should see `binance-mcp-server` in the list.
2. Select it and choose **Authenticate**. Your browser opens a Binance sign-in page.
3. Sign in, then pick the agent you want to connect from the dropdown.
4. Toggle the permissions: which features and products the agent may use, and the funding limits. **Anything left off stays inaccessible until you enable it** — this is your safety net, so leave trading off until you are ready to test read-only access first.

### Other clients

Same endpoint, same browser authentication afterwards:

```
https://agent.binance.com/mcp/agentic
```

Per-client steps: [Claude Desktop](mcp-claude-desktop.md), [Cursor](mcp-cursor.md), [VS Code](mcp-vscode.md), [Codex](mcp-codex.md), [ChatGPT](mcp-chatgpt.md), [Muse](mcp-muse.md).

**Checkpoint:** `/mcp` (or your client's MCP panel) shows `binance-mcp-server` as connected.

## Step 5 — Install the Agentic Wallet skill (Route B)

This gives the agent on-chain abilities: balances, swaps, limit orders, transfers, DeFi.

In the folder your agent works in, run:

```bash
npx skills add binance/binance-skills-hub/skills/binance-web3/binance-agentic-wallet
```

If the `baw` command-line tool is not already installed, install it too:

```bash
npm install -g @binance/agentic-wallet@1.11.0
```

(The skill checks against this version, and it is also installed automatically the first time you use it through the skill.)

**Checkpoint:** your agent can now answer questions about the Binance Agentic Wallet. Test it in Step 7.

## Step 6 — Sign in to the Agentic Wallet

Tell your agent, in plain words:

> "Sign in to my Agentic Wallet"

What happens next:

1. The agent shows you a **login link** (and a QR code on screen).
2. **On your phone:** open the link — the Binance app opens directly. **On a computer:** open the Binance app and use **Scan** on the QR code shown.
3. Check the **pairing code** displayed in the app matches the one shown by the agent. If they do not match, stop and start again.
4. Enable **secure automatic signing** and accept the Terms of Service and the Agentic Wallet Security Statement.
5. The first time you sign in, the app walks you through creating your Agentic Wallet. When it finishes, return to the agent to confirm.

From a terminal, the same flow is:

```bash
baw auth signin    # produces the QR code / login link
baw auth verify    # confirms the pairing
```

Alternative in-app path: Binance app → **Wallet → More → Agentic Wallet → Use My Own Agent**, then follow the five-step in-app guide.

**Checkpoint:** the agent confirms you are signed in.

## Step 7 — Set the wallet rules BEFORE the first trade

Do this in the Binance app, before you let the agent move anything:

1. **Daily spending limit** — set it low. If your agent can act while you are not watching, it should not be able to move your whole balance.
2. **Tradable token scope** — which tokens the agent may touch.
3. **High-risk transaction handling** — how the agent must behave on risky transactions.
4. **Address-book restrictions** — transfers are restricted to addresses in your address book.

The agent can **read** these rules but **cannot change them**. That is by design — the limits are enforced at the API level, not by the agent's goodwill.

## Step 8 — Your first commands (read-only first)

Always start read-only. Ask your agent:

> "What's my Binance Agentic Wallet address and USDT balance?"

What success looks like:

- **If it answers with an address and balance:** you are connected. 🎉
- **If it says you are not signed in:** the skill loaded correctly — go back to Step 6 and complete sign-in.
- **If it does not recognise the request at all:** the skill was installed in the wrong folder. Re-run the Step 5 command in the folder your agent is actually working in, then **restart the agent session** so it reloads its instructions.

Then try market data (Route A):

> "Show me the BTC/USDT order book top 5 bids and asks."

## Step 9 — Fund only what you are willing to expose

1. For trading: go to **Profile → Dashboard → Sub-account → Asset Management → Transfer** and move funds **into the Agentic sub-account**.
2. For on-chain: fund the **Agentic Wallet** from the Binance app.

The agent **cannot** move funds from your main account into the sub-account or wallet. Only you can. Fund it only with assets you are prepared to make available to agent activity.

## Step 10 — Know how to stop everything

- **Pause one agent:** Sub Accounts → Account Management → Disconnect Agents (pick the agent).
- **Stop all agents at once:** Emergency Stop.
- **End a wallet session:** tell the agent **"Sign out"** — this revokes the session. Do this on shared or temporary machines.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Agent doesn't recognise wallet requests | Skill installed in another directory | Re-run the Step 5 command in the folder your agent works in |
| `npx: command not found` | Node.js missing or too old | Re-do Step 2, then close and reopen the terminal |
| Install succeeds but nothing changes | Session started before install | Restart the agent session |
| Sign-in QR code expires before scanning | Link is short-lived | Ask the agent to sign in again for a fresh code |
| MCP listed but tools fail | Permissions not granted | Sub Accounts → Account Management, enable the missing scope |

## Next steps

- **[Hunting free mints with your agent](02-hunting-free-mints.md)** — the free-mint playbook: verify before minting, free-only, rarity before selling.
- **[Main guide](../README.md)** — the two routes, safety rules, and official sources.

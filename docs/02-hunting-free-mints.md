# Hunting Free Mints with Your Agent

Free mints are NFTs (or tokens) you can claim for **0 mint price** — you only pay the network gas fee. They are the cheapest way to build an on-chain collection, and occasionally one turns out to be rare and valuable. Most are worth little. This playbook is about doing it **safely, quickly, and without ever paying for a "free" mint**.

> **Honest framing first:** free mints are lottery tickets, not income. The method below keeps your cost at gas-only, keeps your main wallet out of it, and stops you from being the person who pays for a fake "free" mint.

## The rules (non-negotiable)

These are the rules that keep the whole activity safe. Break one and you are no longer hunting — you are gambling.

1. **FREE ONLY.** The mint price must be exactly **0**. If a mint costs anything beyond gas, skip it. No exceptions, no "just this once".
2. **AGENT WALLET ONLY.** Mints happen from your Binance Agentic Wallet (or a dedicated agent wallet) — **never** from your main wallet or a wallet holding real funds.
3. **VERIFY BEFORE MINTING.** Never mint from a link alone. Check the contract, the supply, and the mint function on-chain first (see below).
4. **GAS CAP.** Set a maximum gas cost you will accept (a small cap — for example, the equivalent of about **$0.10**). If gas is above your cap, skip the mint.
5. **SIMULATE FIRST.** If the transaction preview or simulation fails, looks wrong, or shows an unexpected token approval, stop.
6. **RARITY BEFORE SELLING.** Never list a minted item at the floor price blind. Check its traits and rarity rank first — a rare trait can be worth many times the floor.
7. **SOLD OUT MEANS MOVE ON.** If the mint is finished, do not chase it, do not pay secondary prices on impulse, and do not retry a failed mint blindly.
8. **NEVER TOP UP FOR A MINT.** If you run out of gas, wait. Do not move fresh funds in just to catch a mint — that is how a free mint quietly becomes a paid one.

## What you need before you start

- The [first-time setup](01-first-time-setup.md) completed: agent connected, Agentic Wallet signed in, wallet rules set (daily limit, token scope).
- A small gas balance in the Agentic Wallet on the mint's chain (for example, a little BNB on BNB Chain). This is the **only** money involved.
- A block explorer for the chain (for example, BscScan for BNB Chain, Etherscan for Ethereum, Basescan for Base).

## Step by step: one mint, done properly

### Step 1 — Find a candidate

Free mints surface through:

- Project announcements on X and Discord (follow the project's official account, not repost accounts).
- Agent and collector communities that share mint links.
- Mint calendars and launch trackers.

**Do not trust a mint link from a DM, a reply-guy, or a random forwarded message.** Go to the project's own announcement and confirm the link matches.

### Step 2 — Verify on-chain (before you mint anything)

Ask your agent to check, or check yourself on the explorer:

1. **Is it still open?** Read the contract's total supply vs. how many are minted. If minted ≥ supply, it is sold out — move on.
2. **Is the price really 0?** Read the mint function / sale config. The mint value must be 0. If the function takes payment, it is not a free mint.
3. **Is this the real contract?** Compare the contract address against the project's official announcement. If they do not match exactly, stop — a lookalike contract is the most common free-mint scam.
4. **What does the mint function do?** A clean free mint is a simple `mint()` call. Be suspicious of functions that ask for token approvals, delegate authority, or move other assets.
5. **What is the gas cost?** Estimate it. If it is above your gas cap, skip.

A good agent prompt for this step:

> "Check this mint for me: [link or contract address]. Is it still open, is the mint price really 0, and what is the estimated gas? Don't mint yet — report first."

### Step 3 — Mint (only if Step 2 is clean)

If everything checks out, tell your agent:

> "Mint it — free mint only, gas under my cap. If anything looks off, stop and tell me."

The agent should:

- Call the simple mint function with value 0.
- Keep the transaction to a single mint (not a batch) unless the project explicitly supports it.
- Show you the transaction hash before you consider it done.

### Step 4 — Confirm on-chain

After the transaction:

1. Check the transaction hash on the explorer — status should be **Success**.
2. Check the NFT actually arrived in your Agentic Wallet.
3. If the transaction failed, read the revert reason before retrying. A revert usually means the mint closed, the supply ran out, or you were not eligible. Do not hammer retries.

### Step 5 — Check rarity before you do anything with it

Before listing, selling, or even deciding to hold:

1. Look up the item's **traits** (the project's rarity tool, or a rarity site for that collection).
2. Check its **rank / frequency** — how rare is this trait combination?
3. Compare with recent sales of similar traits, not just the floor price.

**Never list on floor price alone.** A rare trait listed at floor is money left on the table, and a common item listed far above floor simply will not sell.

### Step 6 — Decide: hold or list

- **Hold** if: the project is active, the item has rare traits, or you believe in the collection.
- **List** if: you want the liquidity and the price (for *your* item's rarity, not the floor) is acceptable.
- **Do nothing** if: you are unsure. An unlisted item costs nothing to keep.

## The daily routine

Free-mint hunting rewards consistency, not obsession:

1. **Check a few times a day** for new announcements from projects you follow — morning, midday, evening is plenty.
2. **Keep a watch** on the mints you care about: supply remaining, closing time, and whether new ones open. Your agent can check these on a schedule and tell you only when something is actually open and free.
3. **Act fast, but never skip Step 2.** Speed matters because free mints sell out — but a skipped verification is how wallets get drained.
4. **Log what you minted** (project, contract, token ID, gas paid). It makes rarity checks and later sales much easier.

## Red flags — stop immediately if you see any of these

- A "free mint" page that asks you to **pay** anything, or to **approve unlimited spending** of a token.
- A contract address that **does not match** the project's official announcement.
- A mint link sent by **DM** or posted as a reply to a popular account.
- A "claim portal" for an airdrop or mint that you found through a search ad or a forwarded link. **Only use the project's official site or the official app.**
- A page that asks you to **connect your main wallet** or import a seed phrase. Never. The agent wallet is the only wallet that touches mints.
- A mint that requires you to **buy a token first** to be eligible. That is a paid mint wearing a free costume.

## What to ask your agent (copy-paste prompts)

**Verify a mint:**
> "Check this mint: [link]. Is it still open, is the mint price 0, is the contract the project's real one, and what's the gas estimate? Report before minting."

**Mint it:**
> "Mint one from [project] if it's free and gas is under my cap. Single mint only. Show me the transaction hash."

**Check what I own:**
> "List the NFTs in my Agentic Wallet from [project] and check the rarity of each."

**Check a sale price:**
> "Before I list token #X, check its traits and recent sales of similar traits. Don't list at floor blindly."

## Reality check

- Most free mints will be worth little or nothing. That is normal.
- The wins come from **volume + rarity**: minting many genuine free mints, checking rarity properly, and selling the rare ones at the right price.
- The losses come from **impatience**: paying for fake free mints, approving malicious contracts, or panic-buying after a mint sells out.
- Gas adds up. Track it. If your total gas spent is climbing past what your rare sales bring in, slow down.

## Next steps

- **[First-time setup](01-first-time-setup.md)** — if your agent is not connected yet.
- **[Main guide](../README.md)** — the two Binance routes, safety rules, and official sources.

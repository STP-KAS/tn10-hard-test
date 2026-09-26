# Grok Build pushback — 20 September 2026

**Writer:** Grok Build (Windows desk).  
**Not** tn10 bot. **Not** kaspa bot. **Not Kaspa core. Not an audit. Not a security credential.**

This GitHub stays [STP-KAS/tn10-hard-test](https://github.com/STP-KAS/tn10-hard-test). No third repo.

Farm / IBD / miner counters live in private [STP-KAS/tn10-grok](https://github.com/STP-KAS/tn10-grok). That journal mixed two voices until this pass labeled them.

tKAS has no value. No seeds.

---

## Who wrote what

| Voice | Machine | What it is allowed to mean |
| --- | --- | --- |
| **Grok Build** | this Windows desk | Catalog, unit tests, REST reads, desk kaspad if it is up. This GitHub (14 Sep pass + this file). |
| **tn10 bot** | Grok Bot Linux sandbox | TN10 node + CPU farm. RPC `127.0.0.1:16210` **on the sandbox**, not this PC. Private `tn10-grok` REVIEW / RECOVERY. |
| **kaspa bot** | Grok Bot Linux sandbox | Mainnet archival only. Public P2P. Never TN10. |

**This repo is Grok Build.** METHOD used to say “Grok (xAI) on stp’s Windows desk.” That is Build. It is not the 100–150 miner sandbox farm.

Windows `127.0.0.1:16210` is the **desk** TN10 node when it is running. Sandbox loopback is a different machine. Do not flatten them.

---

## What still holds from the 14 Sep pass

Rechecked this evening against api-tn10 + `gh api`. Not a re-run of every `npm test`.

| 14 Sep claim | 20 Sep Build |
| --- | --- |
| 1 sompi unconstructible (`Storage mass exceeds maximum`) | **Holds** as KIP-9 / classroom law. Not re-broadcast. |
| Payload tx `64057dd7…` accepted, UTF-8 `tn10-hard-test payload-check` | **Holds.** REST `is_accepted=true`, payload hex `746e3130…636b`. |
| Old journal `59b284…` accepted, `payload` **null** | **Holds.** |
| kns red X is a **comment grep**, not a hostile `readInputState` call | **Holds.** Same linter. |
| PegLab genesis is a **different** sponsor, not groks-wallet | **Holds.** Do not retell. |
| explorer-tn10.kaspa.org paused / 402 | **Holds.** Use [tn10.kaspa.stream](https://tn10.kaspa.stream/) + [api-tn10.kaspa.org](https://api-tn10.kaspa.org/). |
| Eight honest jobs, not “N products” | **Holds.** Live org is larger; most new GitHubs are reviews/docs. |
| HTTP 402 ≠ x402 v2 | **Holds.** Canonical envelope remains elldeeone/kaspa-x402. |
| Do not mix mainnet `:16111` and TN10 `:16211` | **Holds.** Do not paste TN10 into kaspa bot. |

---

## Pushback on this GitHub

### 1. Inventory **36** is a frozen snapshot

`GET /users/STP-KAS/repos?per_page=100&type=all` on 14 Sep → 36.  
Same call **20 Sep 2026** → **50 public**. Authenticated `GET /user/repos` → **52** owner repos (**2 private**: `tn10-grok`, `kns-kasware-tn10-test`).

`/users/{user}/repos` **drops private**. Use `/user/repos` when the operator says everything.

New public since the 36-row table (not products): `tn10-hard-test` itself, `kaspa-dapps`, `kns-dotk`, `dotk-review`, `kaspa.org-kaspaexplained`, `iziodev-build-a-kaspa-l1-grok-reveieuw`, `grok-heavy-showcase`, `Xai.mainnet.public.nodes`, `kns-kaspire-tn10-review`, `kusdt-bitcoffee`, `poc-revisited`, `staghunt-grok-review`, `three-x-reviews`, profile `STP-KAS`.

Do not update the 14 Sep table in place. Date-stamp it. That is what [INVENTORY.md](INVENTORY.md) does now.

### 2. “Keep inject kit” contradicts the disclaimer on this same GitHub

[INVENTORY.md](INVENTORY.md) row 31 and classroom step 7 said keep [wallet-integration](https://github.com/STP-KAS/wallet-integration).  
[DISCLAIMER.md](DISCLAIMER.md) already says Kasware / Kastle / in-page inject are **withdrawn**. Pay QR / `kaspa:` URI / paste txid. Never a seed.

**Build:** do not keep the kit. Tests-passing is not permission to clone inject.

### 3. LIVE.md ~300k tKAS is 14 Sep local RPC, not today’s locked pay-from

14 Sep local `balance.mjs`: ~300,543 tKAS / ~97k UTXOs on the mining receive.  
20 Sep api-tn10 on the **locked faucet pay-from** (same public address as groks-wallet README): **~4,068,352 tKAS** / **1,184,934** txs.

Sweep rule (farm folds into pay-from under 1M tKAS) still **does not fire**.

LIVE.md stays a 14 Sep card. Refresh from REST + local RPC; do not leave STATUS-style numbers in the README as if they were live.

### 4. Desk paths do not belong in a public report

METHOD and SOURCES named the desk username and the gitignored seed **path**. Username + layout is not a key, and it is still not for GitHub. Replaced with `LOCAL/…` this pass.

### 5. argent-xai “pins match freeze” did not stay true

14 Sep TESTS: `check.ps1` pass at silverscript v1.0.0 `3ed9733`.  
17 Sep master-file retest: **DRIFT** after Argent PR #63 (pin `867b080` vs live `e76ee07`). SilverScript tag itself still v1.0.0. Argent still **no tag**.

### 6. Public indexer is not one version string

20 Sep `GET /info/kaspad`: rusty **2.0.1**, `isSynced true`, mempool **3**.  
`GET /info/health` wrpc row: **2.0.0**. Do not quote a single “the indexer is 2.0.1” without the endpoint.

Network this evening: DAA **~575,978,838**; hashrate **~21.1 MH/s** (`/info/hashrate` is TH/s); tips **~2,039**; `blockCount = headerCount` **1,334,743**. 18 Sep journal had tips ~3.6k and mempool ~7.8k–10.9k. The DAG is quieter than the stress window. That is not a pin.

---

## Metric split (Build vs bot)

| Layer | Who | What it proves |
| --- | --- | --- |
| `Found a block` / `route is full` / `submit_ok` | tn10 bot farm logs | Work on **that** node’s submit route |
| Local `Accepted … via submit` | whichever kaspad you attached | That node stored the block. **Not** selected-parent on the public DAG. |
| api-tn10 balance / tx count / payload hex | Grok Build REST | Live DAG object |
| Clean-address coinbase | Grok Build | Measurable only if the mine-to was empty |

18 Sep desk pass already showed the gap: 10 local accepts during IBD, public REST **404**. High find count on a ~10–25 MH/s testnet is the expected CPU outcome, not a majority claim.

---

## Desk this evening (Build, not the sandbox)

Windows TN10 `kaspad` **v2.0.1** is **tip-following** (relay + submit mixed, bodies processing, ~9–11 blocks/s, ~48 u-tps). Miner **8 threads**, `grokstress`, **no** `--mine-when-not-synced`. Mine-to is an empty operator slot (not stored here).

That is **not** the sandbox farm. Last tn10-bot note in `tn10-grok`: datadir **wiped**, miners **0**, fresh IBD, planned 10 miners at rotation index 29. Build **cannot** see sandbox loopback from this PC. Do not report desk tip-follow as farm recovery.

---

## Agree / do not round up

**Agree (operator notes, not Core law):** gate mining on tip-following; `RouteIsFull` is backpressure; 1 sompi is not a TN10 output; payload claims need REST hex; PegLab will depeg; Luke’s envelope is the x402 binding; two networks, two bots; tKAS is toy.

**Do not round up:** 36 (or 50) GitHubs to products; local submit to coinbase; HTTP 402 to x402; wallet-integration tests to “keep inject”; sandbox wipe to desk state; “Grok” as one author.

Card: [kaspa-master-file DESK-BOT.md](https://github.com/STP-KAS/kaspa-master-file/blob/main/DESK-BOT.md).

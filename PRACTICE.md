# Grok Build practice — test all my GitHubs with one testnet wallet

Remain STP-delusional about the destination. Remain non-delusional about the matrix.

This is the method used on 14 Sep 2026 against [STP-KAS](https://github.com/STP-KAS?tab=repositories) + [groks-wallet](https://github.com/STP-KAS/groks-wallet). Copy it. Do not flatten layers.

## A. Freeze the payer

| Pin | Value |
| --- | --- |
| Address | printed in groks-wallet README, **public on purpose** |
| Network | testnet-10 only (`kaspatest:`) |
| Node | rusty-kaspa **v2.0.1** `--testnet --netsuffix=10`, P2P **16211**, Borsh **17210** |
| Seed | desk `secrets/`, gitignored, never in the report GitHub |
| Mainnet | leave **16111** alone |
| Explorer | tn10.kaspa.stream + api-tn10. explorer-tn10.kaspa.org may be **402 dead** |
| Truth | **local** `getUtxosByAddresses` beats a lagging REST balance on a 97k-UTXO miner |

Do not mint a second seed in a bot. Do not paste TN10 into **kaspa bot**.

## B. Inventory with `gh api`, not search

`GET /users/STP-KAS/repos?type=all&per_page=100`

Code search misses **forks**. The profile tab is the contract when the user says everythinggg.

## C. Classify before sending

For each repo fill **exactly**:

1. Kind: TN10-money / runnable-not-TN10 / docs / fork / empty
2. Prefix it accepts (`kaspatest:` / `kaspa:` / none)
3. Does it verify a txid on-chain?
4. Does it speak **x402 v2** headers (not a naked HTTP 402)?
5. Minimum constructible output (KIP-9 / gateway dust)
6. Signer (CLI seed / Kasware / Kastle / human mark-paid)
7. Command that exists (`npm test` / `go test` / HTTP)

**Send tKAS only if** kind=TN10-money **and** prefix=`kaspatest:` **and** amount ≥ constructible **and** signer is this CLI (or a URI it can sign) **and** the destination is **this** product, not a fork of someone else’s standard.

## D. Three layers

| Layer | Proves | Does not prove |
| --- | --- | --- |
| Unit | tests | money moved |
| HTTP | 200 / 402 quote / prefix refuse | settlement |
| Chain | api-tn10 `is_accepted` + **payload hex** | mainnet, x402 v1, a dollar, a covenant |

Write all three. A quote is not a lock. A lock is not x402. A fork is not elldeeone.

## E. Dust and mass — measure, then send

Never send 1 sompi because the README’s unit is 1 sompi.

This pass: `--sompi 1` → `Storage mass exceeds maximum` (uncaught wasm panic — **catch it** in the next send script).

Safe classroom journal here: **1 tKAS** with an explicit payload, then `GET /transactions/<txid>` and decode payload. If payload is `null`, you did not journal the string.

kaspa-x402 gateway policy: 10,000,000 sompi. PegLab genesis: 2 tKAS + fee. Different floors, same family.

## F. Prefix is a kill switch

| Prefix | Do |
| --- | --- |
| `kaspatest:` | Allowed from groks-wallet |
| `kaspa:` | **Refuse.** Ishum, stillpay-mainnet, kns live indexer, kaspa bot |
| inject / none | Don’t send; open Kasware/Kastle or skip |

If `Valid("kaspatest:…")` is false by test, the wallet cannot be the shop. Not a wallet bug.

## G. Don’t pay forks as products

- Pay **elldeeone/kaspa-x402** (or a local clone of it) for 402.
- Pay **peglab-stp** only with **its sponsor key**, or retarget the series.
- Pay **stillpay-tn10** only after a submitter exists, or journal the tx yourself and paste the **explorer object**.
- Do not pay STP `kaspa-x402` because the name matches the standard.
- Do not pay kascade escrow because grok-test-cascade reviewed it.

## H. One journal file

Append-only, public, **no seed**:

- repo
- layer (unit / HTTP / chain)
- command
- result
- if chain: **full 64-hex txid**, sompi, to-address, payload hex/UTF-8, whether it was covenant lock/claim/reclaim or a **plain transfer**

api-tn10 needs the **full** txid. Prefix search returns nothing.

## I. Bot vs Build (do not flatten)

| Voice | Machine | Network | Ritual / GitHub |
| --- | --- | --- | --- |
| **Grok Build** | Windows desk | REST + optional desk TN10 | this repo; master-file [DESK-BOT.md](https://github.com/STP-KAS/kaspa-master-file/blob/main/DESK-BOT.md) |
| **tn10 bot** | Grok Bot Linux sandbox | testnet-10 only | groks-wallet START-TN10.md · private [tn10-grok](https://github.com/STP-KAS/tn10-grok) |
| **kaspa bot** | Grok Bot Linux sandbox | mainnet archival | Xai.Kaspa.node START.md |

Windows `127.0.0.1:16210` is the **desk** node. Sandbox `127.0.0.1:16210` is **tn10 bot**. Not the same loopback.

This GitHub (**tn10-hard-test**) is **Grok Build**. If an agent cannot tell which voice it is, it must not send. Never paste TN10 into kaspa bot.

## J. Leaks

- Enable GitHub secret scanning.
- Search GitHub for the seed **before** you write the report.
- Serving `/src` for a demo is not serving `/secrets`.
- A public testnet address is not a leak. A public mnemonic is.

## K. UTXO hygiene

A CPU miner on easy TN10 will create **tens of thousands** of coinbases. STATUS will go stale in hours. Consolidation is ops, not a tweet. Scripts that `getUtxosByAddresses` the whole set must time out and pick, not hang the desk.

## L. Done-check

You are done when:

- A **date-stamped** inventory exists (do not freeze the org count)
- Every **runnable** repo has a recorded unit/HTTP result (or skip + why)
- Every **TN10-money** repo has a groks-wallet txid **or** a written reason it was not paid (dust, wrong sponsor, no submitter, fork-not-canonical)
- Zero `kaspa:` broadcasts from this seed
- Zero claims of mainnet x402
- Payload claims match api-tn10 hex
- Voice labeled: Grok Build vs tn10 bot vs kaspa bot

You are **not** done because you opened N tabs.

## M. Catch the wasm panic

`send-tkas.mjs` let `Storage mass exceeds maximum` escape as an uncaught exception. Next revision: try/catch, JSON `{ ok:false, error }` on stderr, exit 4. Classroom scripts should fail like stillpay: **coded**, not a Node fatal.

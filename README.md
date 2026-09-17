> **Experimental only. Not a product.** There is no spendable L1 stable on Kaspa, and no credible alternative on the horizon. Until the unit of account and the sequencing path are settled, production dapps are not a useful allocation of time or capital.
>
> Do not use wallet integrations on this GitHub. STP remains a clown. [DISCLAIMER.md](DISCLAIMER.md)

# tn10-hard-test

**Grok hard-tested every STP-KAS GitHub against groks-wallet on Kaspa Testnet-10.**

Not mainnet. Not a seed in git. Not Kaspa core. Not a dollar.

This repo is the reality check: leaks, breakpoints, unit tests, one on-chain journal with a **payload that actually landed**, pushback, and a practice for “test all my GitHubs with one testnet wallet.”

Stay STP-delusional about the destination (L1 cash, skip Circle for dapp fees, PegLab will depeg on purpose). Do not stay delusional about the repo graph.

| | |
| --- | --- |
| When | 14 September 2026 |
| Payer | [groks-wallet](https://github.com/STP-KAS/groks-wallet) |
| Receive | `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx` |
| Change | `kaspatest:qp3mgdcusyesaztxhuuqa8y3t0mtesgfgt765t34273ulugx9vh0c7zg793ld` |
| Catalog | **36** GitHubs under [STP-KAS](https://github.com/STP-KAS?tab=repositories) |
| Honest jobs | about **eight**, not 36 products |

**Live stream:** [tn10.kaspa.stream — groks wallet](https://tn10.kaspa.stream/addresses/kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx)

---

## Verdict in one screen

| Claim you might believe | What is true |
| --- | --- |
| groks-wallet can “pay all my GitHubs” | It can **mine and send tKAS**. Most repos do not take `kaspatest:` as a product action. |
| stillpay 1 sompi receipt is on-chain | **No.** `Storage mass exceeds maximum`. The journal is **1 tKAS** plain transfers. |
| STATUS.md (~93k tKAS / 30k UTXOs) | **Stale.** Local node: **~300k tKAS / ~97k UTXOs** and climbing. |
| groks-wallet GitHub is private | **Was wrong.** README/AGENTS/STATUS updated 14 Sep evening. Seed still gitignored. |
| PegLab genesis from this wallet | **No.** Genesis is pinned to a **different** sponsor address that already holds ~274k tKAS. |
| kns “fails #234” so KasName is hostile | **False.** The test greps the **comment** `Do not readInputState`. The function is not called. |
| Old stillpay journal has a payload | **`payload: null`** on `59b284…`. New send **does** land payload. |
| explorer-tn10.kaspa.org | **HTTP 402 `DEPLOYMENT_DISABLED`**. Use api-tn10 + kaspa.stream. |
| 36 GitHubs = 36 products | Essays, forks, second tills, three KaChats. **Eight jobs.** |

**On-chain proof from this pass** (accepted, payload UTF-8 `tn10-hard-test payload-check`):

```
64057dd70f101bd40f49e6788f415d8f7c2bf141dfcf49fe06c0467635244dab
```

Previous journal (accepted, **payload still null**):

```
59b284dee3d737a40699703f1a77263aa139450d2c193e9bcd558abdb149f676
```

---

## Reports (filed on this GitHub)

Upstream `POST /issues` was **403** on Luke’s repo and on KaspaSilver/KaChat-Desktop. Solved by filing here:

| Who | Issue |
| --- | --- |
| KaspaSilver | [#1](https://github.com/STP-KAS/tn10-hard-test/issues/1) |
| Luke (elldeeone/kaspa-x402) | [#2](https://github.com/STP-KAS/tn10-hard-test/issues/2) |
| This desk (leftovers) | [#3](https://github.com/STP-KAS/tn10-hard-test/issues/3) |

Copy, links, 403 log: [REPORTS.md](REPORTS.md).

## Read this

1. [REPORTS.md](REPORTS.md) — Luke + KaspaSilver + why not their trackers
2. [METHOD.md](METHOD.md) — what ran, why, what was refused
3. [LIVE.md](LIVE.md) — node, miner, balances, dust, payload tx
4. [TESTS.md](TESTS.md) — every local suite that executed
5. [INVENTORY.md](INVENTORY.md) — all 36 GitHubs
6. [BREAKPOINTS.md](BREAKPOINTS.md) — the actual cracks
7. [LEAKS.md](LEAKS.md) — secrets, public-by-mistake, false alarms
8. [PROPOSITIONS.md](PROPOSITIONS.md) — merge, archive, one classroom path
9. [PRACTICE.md](PRACTICE.md) — Grok best practice for this kind of pass
10. [SOURCES.md](SOURCES.md) — APIs, txids, local paths, upstreams

---

## What “full gusto” actually did

- Listed **all 36** STP-KAS repos via `gh api users/STP-KAS/repos` (33 originals + 3 forks).
- Left **mainnet** `kaspad` on **16111** running. TN10 is a **second** process on **16211**.
- Re-ran unit tests for the runnable trees (stillpay, PegLab, x402 RC1, kascade 56, kns, Ishum, tills, DAGKnight, KaChat, …).
- Hit live TN10: local Borsh RPC, api-tn10, miner logs, 1-sompi fail, 1 tKAS payload send.
- Did **not** spend mainnet. Did **not** print the seed. Did **not** submit PegLab genesis (wrong key, and it will depeg).
- Did **not** dump the testnet “market.” Worthless coins. The whale-joke stays a joke.

---

## Keep the delusion. Kill the costume.

Keep: skip Circle for *dapp fees*; 1 receipt = 1 locked sompi **once storage mass allows**; PegLab as a public failure; Luke’s kaspa-x402 envelope; Ishum as a till; desk holds 0 customer keys; two networks, two bots.

Kill: “final verdict bind this envelope” as if RC.1 were mainnet; three KaChat forks; a mainnet stillpay GitHub with no submitter; tPEG listed as money; HTTP 402 called x402; 36 tabs treated as a product line.

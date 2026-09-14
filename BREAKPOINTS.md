# Breakpoints

Ordered by how much they can lie to you.

## 1. Teaching unit vs constructible output

stillpay, peglab-poc, and the classroom story: **1 receipt = 1 locked sompi**.

Live:

```
Storage mass exceeds maximum
```

KIP-9 storage mass makes a 1-sompi output fail in the wasm constructor. kaspa-x402 documents a **10,000,000 sompi** gateway floor for the same reason. PegLab genesis wants **2.01 tKAS**.

**Fix the tin:** journal a storage-mass-safe lock, or stop calling 1 sompi the on-chain unit. ENGINE_SPEC arithmetic can stay 1:1. The chain cannot.

## 2. UTXO explosion

CPU miner → one coinbase per accepted submit → receive address.

| When | UTXOs | tKAS |
| --- | ---: | ---: |
| STATUS.md 17:46 | 30,088 | ~93,141 |
| This pass, local RPC | **97,047–97,110** | **~300,543–300,737** |

Spend still worked (picker takes the **largest** UTXO, not the whole set). REST `/utxos` is a **37 MB** dump or **422**. api-tn10 **balance lags**.

This will eventually hurt: wallet restore, explorers, `getUtxosByAddresses` on weaker RPC, any script that consolidates naively.

**Fix:** consolidate on a schedule (storage-mass-safe chunks), or mine to a dedicated address and sweep. Do not treat 97k UTXOs as a flex.

## 3. Payload claimed vs payload on the tx

| txid | accepted | payload |
| --- | --- | --- |
| `59b284dee3d737a40699703f1a77263aa139450d2c193e9bcd558abdb149f676` | yes | **null** |
| `64057dd70f101bd40f49e6788f415d8f7c2bf141dfcf49fe06c0467635244dab` | yes | **`tn10-hard-test payload-check`** |

`REPORT.md` talked as if the first journal carried `stillpay-tn10 groks-wallet 1-sompi receipt`. The explorer object does not. The second send proves the API **does** return native payload.

**Fix:** journal only what `GET /transactions/<txid>` shows. Never upgrade a local `--payload` flag to “on-chain” without the hex.

## 4. Docs say private / 93k; GitHub is public / 300k

- `AGENTS.md`: groks-wallet is **private**. GitHub API: `private=false`.
- `STATUS.md`: ~93k tKAS / 30k UTXOs. Live: ~300k / 97k.
- Local `Documents\kaspa\groks-wallet` is **not a git repo**. Push tree is `groks-wallet-push`. Easy to edit the live folder and think GitHub updated.

**Fix:** STATUS is a live card — regenerate from `balance.mjs`. AGENTS.md must say **public**. One folder, one remote.

## 5. One wallet cannot genesis PegLab

`peglab-stp/src/network.mjs` pins:

```
SPONSOR_ADDRESS = kaspatest:qzpvdakagvwfm95g8pv9ndpupjtndgjfhmve08cg3tv5wgfytjzf7cudwwzv0
MINING_ADDRESS  = kaspatest:qqup3k4ru5uhj9swa05afa3zqcwkyhtv9vz9dme68cglza73mc5yk4r7an5cj
```

Those addresses already hold **~274k** and **~104k** tKAS. groks-wallet is a third whale. Dry-run genesis compiles and picks a sponsor UTXO. `--submit` needs `PEGLAB_SPONSOR_KEY`, not groks `wallet.txt`.

**Fix:** either retarget genesis at groks-wallet (new series, new sponsor x-only) or stop saying “use grok wallet to genesis PegLab.”

## 6. kns “#234 fail” is a grep of a comment

`KasName.sil` line 13:

```
// Do not readInputState a foreign covenant (silverscript#234, unmerged;
```

`attack_test.go` does `strings.Contains(s, "readInputState")` on every non-`FORBIDDEN-*.sil` file. Comments count. `FORBIDDEN-ForeignTokenVault.sil` is supposed to contain the call.

The covenant uses `validateOutputState` and locks continuation value. House rule is still right. The red X is a linter bug.

**Fix:** skip comments, or match `readInputState(` as a call.

## 7. HTTP 402 is not x402

| Surface | What it is |
| --- | --- |
| stillpay `stillpay-quote-v1` | Unsigned classroom 402. Not v2 headers. |
| kns `/api/v1/call` 402 | Costume |
| Gramlane `X-Kaspa-Payment` | HTTP layer; jar is `ledger.json` |
| explorer-tn10.kaspa.org **402** | Cloudflare/deployment disabled, irony |
| elldeeone kaspa-x402 RC.1 | **Actual** x402 v2 binding, `kaspa:testnet-10` |

Calling all of these “x402” is how Discord gets a fake standard.

## 8. Network prefix is a kill switch

| Repo | Prefix | groks-wallet |
| --- | --- | --- |
| stillpay-tn10, peglab-stp | `kaspatest:` | quote / classroom |
| stillpay-mainnet, ishum, kns live indexer, Xai.Kaspa.node | `kaspa:` | **refuse** |
| KaChat / wallet-integration | Kasware/Kastle inject | CLI seed is the wrong signer |

Ishum `addr.Valid` requires `kaspa:`. That is honesty.

## 9. Forks are not the product

| STP-KAS name | Upstream |
| --- | --- |
| kaspa-x402 | elldeeone/kaspa-x402 |
| rusty-kaspa | kaspanet/rusty-kaspa (desk runs **release v2.0.1**, not this fork) |
| kachat-test-with-silver | KaspaSilver/KaChat-Desktop |

Paying the fork because the name matches the standard is a breakpoint in the brain, not the chain.

## 10. Timeout `.sil` does not lock output value

stillpay tests say it explicitly: “refuses skim in JS only (the `.sil` does not).” JS ENGINE_SPEC is not SCRIPT_ENFORCED. A live lock/claim/reclaim journal does not exist for STP’s series.

## 11. Compiler pin drift

argent-xai freeze: silverscript **v1.0.0** `3ed9733`.  
project-delusional / peglab-stp READMEs still talk **v1-rc1** / “as of 5 Sep 2026.”

A stale pin on the classroom that is allowed to fail is how you compile the wrong bytecode.

## 12. Explorers and faucets

- faucet-tn10: **403**
- explorer-tn10.kaspa.org: **402 DEPLOYMENT_DISABLED**
- You cannot “look it up on the official TN10 explorer” today. api-tn10 + kaspa.stream.

## Non-breakpoints (do not file as bugs)

- PegLab depegs. That is the deliverable (`KNOWN-BREAKS.md`, tests 16/16).
- stillpay serving `/src/*.mjs`. Demo imports.
- Public mining address. Intentional.
- Mainnet node on 16111 while TN10 mines. Correct split.
- kascade not being a CDN. Already the grok-test-cascade verdict; do not re-litigate as a leak.

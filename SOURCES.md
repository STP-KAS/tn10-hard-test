# Sources

Nothing here is a seed.

## GitHub (this desk)

- Catalog: https://github.com/STP-KAS?tab=repositories
- Payer: https://github.com/STP-KAS/groks-wallet
- Prior classification: groks-wallet `REPORT.md` / `STATUS.md` (14 Sep 2026, **stale numbers**)
- This report: https://github.com/STP-KAS/tn10-hard-test
- Issues: [#1 Silver](https://github.com/STP-KAS/tn10-hard-test/issues/1) · [#2 Luke](https://github.com/STP-KAS/tn10-hard-test/issues/2) · [#3 desk](https://github.com/STP-KAS/tn10-hard-test/issues/3)
- Sister issues: [kaachat-desktop#1](https://github.com/STP-KAS/kaachat-desktop/issues/1) · [grok-heavy-test#1](https://github.com/STP-KAS/grok-heavy-test/issues/1)

`gh api users/STP-KAS/repos?per_page=100&type=all` — 36 repos (33 + forks `kaspa-x402`, `rusty-kaspa`, `kachat-test-with-silver`).

Authenticated as `STP-KAS` (GitHub user id 227352643).

## Chain / HTTP

| What | URL |
| --- | --- |
| Receive stream | https://tn10.kaspa.stream/addresses/kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx |
| Balance (sompi) | https://api-tn10.kaspa.org/addresses/kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx/balance |
| Health | https://api-tn10.kaspa.org/info/health |
| BlockDAG | https://api-tn10.kaspa.org/info/blockdag |
| Payload tx | https://api-tn10.kaspa.org/transactions/64057dd70f101bd40f49e6788f415d8f7c2bf141dfcf49fe06c0467635244dab |
| Old journal | https://api-tn10.kaspa.org/transactions/59b284dee3d737a40699703f1a77263aa139450d2c193e9bcd558abdb149f676 |
| Faucet | https://faucet-tn10.kaspanet.io → 403 |
| explorer-tn10 | https://explorer-tn10.kaspa.org → 402 DEPLOYMENT_DISABLED |

Local RPC: `127.0.0.1:17210` Borsh, network `testnet-10`, kaspad **2.0.1**.

## Txids (full 64 hex; prefixes do not resolve)

| txid | What |
| --- | --- |
| `64057dd70f101bd40f49e6788f415d8f7c2bf141dfcf49fe06c0467635244dab` | 1 tKAS receive→change, payload `tn10-hard-test payload-check`, accepted |
| `59b284dee3d737a40699703f1a77263aa139450d2c193e9bcd558abdb149f676` | prior 1 tKAS journal, accepted, **payload null** |

## Local trees

- `C:\Users\<user>\Documents\kaspa\groks-wallet` — node, miner, secrets (not git)
- `C:\Users\<user>\Documents\kaspa\groks-wallet-push` — git remote for groks-wallet
- `C:\Users\<user>\stillpay-tn10`, `stillpay-mainnet`, `peglab-stp`, `peglab-poc`
- `C:\Users\<user>\src\kaspa-x402` — STP fork checkout
- `C:\Users\<user>\grok-test-cascade-work\kascade`
- `C:\Users\<user>\kns`, `kns-spec`
- `C:\Users\<user>\Documents\kaspa\ishum`, `superapp` (gramlane), `superappstablesalternative` (till)
- `C:\Users\<user>\dagknight-test-grok`
- `C:\Users\<user>\wallet-integration`, `kaachat-desktop`

## Upstream (not STP originals)

- kaspa-x402 standard: https://github.com/elldeeone/kaspa-x402 (RC.1, `kaspa:testnet-10`)
- rusty-kaspa: https://github.com/kaspanet/rusty-kaspa (desk binary v2.0.1)
- KaChat: https://github.com/KaspaSilver/KaChat-Desktop
- silverscript v1.0.0 pin: `3ed973335b59` (argent-xai freeze)
- silverscript #234: https://github.com/kaspanet/silverscript/pull/234 (closed unmerged)
- kascade review target: https://github.com/kaspahttp402/kascade
- x402 v2 specs: https://github.com/x402-foundation/x402
- Kaspa Toccata docs: https://github.com/kaspanet/docs/tree/main/content/docs/toccata

## What this pass is not

- Not a security audit of elldeeone, kaspanet, or KaspaSilver.
- Not mainnet-readiness for kaspa-x402.
- Not a claim that tPEG, GRAM, or kUSD is money.
- Not a dump of TN10.

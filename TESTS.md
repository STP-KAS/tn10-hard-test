# Tests that actually ran

Commands executed on this desk, 14 September 2026. No source edits. No mainnet broadcast.

| Repo / tree | Command | Result |
| --- | --- | --- |
| stillpay-tn10 | `npm test` | **16 pass / 0 fail** |
| stillpay-tn10 | HTTP `:8771` GET `/` | **200** |
| stillpay-tn10 | GET `/server/serve.mjs`, `/.git/config` | **403** |
| stillpay-tn10 | GET `/src/network.mjs` | **200** (allowlist: demo engines) |
| stillpay-tn10 | `assertAddress(groks)` / `kaspa:` | **ok** / `WRONG_NETWORK` |
| stillpay-tn10 | live `paymentRequired` 1 sompi | **402** `stillpay-quote-v1` |
| stillpay-mainnet | `npm test` | **16 pass** (refuses `kaspatest:`) |
| peglab-stp | `npm test` | **16 pass** (includes advertised depeg) |
| peglab-stp | HTTP `:8765` | **200** |
| peglab-stp | `node server/submit-genesis.mjs` (no `--submit`) | **review ok**, sponsor ≠ groks-wallet |
| peglab-poc | `npm test` | **14 pass** |
| wallet-integration | `npm test` | **16 pass** |
| kaachat-desktop | `npm test` | **9 pass** |
| kaspa-x402 (local `src\kaspa-x402`, STP fork of elldeeone) | `npm test` (build + workspaces + examples) | **EXIT 0** — core 163, covenant 27, server 214, client 124, facilitator 36, CLI 6, demo-gateway 107, scripts 18 |
| kascade (`grok-test-cascade-work\kascade`) | `npm test` | **56 pass / 0 fail** |
| kns | `go test ./...` | **FAIL** `TestContractSourcesDoNotReadForeignState` — comment grep (see BREAKPOINTS) |
| kns-spec | `go test ./...` | **pass** |
| kaspa-data-vault (local only, **not** in the 36 GitHubs) | `go test ./...` | **pass** (`internal/vault`) |
| ishum | `go test ./...` | **pass** |
| kaspa-till (`Documents\kaspa\superappstablesalternative`) | `go test ./...` | **pass** |
| gramlane (`Documents\kaspa\superapp`) | `go test ./...` | **pass** |
| xai-reasoning-3 | `go test ./...` | **pass** |
| grok-kaspa-collab/desk | `go test ./...` | **pass** |
| dagknight-test-grok | `cargo test` | **8 pass / 0 fail** |
| argent-xai | `powershell -File check.ps1` | **pins match freeze** (silverscript v1.0.0 `3ed9733`) |
| groks-wallet | `node scripts\balance.mjs` | synced, **97047 UTXOs**, 300543 tKAS |
| groks-wallet | `send-tkas --sompi 1` | **FAIL** `Storage mass exceeds maximum` |
| groks-wallet | `send-tkas --sompi 100000000 --payload tn10-hard-test payload-check` | **txid `64057dd7…` accepted, payload on api-tn10** |
| grok-test-cascade/follow-up | `npm test` | **pass** |
| ishum HTTP `:8090` (already up; not `:8092`) | GET `/pos` `/store` | **200** |
| ishum POST store `payTo=kaspatest:…` | HTML error, no save | **refused:** pay-to must be mainnet `kaspa:` |
| kachat-test-with-silver | `npm test` | **skip** — no `test` script |
| mix-club (local; GitHub is mixer-concept) | `npm test` | **fail** missing script; suite is `npm run check` (not run) |
| sixpack.wtf / gramlanepeglab | — | **skip** static |

## Docs / empty / no `test` script

No binary test for: `ok` (empty repo, Git 409), `402-is-not-x402`, `x402-vs-grok`, `x402-ishum`, `delusional-stp-grok-mix`, `grok-heavy-test`, `feedback-stp-delusional`, `kaspa-master-file`, `project-delusional`, `windows-p2p-node-guide`, `Xai.Kaspa.node`, `sixpack.wtf` (static host; local `serve.mjs` not re-run this pass), `mixer-concept`, `kaspaexplained-delusional-stp`, `gramlanepeglab`.

Those were **read and classified**, not paid.

## Not run this pass (and why)

| Thing | Why |
| --- | --- |
| kaspa-x402 **funded live proof** | Needs adapter env + 30 selected-chain conf + min outputs; RC1 unit/examples already green; do not confuse with mainnet |
| Ishum HTTP `:8092` | Process not listening; `addr.Valid` already refuses `kaspatest:` in unit tests |
| KaChat handshake with Kasware | Inject wallet, not this CLI seed |
| `rusty-kaspa` rebuild | Desk runs **v2.0.1 release** `kaspad.exe`, not the STP fork |
| `kachat-test-with-silver` `npm test` | Fork of Silver; desktop copy already 9/9 |
| PegLab `--submit` | No sponsor key file; will depeg; not groks-wallet |

## How to read a green suite

`npm test` on stillpay does **not** mean a sompi locked.  
`npm test` on kaspa-x402 does **not** mean `demo.kaspa-x402.org` took this wallet.  
`cargo test` on dagknight-test-grok does **not** mean DAGKnight is on mainnet (it is not; GHOSTDAG is).

# What I did, and why

Operator: Grok (xAI) on STP-KAS’s Windows desk.  
Ask: use groks-wallet, test **everything** under https://github.com/STP-KAS?tab=repositories on testnet, find leaks and breakpoints, reality-check, push back, propose, then make a GitHub of it.

## Why this method

A wallet cannot “test a GitHub.” A wallet can:

1. Be the **wrong network** for that GitHub (`kaspa:` vs `kaspatest:`).
2. Sign a **plain transfer**.
3. Sign a **covenant** the GitHub actually compiles.
4. Or do **nothing**, because the GitHub is an essay.

So the pass is a **matrix**, not a spray of tKAS. Sending coins into a docs repo proves nothing. Skipping a live TN10 send on the one repo that claims 1 sompi would be theater.

## Steps

### 1. Identify the payer

- Repo: [STP-KAS/groks-wallet](https://github.com/STP-KAS/groks-wallet)
- Receive (mining): `kaspatest:qzffl5xy9np46gkttyuftqnv2w04pr8g3wsp7c3vv8se3txtelx6q7c0v0ldx`
- Change: `kaspatest:qp3mgdcusyesaztxhuuqa8y3t0mtesgfgt765t34273ulugx9vh0c7zg793ld`
- Seed: `C:\Users\<user>\Documents\kaspa\groks-wallet\secrets\wallet.txt` — **read only by send/balance scripts, never copied into this repo**
- Local tree is **not a git checkout**. GitHub is pushed from `Documents\kaspa\groks-wallet-push`.

### 2. Inventory

`gh api users/STP-KAS/repos?per_page=100&type=all` → **36** repos.

GitHub code search `user:STP-KAS` only sees **33**; it drops the three **forks**: `kaspa-x402`, `rusty-kaspa`, `kachat-test-with-silver`. The profile tab shows 36. Use `gh api`, not search, when the user says everything.

Authenticated user: `STP-KAS` (id 227352643).

### 3. Do not mix Kaspas

| Process | PID (this pass) | Ports | Network |
| --- | --- | --- | --- |
| `kaspad` | 31088 | P2P 16211, gRPC 16210, Borsh 17210, JSON 18210 | **testnet-10** |
| `kaspad` | 32924 | P2P **16111** | **mainnet** (left alone) |
| `kaspa-miner-v0.2.7` | 33728 | → 127.0.0.1:16210 | TN10, 8 threads, ~11 MH/s |
| PegLab serve | 51020 | :8765 | classroom UI |

Why: a second bind on 16111, or pasting TN10 into **kaspa bot**, is how you brick a datadir. [Xai.Kaspa.node](https://github.com/STP-KAS/Xai.Kaspa.node) stays mainnet. This wallet stays TN10.

### 4. Three layers, never flattened

| Layer | Tool | Proves |
| --- | --- | --- |
| Unit | `npm test` / `go test` / `cargo test` / `check.ps1` | Code paths |
| HTTP | loopback GET, 402 quote, prefix refuse | The demo is up |
| Chain | wasm SDK → local 17210, then `GET api-tn10/.../transactions/<txid>` | Money moved |

A 402 JSON object is not a txid. A txid without a payload is not the payload you claimed. A payload on a **plain transfer** is not a timeout covenant.

### 5. Live chain probes (TN10 only)

- Local: `node Documents\kaspa\groks-wallet\scripts\balance.mjs` (Borsh `getUtxosByAddresses`)
- Public: `https://api-tn10.kaspa.org/addresses/<addr>/balance`
- Health: `https://api-tn10.kaspa.org/info/health` and `/info/blockdag`
- Dust: `node scripts\send-tkas.mjs --sompi 1` → expect storage-mass fail
- Payload: `--sompi 100000000 --payload "tn10-hard-test payload-check"`
- stillpay: `assertAddress` + `makeQuote` / `paymentRequired` (no wasm submitter in that repo)
- PegLab: `node server/submit-genesis.mjs` **without** `--submit`

### 6. Leak scan (no values in git)

- GitHub code search: mnemonic, `receive-0-private-key`, `wallet.txt`, `ghp_`, `BEGIN PRIVATE KEY` → **0 hits**
- `github__list_secret_scanning_alerts` on groks-wallet → **404, scanning disabled**
- `git ls-files` on groks-wallet-push → no secrets
- stillpay HTTP allowlist: `.git` and `/server/serve.mjs` 403; `/src/*.mjs` **200 by design** (demo ES modules)

### 7. What was refused, on purpose

| Action | Why not |
| --- | --- |
| Print mnemonic / private key | This report is public |
| Mainnet send | This wallet is TN10 |
| Stop mainnet node | Public 16111 stays up |
| PegLab `--submit` | Wrong sponsor key; toy **will depeg** |
| 1-sompi on-chain receipt | Consensus/storage mass will not construct it |
| Pay Ishum as the shop | `addr.Valid` requires `kaspa:` |
| Pay STP `kaspa-x402` as “the standard” | Canonical is elldeeone; STP copy is a fork |
| Dump TN10 | Joke in groks-wallet README. Worthless coins. Not the work. |

## Why a new GitHub

groks-wallet `REPORT.md` already classified the 36 once, at ~5k–93k tKAS, with a **null-payload** journal. This pass:

- Re-ran tests after the wallet became a **~300k tKAS / ~97k UTXO** object
- Proved 1 sompi is **unconstructible**
- Landed a **payload** so the old `payload: null` is not “the API is blind”
- Corrected “PegLab genesis from groks-wallet” (it is a **different** sponsor)
- Corrected “kns fails #234” (comment grep)
- Wrote the practice so the next Grok does not flatten quote / unit / chain

STATUS.md and AGENTS.md in groks-wallet are now known-stale. This repo is the 14 Sep evening snapshot, not a live card. Refresh numbers from api-tn10 + local `balance.mjs`.

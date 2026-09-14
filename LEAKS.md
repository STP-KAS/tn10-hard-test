# Leaks

No mnemonic, private key, or GitHub token is written here. If a path is named, the **value is not**.

## Critical (spend keys) — none found in GitHub

| Check | Result |
| --- | --- |
| code search `mnemonic` / `receive-0-private-key` / `wallet.txt` `user:STP-KAS` | **0** |
| code search `ghp_` / `BEGIN PRIVATE KEY` / `sk-` / `xai-` `user:STP-KAS` | **0** |
| `git ls-files` on `groks-wallet-push` | no `secrets/`, no `*.kpk`, no `wallet.txt` |
| Local `Documents\kaspa\groks-wallet\secrets\` | present on disk, **gitignored** in the published tree; local folder is **not even a git repo** |
| GitHub secret scanning on groks-wallet | **disabled** (API 404). Enable it. |

Public mining address is **not** a leak. It is the product of a testnet classroom wallet.

## High

| Finding | Why it matters |
| --- | --- |
| groks-wallet is **public** while AGENTS.md says **private** | People will clone it expecting no address history. Address is already on kaspa.stream. Seed is still off git. The *intent* leaked: the README reads like an ops runbook for a desk node. That is fine **if** you mean it to be public. Say so. |
| Secret scanning **off** | The one repo that talks about `secrets\wallet.txt` should have scanning **on**. |
| PegLab / stillpay `.local/sponsor.json` pattern | Gitignored. Confirm it never landed in history (`git log --all -- .local`). Dry-run this pass: file **missing**. Good. |

## Medium

| Finding | Notes |
| --- | --- |
| stillpay serves `/src/*.mjs` and `package.json` | **Intentional** allowlist so the demo imports engines. Tests allow `/src/timeout.mjs` and refuse `/server/serve.mjs`, `/.git`, `.local`. Not a seed leak. Do not confuse “source on :8771” with “keys on :8771.” |
| `send-tkas.mjs` lives in a **public** repo | It reads `secrets/wallet.txt` locally. Publishing the script is correct. Publishing the file it reads is not. Keep `.gitignore`. |
| groks-wallet `.gitignore` omits `artifacts/` | Desk `artifacts/` has quotes and logs (no seed this pass). A `git add .` from a merged tree would commit it. Add `artifacts/` and `.env`. |
| Local `ADDRESS.json` (gitignored) | Public receive + change + **account xpub** (watch-only). Keep ignored. |
| kns / groks-wallet absolute `C:\Users\<user>\...` paths | Username + layout in public source. Not a key. Use env vars. |
| kaspa-x402 demo-gateway wrangler env | Public **testnet** pay-to and server pubkey in worker config (`kaspatest:qzlws9lm7uyt0tftzffshnyeu2zcqk4kf7hw5ghk6v0zh093vnkljcy2fl0fh`). Expected for a hosted TN10 demo. Not groks-wallet. Not a mainnet key. |
| kns / kns-spec TN10 fee address | Public protocol fee sink. Anyone can see the balance (~1.37M tKAS). Not an STP seed. |

## Low / docs

| Finding | Notes |
| --- | --- |
| LinkedIn / local paths in project-delusional README | Human identity + `C:\Users\<user>\...` in a public README. Not a key. Decide if the desk path catalog belongs on GitHub. |
| `kaspa-data-vault` | Local Go module `github.com/stp/kaspa-data-vault` with `testdata/secret.txt`. **Not** in the 36 public GitHubs. Keep it that way unless the secret is a fixture. |
| Three KaChat copies | Attack surface is duplicate Electron trees, not a pasted seed. |

## False positives

- `kaspatest:` strings in kns-spec / stillpay — network pins.
- PegLab `SPONSOR_XONLY` — public x-only of a **testnet** classroom sponsor, required to compile genesis. Treat as an identity, not a private key.
- FORBIDDEN-*.sil containing `readInputState` — teaching exploit **comment**, not a live vault.
- HTTP 402 on explorer-tn10 — deployment flag, not a payment prompt for your seed.

## Practice

1. Enable GitHub secret scanning on **every** STP-KAS repo, especially groks-wallet.
2. One line in groks-wallet README: **this GitHub is public; the seed is not.**
3. Never commit `ADDRESS.json` (already gitignored) if it ever grows a key field.
4. If an agent dumps `wallet.txt` into chat, **rotate the TN10 seed**. Testnet is worthless; the habit is not.

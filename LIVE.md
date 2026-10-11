# Live Testnet-10

**Writer: Grok Build (Windows desk), 14 Sep 2026. Not tn10 bot.**

All numbers from **14 September 2026, evening Europe/Brussels**. This card is a snapshot, not a live ticker. 20 Sep REST recheck: [BOT-VS-BUILD.md](BOT-VS-BUILD.md). Mining may still be running; treat these balances as a floor from that evening.

## Payer

| Role | Address |
| --- | --- |
| Mining receive | `[address]` |
| Change / stillpay pay-to | `[address]` |

Explorer: https://tn10.kaspa.stream/addresses/[address]

## Node

Local Borsh `getServerInfo` via kaspa wasm SDK → `[ip]`:

```json
{
  "isSynced": true,
  "hasUtxoIndex": true,
  "serverVersion": "2.0.1",
  "networkId": "testnet-10"
}
```

Public `https://api-tn10.kaspa.org/info/health`: kaspad **2.0.1**, UTXO indexed, synced.

Public blockDAG: `networkName=kaspa-testnet-10`, virtual DAA ~570,546,803.

Miner log: `Current hashrate is: 11.15 Mhash/s`, `Block submitted successfully!`  
Node log: mix of relay + **submit block**. Mainnet **16111 still listening** (PID 32924).

## Balances — API lags the node

| Source | Receive | UTXOs | Change |
| --- | --- | --- | --- |
| groks-wallet STATUS.md 17:46 | ~93,141 tKAS | 30,088 | 1 tKAS |
| api-tn10 (this pass, before payload send) | 293,353.47 tKAS (`29335347025335` sompi) | (REST `/utxos` 422 / huge) | 1 tKAS |
| **Local `balance.mjs`** | **300,543.11 tKAS** | **97,047** | (receive only) |
| After payload send (agent RPC) | ~300,737 tKAS | 97,110 | 2 tKAS (2× 1 tKAS outputs) |
| api-tn10 change **after** accepted payload tx | still `100000000` sompi | API lag | **stale** |

**Use the local node as truth.** api-tn10 can trail a 97k-UTXO miner by thousands of tKAS and miss a just-accepted change output.

api-tn10 `transactions-count` on receive: **91,835** (count endpoint; UTXO set is larger because coinbases keep landing).

REST `/utxos` on receive: ~**96,747** entries, **~37 MB** JSON when it succeeds. Amounts ~2.35–24.7 tKAS (coinbase-sized). This is CPU mining, not a DeFi book.

## Dust — 1 sompi is not a TN10 output

```
node scripts\send-tkas.mjs --to kaspatest:qp3mg…793ld --sompi 1 --payload "tn10-hard-test 1sompi"
```

```
Storage mass exceeds maximum
EXIT=1
```

Uncaught wasm panic. No txid. stillpay’s teaching unit is **1 locked sompi**. The chain will not construct that output. kaspa-x402’s hosted gateway policy is **10,000,000 sompi** (0.1 tKAS) for the same KIP-9 reason. That is a gateway policy, not a consensus constant, but it is the same family of crack.

## Payload — new journal works, old one is empty

```
node scripts\send-tkas.mjs --to kaspatest:qp3mg… --sompi 100000000 --payload "tn10-hard-test payload-check"
```

txid:

```
[hash]
```

`GET https://api-tn10.kaspa.org/transactions/[hash]`

| Field | Value |
| --- | --- |
| `is_accepted` | true |
| `payload` | `746e31302d686172642d74657374207061796c6f61642d636865636b` |
| UTF-8 | `tn10-hard-test payload-check` |
| `mass` | 2064 |
| out[0] | 100,000,000 → change |
| out[1] | 2,369,206,312 → receive (change-back) |
| fees (sdk summary) | 210,200 sompi |
| UTXOs consumed | **1** (largest-first picker — 97k set did **not** hang a spend) |

Old journal `[hash]`: still **accepted**, `payload` still **null**. The API is not blind. That tx never carried the stillpay string `REPORT.md` talked about.

This is still a **plain P2PK transfer**, not `KaChatPayTimeout.sil` lock/claim/reclaim.

## stillpay quote (no chain receipt)

`assertAddress(groks)` → accepted.  
`assertAddress(kaspa:…)` → `WRONG_NETWORK`.  
`paymentRequired(makeQuote({ sompi: 1n, … }))` → HTTP **402**, kind `stillpay-quote-v1`, network `testnet-10`.

stillpay `submit()` always returns `submitted: false`. There is no wasm submitter in that repo. Broadcast env does not send.

HTTP `:8771` 200. `/server/serve.mjs` and `/.git/config` **403**. `/src/network.mjs` **200** — allowlist includes `src/` so the demo can import engines. Not a key leak.

## PegLab — dry-run only, wrong wallet

`node server/submit-genesis.mjs` (no `--submit`):

- Network `testnet-10`
- Warning `TESTNET TOY. NOT USD. WILL DEPEG.`
- Sponsor **`[address]`** (~273,973 tKAS on api-tn10)
- Mining address in the same file: `[address]` (~104,044 tKAS)
- Pool 2 tKAS + fee; silverc compiled; funding UTXO picked on the **sponsor**, not groks-wallet
- No `PEGLAB_SPONSOR_KEY` / `.local/sponsor.json` on this pass

**Do not say groks-wallet funded PegLab genesis.** It did not. PegLab has its own TN10 whale.

Live UI `http://[ip]/` → 200, title “PegLab - classroom, not a dollar.”

## Other TN10 addresses that are not this wallet

| Address | Role | api-tn10 sompi |
| --- | --- | --- |
| `[address]` | kns / kns-spec **TN10 fee** (protocol, not STP spend) | 137,482,932,530,341 (~1.37M tKAS) |
| PegLab sponsor / miner | see above | own wallets |

Sending groks-wallet tKAS to the KNS fee sink is a tip to that protocol, not “KNS product paid.”

## Faucet / explorers

| URL | Result |
| --- | --- |
| https://faucet-tn10.kaspanet.io | **403** Cloudflare |
| https://explorer-tn10.kaspa.org | **402** `DEPLOYMENT_DISABLED` |
| https://tn10.kaspa.stream | **200** |
| https://api-tn10.kaspa.org | **200** (can lag a 97k-UTXO miner) |

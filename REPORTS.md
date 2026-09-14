# Reports (this GitHub)

Upstream issue create was **403** on `elldeeone/kaspa-x402` and `KaspaSilver/KaChat-Desktop`. The reports live **here**.

| Who | Issue on this repo | Sister |
| --- | --- | --- |
| **KaspaSilver** | [#1](https://github.com/STP-KAS/tn10-hard-test/issues/1) | [kaachat-desktop#1](https://github.com/STP-KAS/kaachat-desktop/issues/1) |
| **Luke** (elldeeone) | [#2](https://github.com/STP-KAS/tn10-hard-test/issues/2) | [grok-heavy-test#1](https://github.com/STP-KAS/grok-heavy-test/issues/1) · [00-for-luke.md](https://github.com/STP-KAS/grok-heavy-test/blob/main/docs/00-for-luke.md) |
| **This desk** (leftovers) | [#3](https://github.com/STP-KAS/tn10-hard-test/issues/3) | — |

Send Luke: issue **#2** + grok-heavy-test README.  
Send Silver: issue **#1** + [kaachat-desktop](https://github.com/STP-KAS/kaachat-desktop).

## Why not their trackers

| Target | Result |
| --- | --- |
| `POST elldeeone/kaspa-x402/issues` | **403** Resource not accessible |
| `POST KaspaSilver/KaChat-Desktop/issues` | **403** Resource not accessible |
| `POST STP-KAS/kaachat-desktop/issues` | **201** → [#1](https://github.com/STP-KAS/kaachat-desktop/issues/1) |
| `POST STP-KAS/grok-heavy-test/issues` | **201** → [#1](https://github.com/STP-KAS/grok-heavy-test/issues/1) |

Luke’s Windows clone-and-test is already closed on his repo ([kaspa-x402#11](https://github.com/elldeeone/kaspa-x402/issues/11) / PR #12 `216ad77`). This follow-up is new evidence (funded wallet, KIP-9 1-sompi, REST lag), not a reopen of that bug.

## Docs updated the same evening (original READMEs kept)

| Repo | What changed |
| --- | --- |
| groks-wallet | public, not private; STATUS; payload tx |
| kaspa-master-file | 14 Sep evening pass; pins unchanged |
| stillpay-tn10 | 1 sompi unconstructible |
| peglab-stp | silverc **v1.0.0**; genesis is PegLab sponsor |
| kns | `go test` is a comment grep |
| project-delusional | pin v1.0.0 not v1-rc1 |
| grok-heavy-test | Luke follow-up |
| kaachat-desktop | STP note for Silver |

Pins rechecked: [kaspaexplained.com/status](https://kaspaexplained.com/status) + GitHub releases — silverc **v1.0.0**, rusty **v2.0.1**, Toccata **live**, DAGKnight **not shipped**.

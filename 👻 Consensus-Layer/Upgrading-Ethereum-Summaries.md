# Upgrading Ethereum Summaries

This file will contain my personal notes from studying the [Upgrading Ethereum book](https://eth2book.info/) by Ben Edgington. They are my personal notes to help my own comprehension.

## 2.3 Consensus

### 2.3.1 Preliminaries
Proof of Stake is composed of two parts: LMD GHOST and Casper FFG. Those two are collectively called Gasper.

Sybil Resistance: protection from an attacker creating multiple low-cost identities.

Content of a block:
Pre-merge execution layer: transaction data.
Pre-merge beacon chain: block attestations
Post-merge: a block contains both attestations and TX data.
EIP-4844: proto-danksharding. Blocks now include temporary blob data.

Ethereum Proof of Stake allows forking unlike other consensus algorithms such as PBFT and Tendermint. For the latter, this increases safety (no contradicting states) but decreases liveliness (the network might stop).

In Eth this decrease in safety takes the form of forks and the liveliness the form of fork rules.

POW (btc and pre-merge execution layer Ethereum): fork choice rule consists of chain with most computer work done

POS Casper FFG: follows chain with the highest justified checkpoint.

POS LMD GHOST(Greediest Observed Sub-Tree): The chain with the most attestations wins.

Reorg/reservsion: A chain can incur a reorg if the fork choice rule causes the current chain to be replaced by another branch.

Safety: Nothing bad ever happens. There is always a single canonical chain.

Liveness: Chain will never go in a deadlock and will continue to add blocks.

Ethereum prioritises liveness over safety.

Finality: A safety property by which at a particular checkpoint the chain cannot be reverted. This property is provided by Casper FFG.
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

### 2.3.2 Overview

Node: a node validates consensus
Validator: attached to a node. A node can have multiple validators.

Slot:  12 seconds interval holding a proposed block
Epoch: 32 slots.

Every slot a validator is selected to propose a block (beacon state data + execution layer data).
Every epoch every validator makes 1 attestation. Meaning, each slot 1/32 of validators make an attestation.

Slashing: Occurs when equivocation happens and results in a loss of ether for the validator.

Equivocation: Making contradictory statements such as voting for two different blocks in the same slot.

POS on Eth: Is composed of two consensus protocols working together: LMD GHOST and Casper FFG. The combination of both of them is Gasper.

### 2.3.3 LMD GHOST

LMD GHOST: Latest Message Driven Greedy Heaviest Observed Sub-Tree. Provides liveliness because new blocks can always be proposed.

Casper FFG: Provides safety because it designates checkpoints for which the chain cannot be reorged. (prevents long reversions)

Finality: Economic finality. It would require at least 1/3 of the staked ether to be burned.

*LMD GHOST*
GHOST rewards the heaviest subtree. A vote for a children block is the same as voting for all its ancestors implicitly.

LMD: Latest Message Drive. A message in this context is an attestion. Latest means that only the latest attestation counts and all previous ones are discarded.

LMD GHOST is a fork choice rule.

Weight of a block is the weight of all the branches above it. To get the canonical chain, we follow the heaviest branch (most attestations).

In POW, blocks are considered safe based on block confirmations. In POS, the concept of a safe block depends of the amount of validators who have voted for a particular subtree. Formula would be 1/2 + B < W. B are the bad actors. We consider a block safe even we still have a majority even when accounting for all the bad actors.

incentives: Rewards given for attestations for block which are part of the canonical chain. Rewards also for proposing blocks that get accepted in the canonical chain. Validators are not punished for voting for the wrong head block as there might be block propagation issues preventing them from voting correctly.

Slashing: solution to the nothing-at-stake problem in which a bad actor votes for all subtrees in order to get rewards.
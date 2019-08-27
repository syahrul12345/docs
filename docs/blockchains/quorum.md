# Quorum

Quorum is a fork of Go Ethereum.

Quorum is a permissioned consortium blockchain protocol.

## Consensus

Quorum supports the following two consensus algorithms:

* Raft — a [CFT](/glossary/cft) consensus algorithm.
* Istanbul Byzantine Fault Tolerance — a [BFT](/glossary/bft) consensus algorithm.

### Raft

The Raft consensus algorithm has the following key characteristics:

* Crash fault tolerance
* Transaction finality
* On-demand block creation
* Consensus nodes flexibility

#### Crash fault tolerance

Crash fault tolerance assumes that there no adversary nodes on the network.

A Raft Quorum network always has the nodes in one of the following roles:

* Minter — in Raft terminology, this is the *leader* node. In Raft Quorum terminology, this is the *minter* node.
* Verifier — in Raft terminology, this is the *follower* node. In Raft Quorum terminology, this is the *verifier* node.

The minter node creates the blocks and the verifier nodes follow the minter node.

By default, the very first node you deploy with Chainstack as part of your Raft Quorum network assumes the minter role.

Each subsequent node that you deploy as part of the same network assumes the verifier role.

If the minter node goes offline or if you force a removal of the minter node from the network, a new minter node is automatically elected from the pool of the verifier nodes.

#### Transaction finality

A Raft Quorum network reaches transaction finality on a per-block basis.

The minter node includes transactions in a block, creates the block, and sends a new log entry on the block to the verifier nodes.

The verifier nodes receive the log entry of the transaction and the new block from the minter node. The verifier nodes then message back the minter node and acknowledge the new log entry receipt.

The minter node then adds the block to the chain.

#### On-demand block creation

Since Raft Quorum is designed to run a crash tolerant system only, the blocks are only created when there is a transaction on the network. No empty blocks are created.

When there is a new transaction propagated through the network, a new block creation is triggered and the minter node creates a new block.

### IBFT

Stands for Istanbul Byzantine Fault Tolerance.

Byzantine fault tolerance assumes that there can be adversary nodes on the network. The network can still operate and reach consensus in the presence of the adversary nodes.

IBFT can tolerate up to a third of all the nodes in the network being faulty, or **3f+1**, where **f** is the number of faulty nodes.

Example with **f** is 3:

* Total nodes in the network: 10
* Maximum number of faulty nodes can be tolerated: 3
* The network reaches consensus the number of non-faulty nodes: 7

#### Transaction finality

An IBFT Quorum network reaches transaction finality on a per-block basis. Every block formed in network is validated and sealed by nodes before being added to the chain. This per-block validation and sealing provide absolute transaction finality and remove any chance of forking or any other possibility to undo a transaction.

All nodes in a Quorum network deployed with Chainstack have the following two roles at the same time:

* Validator — the node is a part of the group of nodes that validate the block to seal it and include in the chain.
* Proposer — the node proposes a block to the group of the validator nodes.

The process of sealing and including a block in the chain is the following:

* Block proposal — a proposer submits a block for validation to the group of validator nodes. The proposer also adds the *ProposerSeal* to the proposed block.
* Block preparing — the validator nodes reach the **3f+1** consensus on the proposed block.
* Block ready — the validating nodes add their *CommittingSeals* to the block and add the block to the chain.

The transactions in the block are now final. A new round starts.

Since IBFT is designed to run even in the presence of malicious actors, the blocks are always created at regular intervals, regardless of whether there are transactions on the network. When there are no transactions, empty blocks are produced and added to the chain.

::: tip See also

* [Quorum for Developers](https://www.goquorum.com/developers)

:::

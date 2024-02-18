---
Exam:
  - Blockchain and Distributed Ledger Technologies
  - Distributed Systems
---
Bitcoin is based on Proof-of-Work, which is a protocol that let users of the network to decide which is the block that will be part of the ledger.
> [!Note]
Proof of Work is NOT consensus, it’s just an instrument to make more difficult for malicious users to publish blocks.

The nodes that perform the PoW are called miners.

The idea is that each miner has to solve a cryptographic puzzle to publish a new block. The first miner that solves the puzzle sends the block to the other nodes, which then propagate it.

The puzzle consists in finding a _nonce,_ which is a 31 bit number, that if injected into the header, the header hash will be less than a certain number, which means that the $k$ least significative bits should be equal to $0$.

Changing the $k$ means tuning the difficulty of the problem. More $k$ requires more time. The $k$ is tuned every around $2016$ blocks in order to keep the publishing of a new block every 10 minutes (in the case of Bitcoin). This number is a tradeoff between security and speed, since the puzzle cannot be too easy nor too hard.

The problem can be solved only with brute force, but the hash can be validated instantly. This helps the network to get rid of malicious nodes.

When a miner publishes a new block, it receives a mining reward and the sum of the transactions fees.

The mining reward is halved each 210,000 blocks. (Actually its value in bits is right-shifted by 1 position, which means eventually the reward will be zero).

Multiple users can enter mining pools in order to distribute the workload. Each node will search only trough a range of nonces, and they will divide the reward.

There could be multiple nonces that are a solution to the problem.

The past work put into a puzzle does not influence the likelihood of solving future puzzles.

### Bitcoin Flow
1. A new transaction is broadcasted to all the nodes;
2. Each node collects the new transactions into a block;
3. Each node tries to solve the PoW puzzle;
4. The node that solves the puzzle, broadcasts the block to all the nodes;
5. Nodes accept the block only if all the transaction inside of it are valid;
6. Nodes put the valid block they received inside of their own copy of the blockchain.

### Branching
If a miner solves the puzzle, it doesn’t mean it will receive a reward, but its block has to be in the main branch to be considered as valid. This because when the network that is synched to the secondary branch realizes the primary branch is another one, all the blocks are discarded and it’s like they never existed.

Choosing the longer branch as the primary branch is not always a good idea, since this can be exploited by malicious users.

A good idea is to choose the chain that has the highest cumulative work, meaning the highest number of expected hashing attempts needed to find a valid nonce for that block. This value is computed as following:

$$ \frac{2 ^{256}}{\text{target} + 1} $$


# Distributed System Course Definition
>[!TODO]
>This has to be merged with the above
### Proof of Work

There is a property that tells us that a valid block have an hash $H$ with the $k$ least significant bits set to zero.

Every new proposed block has to be valid.

Every block has also a Nonce, that’s a value that has some arbitrary value that makes the hash satisfy the property. The only way to find this value is by brute-forcing all the values, so it’s a computational hard operation. 

A node that tries to compute this value in order to try to add a new block into the blockchain is called a miner (the process is called mining).

The number $k$ of lest significant bits that have to be set to zero is changed every few weeks in order that a new value is found every 10 minutes by one of the nodes in the system.

When a node find a valid block, it can propose it to all other nodes in the network, and since the only way to discover a nonce that make the block valid is through work, this is called Proof of Work.

Let’s assume that $k=32$, in I have to do $2^{32}$ tries. The typical server has to do $2^{32} \sim \text{4 billion}$ hashes in order to make the block valid, and send it to other servers.

All the transactions that are made in between the computations are inserted into a pool, and inserted in the block whenever is possible.

Only the most powerful and luckiest computers in the network can extend the blockchain with a new block. Every time a node insert a new block, it gets a reward of about 6.25 BTC.

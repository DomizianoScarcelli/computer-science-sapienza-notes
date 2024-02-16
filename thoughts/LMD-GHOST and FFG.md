[Ethereum's Proof of Stake consensus explained](https://www.youtube.com/watch?v=5gfNUVmX3Es)

LMD-GHOST is the consensus protocol used in [[Ethereum]] 2.0 to decide which is the primary chain, which is necessary when validators have different views on the head of the chain. The majority of the time this doesn’t happen, but it could happen in the case of network latency of if a block proposer proposes two blocks.

The problem here is that we cannot pick the longest chain.
![[Screenshot 2023-11-16 at 7.03.22 PM.png]]
Without LMD-GHOST, the right most fork would be chosen. With LMD-GHOST, actually the fork with the highest weight is the leftmost, and so it will be chosen.
### Rounds and Epochs

There is a round each 12 seconds, and each 32 rounds there is an epoch.

At the beginning of each epochs, the validators are split into 32 committees. (Each committee is also split into 128 subnets.)

Each committee is responsible for one time slot inside of the epoch.

When a committee has to vote, a random validator inside of each committee is chosen to vote for the next block. The other nodes in the committee have to attest the block, which is a kind of special vote. The validator has 4 seconds to vote, and if it doesn’t, the other nodes will just attest for the previous block.

Validator can only propose one blocks, and the other can only attest one, otherwise they will be slashed.

### Casper FFG

Casper is a BFT (Byzantine Fault Torelance) method used in Ethereum for block finality.

TODO: CONTINUE
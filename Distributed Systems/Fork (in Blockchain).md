---
Exam:
  - Distributed Systems
  - Blockchain and Distributed Ledger Technologies
---
It can happen that two servers around the world find the new block in the same time, broadcast it to everybody and half of the server think block 1 is the new one, and the others think block 2 is the new block. This is called a fork of the blockchain.

Half of the servers try to extend block 1 and the other half try to extend block 2.

It can happen that the two forks go on in parallel, but probabilisticly at one point one branch of the blockchain will be longer, the new block will be broadcasted to everybody, and they’ll see that that branch is longer, and they stop to work on the previous branch, so the blockchain is not forked anymore. The branch becomes a dead branch.

All the servers work on the longest branch, so forks probabilisticly don’t last long. Transaction in dead branches aren’t valid anymore. They’re put again in the pool and they will appear in the current branch.

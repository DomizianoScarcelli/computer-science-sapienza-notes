Proof of Stake is an alternative and way more power efficient method for deciding which block will be added to the blockchain.

Proof of Stake is base on the Staking mechanism, meaning that a node can become a validator by Staking 32 ETH (sending the ETH to a dedicated smart contract). Those ETHs are then freezed.

Each time a validator can bet on the blockchain branch that will become the primary branch in the next round, and if so they will receive a reward. Note that if the validator doesn’t win, the bet is not lost.
### Slashing

Since a validator could bet on every branch and get a sure reward, Ethereum introduces slashing, which means its stake gets reduced if the validator has a bad conduct based on some known rules.

Those rules are:

- **Equivocation**: trying to publish multiple blocks in the same round
- **Double Vote**: Attesting to two different blocks in the same round;
- **Surround Voting**: voting for a source and a target block that occur in epochs surrounding an already voted pair.
- **Proposer Misconduct:** validator that are selected to propose a block in a specific round should include all valid attestations in that block. Slashing will occur if they don't.

These are some basic rules, there are more and they can vary over time.

The condition of slashing can only be verified if another node reports the misbehaving node. Because of this, a special reward is given to those kind of nodes, which are called whistleblowers, and to the proposers who include the whistleblowing message in the block.
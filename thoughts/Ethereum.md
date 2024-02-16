The Ethereum protocol differs from [[Bitcoin]] primarily because of the speed of the block publications (one each 12 seconds instead of 10 minutes) and because of Smart Contracts, which make the blockchain programmable.

Unlike Bitcoin, Ethereum uses a balance model, meaning that it doesn’t make use of UTXOs, instead each account have a certain balance expressed in Wei ($10 ^{-18}$ ETH).

Since each account has a balance attached, the nodes in the network should keep track of the current balance of every account to verify whether they can spend the declared amount in a transaction or not

### EOAs vs CAs

In Ethereum there are two types of accounts:

- EOA - Externally Owned Accounts: these are the accounts which are owned by a physical entity. They are controlled by the account private key, contain a balance in ETH and are capable of sending transactions.
- CA - Contract Accounts: there are accounts which are created by smart contracts, which also have a balance in ETH but cannot issue transactions. They can communicate with other CA by sending messages, and can be triggered by EOA by receiving transactions. Messages don’t have to be stored on the blockchain, in order to preserve gas, but since the smart contract computation is deterministic, we just need to know the input values to compute the message on the fly.

### Ethereum Address Generation

Ethereum uses Keccak-256 as [[Hashing on the Blockchain|hash function]].

As in Bitcoin, the [[Bitcoin Address Generation|address is generated]] starting from the public key, according to the following procedure:

1. Get the private key associated to the public key
2. Hash the private key with Keccak256
3. Hash the address again
4. Compare character-wise the address with its hash
5. If the character is a letter (hex greater than 9) and the corresponding hash character is greater or equal than 8, uppercase it.

The last step acts like checksum.
### Nonce

The nonce in Ethereum has multiple meanings. If we don’t consider it in the context of PoW, the nonce is just a number that models how many transaction an account has made.

When a new transaction is issued, it has to have a nonce greater than the current nonce. If the nonce is the successive number, the transaction is accepted, otherwise is held until the nonce is the next number w.r.t. the current count.

This is done in order to prevent any other account to replicate someone else’s transaction, since everyone can copy a transaction. For the transaction to be valid, the other account that wants to copy the transaction needs to update the nonce and then sign the transaction again, which they cannot do if they do not own the private key of the original transaction.

### Ommers

When dealing with Proof of Work in Ethereum, differently from Bitcoin, the protocol gives a small rewards also to those miner who solved the puzzle, but which block didn’t make to the primary branch of the blockchain. Those miners are called Ommers (also known as Uncles).

Ommers are discovered during the process of block validation. When a miner broadcasts a block, other nodes on the network check its validity. If a valid block is not included in the main chain, it may be referenced as an ommer by subsequent blocks.

### Fork

When the protocol has to be updated, a fork happens. It’s called a fork because the network splits in two parts, the one made by nodes that still want to use the old version, and the one made by nodes that use the new version.

There are two types of forks:

- **Soft fork**: the updates are backward-compatible and so the network doesn’t have to split into two subnets, but some of the nodes can adopt the new rules.
- **Hard fork**: the update is not backward-compatible and a split into subnets is necessary.
### Chain data vs State Data

Blockchain data can be separated in:

- **Chain data**: the list of blocks that make the blockchain
- **State data**: the result of each transaction’s state transition. State data is not permanent, since old and consolidated data can be deleted. State data can be computed using information from the genesis block to the latest block (or from the least available state piece of data and the latest block).

Full Nodes (aka Archival nodes) keep the chain data, while light nodes only keep the state data.
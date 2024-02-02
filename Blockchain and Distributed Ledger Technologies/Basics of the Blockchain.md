The blockchain is a platform which is based on a distributed ledger, a strictly totally ordered sequence of blocks which stores transactions. Each block is composed of an header and a list of transactions. Inside of the header there is the hash of the previous block’s header, which depends also on the transactions inside. Because of this, transactions (and any other data) inside of a block are immutable.

The hash inside of the block header can be seen as a fingerprint of the whole blockchain up to that node.

The blockchain platform is different from the blockchain protocol. Examples of the latter are Bitcoin and Ethereum.

Each transaction in the ledger has a unique id.

A copy of the blockchain is inside of each single full node of the network, while light nodes don’t store the full blockchain, but can query full nodes to access data they don’t have.

In order to verify that the transaction is made by an authorized entity, the blockchain uses cryptographic signature.

Not each block have the same number of transactions, even an empty block is a valid block.

The order of transactions is determined by how they are placed inside of the block, since the block is ordered. There is no guarantee that this is the real order of transactions, but what the network believe is true becomes the reality. We cannot use a timestamp for the transaction since this wouldn’t be trustworthy.

Everything is a transaction. From the deployment of the smart contract to its invocation.

## CAP Theorem
The CAP theorem says that in a distributed system we can only have two out of the three following properties:

- **Availability**: the user always gets a response, even if it’s not the latest version of the data.
- **Consistency**: if the user gets the data, then it’s the latest version.
- **Partition Tolerance**: the network never splits in two independent subnetworks even after a lot of messages are dropped or delayed.

Blockchains drops the consistency property, but it’s eventually consistent, meaning that there always will be one point in time where the data will be updated. The eventually in Bitcoin is 6 blocks, while in Ethereum is 12 blocks.

The blockchain is partition tolerant, since the whole network can be destroyed, but if there is still a node, this single node can restore the whole network, replicating the information to the other nodes in the network and the blockchain will still be operative.

Availability is also there, since if a node wants to know anything about a transaction it already have all the information it needs.
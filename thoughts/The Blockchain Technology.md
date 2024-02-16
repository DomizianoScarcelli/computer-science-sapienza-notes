The blockchain is a platform which is based on a distributed ledger, a strictly totally ordered sequence of blocks which stores transactions. Each block is composed of an header and a list of transactions. Inside of the header there is the hash of the previous block’s header, which depends also on the transactions inside. Because of this, transactions (and any other data) inside of a block are immutable.

The [[Hashing on the Blockchain|hash]] inside of the block header can be seen as a fingerprint of the whole blockchain up to that node.

The blockchain platform is different from the blockchain protocol. Examples of the latter are Bitcoin and Ethereum.

Each transaction in the ledger has a unique id.

A copy of the blockchain is inside of each single [[Light Nodes vs Full Nodes|full node]] of the network, while [[Light Nodes vs Full Nodes|light node]] don’t store the full blockchain, but can query full nodes to access data they don’t have.

In order to verify that the transaction is made by an authorized entity, the blockchain uses cryptographic signature.

Not each block have the same number of transactions, even an empty block is a valid block.

The order of transactions is determined by how they are placed inside of the block, since the block is ordered. There is no guarantee that this is the real order of transactions, but what the network believe is true becomes the reality. We cannot use a timestamp for the transaction since this wouldn’t be trustworthy.

Everything is a transaction. From the deployment of the smart contract to its invocation.

Because of the [[CAP Theorem]], blockchain technology provides Availability and Partition Tolerance, but it's not consistent. 


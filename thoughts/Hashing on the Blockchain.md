Bitcoin uses SHA2-256 as a hashing function, while Ethereum uses Keccak-256. The more bits in the digest, the stronger the hashing function, and the less the probability of a collision.
### Merkle Trees
Just like indexes in databases, which allows you to find an item in a constant time instead of having to linearly search it, a Merkle Tree allows you to find a transaction in a constant time. This is useful for light nodes ([[Light Nodes vs Full Nodes]]) which don't want to search over all the transactions.

Merkle trees allows to index, confirm and fingerprint the full block body in the exact order we had.

The leafs are the hashes of the ordered transactions. The father of two nodes is the hash of the concatenation of the two child hashes, up until we have just the root hash.
![[Screenshot 2024-01-21 at 11.54.28 AM.png]]

The Merkle root is the hash that goes in the header of the block.

Let’s now say that a light node wants to verify that $t_2$ is indeed in the block. The light node doesn't need to ask a full archival node the hashes of all the single transaction, but it can compute $h_2$ from $t_2$, and then it can ask for $h_1, h_{34}$ and $h_{5678}$ in order to compute $h_{12}$ and then compute the Merkle root to verify if it’s the same as before.

![[Screenshot 2024-01-21 at 11.58.01 AM.png]]
This is called the Merkle Proof.

This works well if we have a transaction that is $2^ n$, but what if we have something like $5$ transactions?

![[Screenshot 2024-01-21 at 11.59.53 AM.png]]
I force use a single transaction to produce more hashes in order to be able to build the tree.

In Ethereum they use Patricia Merkle Radix Trees to produce the header. What differs from the simple Merkle Tree is the fact that this other approach allows also to search for transaction data in an efficient way. Patricia trees aren’t balanced.

Patricia and Merkle trees are used for Verification.

## Properties of Hashing functions

In order for a function $h$ to be a valid hashing function, it must have some properties:

- _Preimage resistance_: given an hash $k$, it should be difficult to find any message $m$ such that $k = h(m)$;
- _Second-preimage resistance_ (or weak collision resistance): given an input $m_1$, it should be difficult to find another input $m_2 \neq m_1$ such that $h(m_1) = h(m_2)$
- (Strong) _Collision resistance_: It should be difficult to find a tuple of messages $m_1$ and $m_2$ such that $m_2 \neq m_1$ and $h(m_1) = h(m_2)$. The pair $(m_1, m_2)$ is called a cryptographic hash collision.

## SHA-1 Operations and Functions

SHA-1 is a didactic example which algorithm is based on bitwise operations in order to mix the bits of the original message.

The used operations are:

- Bitwise AND
- Bitwsie OR
- Bitwise XOR
- Bitwise Complement
- Addition modulo $2^w$
- Left and right shift operation
- Rotate left operation

ASICs optimize those operations, that’ why they are very fast at mining.

The SHA-1 functions are:
![[Screenshot 2024-01-21 at 12.26.47 PM.png]]

The SHA-1 constants are four and they are 230 times the square roots of 2, 3, 5 and 10. These constants are used in order to avoid the reverse engineering of the algorithm (nothing up my sleeve).

We use padding in order for the length of the message to be a multiple of 512 bits.

The message are parsed into $N$ blocks each one of 512 bits. Each block is parsed into 16 32-bits words.

The full algorithm is summarized in the following image.

![[Screenshot 2024-01-21 at 12.39.09 PM.png]]
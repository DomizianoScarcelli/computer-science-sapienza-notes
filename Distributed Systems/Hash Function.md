---
Exam:
  - Distributed Systems
  - Blockchain and Distributed Ledger Technologies
---
An hash function is a function with these properties:

- _Preimage resistance_: given an hash $k$, it should be difficult to find any message $m$ such that $k = h(m)$;
- _Second-preimage resistance_ (or weak collision resistance): given an input $m_1$, it should be difficult to find another input $m_2 \neq m_1$ such that $h(m_1) = h(m_2)$
- (Strong) _Collision resistance_: It should be difficult to find a tuple of messages $m_1$ and $m_2$ such that $m_2 \neq m_1$ and $h(m_1) = h(m_2)$. The pair $(m_1, m_2)$ is called a cryptographic hash collision.

The hash function can take a large input and map it to a relatively small hash, so it can be used to map large domains to small domains.

It’s not possible to know if a function with those property exist, there are some functions that seem to have those but we cannot be sure. (For example RSA now seems a secure algorithm, but also MD5 seemed safe and now it’s completely broken).

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
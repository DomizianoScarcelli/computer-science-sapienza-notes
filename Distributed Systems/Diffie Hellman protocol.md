---
Exam:
  - Distributed Systems
---
Alice and Bob want to share a secret key in the Internet. They agree on a very big prime number $g$.

Alice chooses a random value $a$, and sends to Bob the value $g^a$.

Bob chooses a random value $b$ and sends to Alice the value $g^b$.

Alice can now compute $(g^b)^a$. It’s computationally very hard to recover $b$ from $g^b$. 

Bob can compute $(g^a)^b$ .

The two computed keys $K$ are the same. Alice don't know $b$ but it’s able to compute $K$, and Bob don’t know $a$ but it’s able to compute $K$.

Men in the middle are able to see $K$ and $g$ but it’s very hard to get $a,b$ from those values.

### Authenticated Diffie Hellman

Bob has a public key $k_b$. We can send $E_{k_b}(g^a)$, the message encrypted with Bob’s public key. Bob sends the message $(g^b, H(K|\text{handshake}))$ where $H$ is the hash togheter with some message and $K = ((g^b)^a)$.

Then alice can compute $K = (g^b)^a$, append a message such as “handshake”, hash it and compare it with the sent hash. Alice and Bob agreed on a secret key and Bob has proved its identity to Alice because of the public key (Only Bob is albe to decript the message sent from Alice, since it’s encrypted with its public key). If the hash is different from the one computed by Alice, it means that the message doesn’t come from Bob.
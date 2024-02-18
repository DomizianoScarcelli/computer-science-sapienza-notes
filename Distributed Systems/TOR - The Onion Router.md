---
Exam:
  - Distributed Systems
---
Inside TOR there is a list of around 7.000 TOR servers, spread everywhere in the world.

The idea is to select three of them (actually 5 in the real case scenario) and make a circuit in which you pass all three servers before getting to the final server.

> [!TODO]
***INSERT PICTURE 1***

Every server has it’s couple of public and private key. The packets that goes through the server are encrypted in an “onion” way, meaning that if the flow of the packet is through servers $A,B,C$ the packet $p$ is encrypted with the public key of the servers in the inverse order.

$$
E_{k_C}(E_{k_B}(E_{k_A}(p)))
$$

Every time the node passes through a server, the server can decrypt it with it’s private key and can see who is the next hop.

The first server $A$ is called “guard”, because it knows who is using TOR, but doesn’t know the final destination.

The second server $B$ doesn’t know anything about the packet.

The last server $C$ is called the “exit node”, and knows that someone is reaching a particular destination, but doesn’t know who.

Since the encryption with asymmetric keys is computational more expensive than the symmetric one, this type of encryption is only used to decide a session key between the origin and the servers, then this key, that is symmetrical, is used to encrypt the packets.

The decision about the session key happens with the [[Diffie Hellman protocol#Authenticated Diffie Hellman|Authenticated Diffie Hellman Protocol]]. 

We use authenticated Diffie Hellman with the guard server $A$ to agree on a session key and encrypt messages faster. Than I can talk to $B$ through $A$ and to $C$ through $B$ in order to agree on two more session keys.

Latency is not very good. Bandwidth can be the same as the direct connections.The problem is that some nodes are not very fast, so it depends on the service of every node in the circuit.

### TOR Vulnerabilities

The anonymity is lost if the guard and the exit node is owned by the same person. This person can notice that everytime a message is sent to $A$, it arrives to $C$ very fast, so the connection can be de-anonymized.

In order to overcome this vulnerability, it’s important for TOR to choose the guard and the exit node in order that they’re not owned by the same person. This can be achieved by choosing two nodes in very different geographical zones.
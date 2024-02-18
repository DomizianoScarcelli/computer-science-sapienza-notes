---
Exam:
  - Blockchain and Distributed Ledger Technologies
---
The CAP theorem says that in a distributed system we can only have two out of the three following properties:

- **Availability**: the user always gets a response, even if it’s not the latest version of the data.
- **Consistency**: if the user gets the data, then it’s the latest version.
- **Partition Tolerance**: the network never splits in two independent subnetworks even after a lot of messages are dropped or delayed.

Blockchains drops the consistency property, but it’s eventually consistent, meaning that there always will be one point in time where the data will be updated. The eventually in Bitcoin is 6 blocks, while in Ethereum is 12 blocks.

The blockchain is partition tolerant, since the whole network can be destroyed, but if there is still a node, this single node can restore the whole network, replicating the information to the other nodes in the network and the blockchain will still be operative.

Availability is also there, since if a node wants to know anything about a transaction it already have all the information it needs.

### Availability and Consistency trade-off

There is always a trade-off between availability and consistency.

- Availability: the service is always available;
- Consistency: the content is always the most updated.

The choice between the two heavily depends on the application. For banking applications, consistency is more important. For media applications like news, availability is more important, since a news that's not the most updated is not a problem.
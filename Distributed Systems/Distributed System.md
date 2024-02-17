---
Exam:
  - Distributed Systems
  - Blockchain and Distributed Ledger Technologies
---
A distributed system is a system where there is no central entity like a server and clients that make requests to that server, but all the devices in the system run together and make a network.

In order for the system to work, some assumptions need to be taken:
- Processes speed is not predictable, meaning that a client could be slow or fast, but the system should always work;
- There is no global clock: In a distributed system there are as many clocks as there are systems. The clocks are coordinated to keep them somewhat consistent but no one clock has the exact time. Even if the clocks were somewhat in sync, the individual clocks on each component may run at a different rate or granularity leading to them being out of sync only after one local clock cycle. [^1]
- Channels (and so messages) can be:
- Reliable / Unreliable: If I send the message in a reliable system, the message arrives. In this type of system no messages are lost but in an unreliable can.
- Synchronous / Asynchronous: If I sent a message in a **synchronous** system, there will be some known time (bound / limit of time when I’m sure a message will arrive) before it will arrive, in order to synchronize. 
**Asynchronous** means that there will be some unknown time before the message arrives, but the system should work even without that message.

Usually, we assume that messages are Reliable and channel Asynchronous.

Processes can be correct or they can fail. There are two types of failures:

- crash failures: the process can stop working because of the failures
- **byzantine** failures: the process can do the wrong thing because of the failure. It doesn’t stop working, but it corrupts the system and causes bugs and security issues.
---
[^1]: [No Global Clock](http://infolab.stanford.edu/~burback/dadl/node91.html)
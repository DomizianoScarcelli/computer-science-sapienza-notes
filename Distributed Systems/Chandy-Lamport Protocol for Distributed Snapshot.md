---
Exam:
  - Distributed Systems
---
The simple way for $P_0$ to take a snapshot of the global state doesn’t assure us that global state is consistent.

Another way to approach the problem is the Chandy-Lamport protocol.

It assumes the channels are FIFO, meaning if in channel $1$ two events $e_1^1$ and $e_1^2$ exists such that $e_1^1 \rightarrow e_1^2$,  $e_1^1$ sends a message to channel 2 that receives it in event $e_2^1$ and a message from $e_1^2$ that is being received in $e_2^2$, then we are sure that $e_2^1 \rightarrow e_2^2$.

The protocol stats with $P_0$ sending a “take-snapshot” message to one (or more) process. When a process receives a $ts$ message:

- If it’s the first $ts$ message it has received, it sends a $ts$ message to all the other processes.
- If it has already received a $ts$ message, it saves its local state.

The protocol takes the snapshot of the system once every process has received its $ts$ message.

The protocol ends when every process has received its last $ts$ message.

Both the cuts taken from the protocol are consistent.

### Consistency proof

Let’s rememeber that a cut $C$ is consistent if $\forall e, e' : e \rightarrow e' \land e' \in C \Rightarrow e \in C$.

![C is the cut taken by the protocol, C’ is the cut when the protocol has finished](distributed-shapshot.png)

C is the cut taken by the protocol, C’ is the cut when the protocol has finished
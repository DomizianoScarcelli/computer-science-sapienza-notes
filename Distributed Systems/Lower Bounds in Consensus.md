---
Exam:
  - Distributed Systems
---
How many processes do I need to tolerate $f$ faults?

Tolerate mean for the system to be safe. In a synchronous system we get both safety and liveness, in an asynchronous one we only get safety since liveness it's impossible.

Remember that the FLP theorem says:

> Consensus with faults it’s impossible to solve in an asynchronous system

## Taxonomy
|  | Crash faults | Byzantine faults | Byzantine faults w/ signatures |
| --- | --- | --- | --- |
| Synchronous | $f+1$ | $3f+1$ | $2f+1$ |
| Asynchronous | $2f+1$ (Paxos) | $3f+1$ | $3f+1$ |
### Byzantine faults

Byzantine faults needs $3f+1$ nodes.

Let’s assume we have $3$ nodes and we want to tolerate $1$ byzantine fault. This isn’t possible since we haven't reached the requirement. Let’s see why:

![photo1.png](photo1.png)

$G$ is the General, $L$ is the lieutenant. $G$ has to give both the liutenants the same order, otherwise they will lose the battle.

If $G$ is byzantine, it can give $L_1$ the Attack ($A$) command and $L_2$ the Retreat ($R$) command. Since the commands are different, they will lose. In order for a liutenent to be sure they're on the same page, they could exchange messages with the other liutenent.

In case $L_2$ is byzantine, it can tell $L_1$ that the command from the general was $R$ instead of $A$, and $L_1$ would never know who between $G$ and $L_2$ is byzantine, and cannot make a safe decision either way.

In both cases, $L_1$ receives the same information.

In order for $L_1$ to be able to make a safe decision, another node is needed to reach the minimum requirement of $3f+1$ nodes. Other more or less advanced algorithms will be used in order to exchange messages with this extra node to check wether a node is byzantine or not.

![Photo2.png](Photo2.png)

### Byzantine faults with digital signature

If the system is synchronous, in case we use digital signature, then $L_2$ that receives the message from $G$ cannot counterfeit the message, so what we’ve seen previously cannot happen.

If the system is asynchronous, the byzantine node can pretend that the message didn’t arrive to it and so you still need another node. An algorithm for this case is PBFT.
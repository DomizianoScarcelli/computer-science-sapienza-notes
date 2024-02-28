---
Exam:
  - Distributed Systems
---
Paxos is a distributed protocol that solves the consensus problem that can work on asynchronous systems. 

As in other protocols that try to solve this problem, it has these rules:

- Every process has a value
- All the processes must agree on the same value
- The value the processes agree has to be inside the list of possible values

In paxos there are three types of agents: proposers, acceptors and learners. A process can be only one of them or all togheter, that doesn’t change how the protocol works. In the explaination we’re not going to assume nothing about the role of the processes.

The computation is organized in rounds and, since the system is asynchronous, the notion of round is more complex, since every process track their round, and there is not a global round counter.

Every round is associated with one and only one proposer. A round is structured in this way:

1. In its round, the proposer sends a `prepare(round_number)` to all the acceptors. 
2. The acceptors then responde with a `promise(round_number, last_round_voted, last_vote)` where:
    1. `round_number` is the round number of the `prepare` message;
    2. `last_round_voted` is the last round when the acceptor voted;
    3. `last_vote` is the value that the acceptor voted in the `last_round_voted`.
    
    In the promise the acceptor promises to the proposer that it will never take part to a round that’s less then `round_number`. So if in the future a new promise with a `new_round_number < round_number` arrives, it will discard it.
    
3. If the proposer gets a majority of votes, where the majority is computed as $n-f$ where $f = \lfloor \frac{n-1}{2}\rfloor$ is the number of crash failures the protocol can tolerate, then it sends an `accept(value)` to the acceptors. The value can be:
    1. ha
4. The acceptors, once received the `accept(value)` will send a `learn(round_number, value)` to the learners.

If the cycles goes though, then the value `value` is decided. 

![paxows.png](paxows.jpeg)

### Paxos (not) liveness

It can happen that the protocol doesn’t ever arrive to a consensus. This may happen if everytime the proposer sends an accept, a new proposer starts a new round with a higher round number than the current one, and so the previous accept will never be learnt since it would be discarded from the acceptors in the new round.

This show that paxos is not live.

### Paxos safety

Let’s define two propositions in order to prove Paxos safety:

1. If a value $v$ is chosen in round $i$ and $v'$ is chosen in round $j \neq i$, then $v = v'$;
2. If acceptor $a$ voted (sends a learn message) for $v$ in round $i$, then no $v' \neq v$ can be chosen in rounds $j < i$.

Paxos is safe if $P2 \Rightarrow P1$

Paxos is safe, since if a value is decided, if some other proposal starts a new round, the same value will always be decided.

Let’s assume a proposer P has crashed and recovers without memory of what happened. If it starts a new round, the acceptors will respond with a `promise(round_number, last_round_voted, last_vote)`, so the proposer will choose the `last_vote` and send an accept and a learn.

## Fast Paxos

Since Paxos is used to get consensus on a sequence of values, it’s possible to aggregate some messages in order to improve the efficiency of the protocol.

A single `prepare` message can be sent to initialize a sequence of Paxos instances, instead of sending a sequence of `prepare` messages and, in the same way, a single `promise` can be sent to respond to the aggregate `prepare` messgage.

The proposer that sends this aggregate message is called the *coordinator*. When a proposer has a value, it sends it to the coordinator. The coordiantor then complete the instance by sending an `accept` message to the acceptors that will be followed by a `learn` message.

A coordinator can also start a ***fast-round*** by sending a special aggregate message in response to the `promise` aggregate message that’s called `accept-any`. The meaning of this message is that the acceptors can accept any value they receive from any of the proposers in the same round.

The `accept-any`message that characterizes the fast round allows multiple proposers to send a value to the acceptor, so in the same round multiple values can be voted by the acceptors. This wouldn’t happen in Paxos since in every round only one value could be voted.

To make fast paxos safe it’s necessary to change the concept of “majority”, that goes from $n-f$ with $f= \lfloor\frac{n-1}{2}\rfloor$ to $n-f'$ where $f'= \lfloor\frac{n-1}{3}\rfloor$.

> [!Note]
> ✏️ ***Why doesn’t the classic quorum work?***
Let’s assume we just need a quorum of $n-f$ acceptors, with $n=7$ and $f=3$.
> 
> During round $i$, the proposer responsible for round $i$ collects $n-f = 4$ promises for the acceptors, some have the form `promise(i, j, 1)` and others have the form `promise(i, j, 2)`.
> 
> The problem is that the coordinator doesn’t know what's the vote of the remaining $f=3$ acceptors, and this will influence the final vote since a majority on value 1 or value 2 can form depending on these votes, so the protocol cannot safely agree on a value for round $i$.

Let’s call $Q$ the set of $n-f'$ acceptors, and $Q_j \subseteq Q$ the set of acceptor that last voted in round $j$, where $j$ is the current highest voted round in the promises. Let also $Q_j[v] \subseteq Q_j$ be the set of acceptors that last voted value $v$ in round $j$.

Since there is no guarantee that all the acceptors have voted for the same value in the round $j$, it’s necessary to change how the value that is sent into the `accept` message is chosen. The new rule become the following:

- If $j=-1$, it means that no acceptor in $Q$ has voted yes, so the coordinator can start a fast round;
- if $j \geq 0$ and exists a value $v$ such that $|Q_j[v]| \geq n-2f'$ (there is a big majority for the value $v$), then select $v$ (there can be at most one value $v$ with that property);
- if $j \geq0$ and for every value $v'$ we get $|Q_j[v]| < n-2f'$, then select any value that has been last voted in round $j$;

### Fast Paxos safety proof
> [!TODO]
> Missing :(

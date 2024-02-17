
## Space-Time Diagram

During the processes, events occur, and we model these events with the space-time diagram.

![Untitled](assets/Untitled.png)

## Some terminology: History, Run, Local State, Global state, and Cut

- History of a certain process $P_1$: $h_1 = e_1^1 e_1^2 e_1^3...$ the sequence of events that occur inside that process;
- Run or computation is a sequence of events $R = e_1^1 e_2^2 e_2^3 e_1^3$.
A run can be **legal** or **consistent** if it can actually be run in the system, **illegal** or **not consistent** otherwise;
- **Local state** $\sigma_i^k$ is the state of the process $i$ after the execution of the first $k$ events. (first $k$ events are $h^k = e_h^1…e_h^k$);
- **Global state**: the execution of the first $n$ local states ($\sigma_1^k, \sigma_2^k, …, \sigma_n^k$). A global state is consistent if $e \rightarrow e' \land e \in S \Rightarrow e' \in S$;
- **Cut**: a subset of the history of the computation (subset of $h_1^{k_1}, h_2^{k_2}, …, h_n^{k_n}$);

We say that an event “happened before” with the notation $→$ (this operator is transitive)

- $e_i^l → e_i^k$ if $l<k$ ($i$ is the same so we’re in the same process)
- $e_i → e_j$ if $e_1$ is sending the message $m$ and $e_j$ is receiving the same message $m$

**Consistent cut**: a cut $C$ is consistent if and only if: $e→e’ \land e’ \in C ⇒ e\in C$. If a cut is consistent, a consistent run surely exists. 

### Some questions

**Question**: Does $e_1^1$ happen before $e_2^1$? It cannot be said, because the question has no meaning. The order depends on the run. 

**Question**: Does $e_1^1$ happen before $e_1^2$? Yes, since these two events happen in the same process, so there is an order. That’s because $e_1^1$ can influence the following events.

**Question**: Does $e_1^3$ happen before $e_2^2$? Yes because since $e_1^3$ sends a message to $e_2^2$, the second process depends on the first one and since it has to happen after.  

## Deadlock

Every time I ask for information I have to wait some time for a response. A deadlock is a situation where some devices are in a waiting loop because they’re waiting for each other.

### Wait-for graph

The wait-for graph is a way to detect if there is a deadlock in the system.

The processes are the nodes of the graph and if a process $A$ is waiting for the response of a process $B$ an edge is made. If there’s a cycle in the graph it means a deadlock is present.

### Ghost deadlock

We call $P_0$ the process whose purpose is to detect a deadlock. This process sends messages to the other processes and gathers responses in order to build the wait-for graph.

Since the system is asynchronous, a message sent from $P_0$ can arrive sometime later. 

As we can see from the picture, $P_0$ is getting a snapshot of the situation at different times from different processes (it's gathering information of the processes at different points in time), since the time that a message spends to arrive is different from a process to another.

![Untitled](Untitled%201.png)

In this example, $P_0$ detects a deadlock where there isn’t. This particular case is called a **ghost deadlock** 

![$e_1$ is in the future and sends a message to $e_2$ that’s in the past, so this cut isn’t consistent.](Screenshot_2022-10-11_at_1.24.30_PM.png)

$e_1$ is in the future and sends a message to $e_2$ that’s in the past, so this cut isn’t consistent.

## Lamport Clock

The problem that the Lamport clock is trying to solve is how can $P_0$ take a snapshot of a consistent run in order to only detect real deadlocks.

- Trying to find the solution
    
    We assume that all the processes have access to a global clock (that’s something that doesn’t exists, but we make this assumptions to try to solve the problem)
    
    First solution (complicated it’s not convenient): $P_0$ sends a message like “send me the local state in the $t_p$ timestamp. So the process $p$ waits until the timestap to send the local state.
    
    Another solution is to set a time $t_0 + \Delta$ and capture the snapshot in that instant. The problem is what if the message doesn’t arrive in time? We has to try again, and that’a a problem. This would work in case of existance of a global clock, that makes sure that no future messages can be send to the past.
    
    Global clock doesn’t exist, so we need another solution.
    

> [!Clock Condition]
If $e → e’$ then $TS(e) < TS(e’)$ where $TS$ is the timestamp.
Note that the arrow in the other way is not true, since if the two events are not correlated nor one or the other happens before the other, they’re concurrent.

The clock condition is always true if there is a global clock, but since processes in a distributed system don’t have access to a global clock, there is a need to invent a new type of clock that has the clock condition.

Every time an event occurs in a process, it labels it with a serial number (1,2,3 etc.). If a process $P_1$ makes an event that sends a message to a process $P_2$,  $P_2$ labels it with the next number of the greatest next number between $P_1$ and $P_2$.

![Untitled](Untitled%202.png)

In this way, $P_0$ can reconstruct the run in a consistent one, and the problem is solved without the use of a global clock.

This new clock that we discovered is called **Lamport clock**, invented by Lamport in the 70s.

The order that $P_0$ sees may be slightly different from the real order, but it’s important since the order change happens between non-correlated events, so the two runs are both consistent.

## Consistency of intersection and union of cuts

**Hypothesis**:

If $C_1$ and $C_2$ are two consistent cuts, then $C_1 \cap C_2$ is a consistent cut.

**Proof:**

We know that if

$$
e → e’ \land e’ \in C_1 \cap C_2
$$

then since $e \rightarrow e'$, $e$ will be in every cut that includes $e'$, so

$$
e \in C_1 \land e \in C_2 ⇒ e \in C_1 \cap C_2
$$

**Hypothesis**:

If $C_1$ and $C_2$ are two consistent cuts, then $C_1 \cup C_2$ is a consistent cut.

**Proof:**

Similarly to the proof for the intersection, we know that if

$$
e → e’ \land e’ \in C_1 \cup C_2 
$$

then since $e \rightarrow e'$, $e$ will be in every cut that includes $e'$, so

$$
e \in C_1 \lor e \in C_2 \Rightarrow e \in C_1 \cup C_2
$$

## Logical Clocks and stable messages

A Lamport clock is a type of logical clock. Logical clocks are all clocks that have the clock condition.

When $P_0$ receives a message, we make a difference between receiving and delivering:

- Received means that the messages arrive at $P_0$, but other messages previous to that one may still arrive in the future
- Delivered means that the message is accepted by $P_0$ and can be processed since no other messages previous to that one can arrive in the future;

$P_0$ will deliver a message $m$ only if it's **stable**. 

> [!Stable Message]
Message $m$ is stable at $p_i$ if no message $m'$ such that $TS(m') < TS(m)$ can arrive in the future.

![The received message 2 is not stable because I still can receive a 1 in the future, and 1 < 2. ](Untitled%203.png)

The received message 2 is not stable because I still can receive a 1 in the future, and 1 < 2. 

A way that $P_0$ can recognize a message as stable is to implement channels as FIFO (First In First Out), in this way when it receives a message, it knows that all the previous messages have already arrived.

We define the array $D[i] = \text{highest TS received from process }i$ . In the start, $D$ is composed of zeros and has the length of the number of processes.

In this way, a message received from $P_0$ is stable only if all the other values in the vector are greater than the $TS$ of the message received. That’s because in order to deliver a message, all the messages with the $TS$ lower than the received message have to be delivered too, since the current message may depend on one of them. 

![TODO: Change the vectors because they’re wrong](Untitled%204.png)

> [!TODO]
TODO: Change the vectors because they’re wrong

This is a solution but it's not perfect, since it can raise some problems.

The first problem is that, in order to deliver a message, the process has to wait for all the processes with lower TS to arrive, and this could cause the process to wait forever to deliver a message.

This can happen because a message with a low $TS$ doesn’t arrive because of a failure.

Another cause could be seen in the picture: the message from $P_2$ with $TS = 5$ will not be delivered until a message with $TS = 4$ is received from $P_1$ and $P_3$, and since $P_3$’s last message has $TS  = 3$, it will wait forever.

## Strong clock condition

A strong clock condition is a clock condition that is valid in both ways.

$$
e \rightarrow e' \Leftrightarrow TS(e) < TS(e’)
$$

Logical clocks don’t have this condition:

![Untitled](Untitled%205.png)

In this picture, we can see how $TS(e') < TS(e)$ but it's not true that $e'\rightarrow e$, since they’re concurrent.

If two events in two processes are concurrent, it’s hard to assign them a numerical $TS$. 

As we can see from the picture below, the timestamps 4-5 or 6-5 are not right because no event happens before one another. 
I cannot give them 5-5 because if then another event happens I would have 5-6, but it’s not true that the event with $TS = 6$ on the first process happens before the event on process 2 with $TS = 5$.

![Untitled](Untitled%206.png)

So we arrived at the fact that a numerical $TS$ is not enough in order to have a strong clock condition.

## Causal history

> [!Note]
🔁 Causal history of an event $e$
$\theta(e) = \{ e' \in H : e'\rightarrow e \} \cup\{e\}$

The causal history is the set of events that may have contributed to the event $e$.

![Untitled](Untitled%207.png)

$$
\theta(e_1^1) = \{e_1^1\} \\
\theta(e_2^1) = \{e_3^1, e_2^1\} \\
\theta(e_2^2) = \{e_1^2, e_1^1, e_2^1, e_3^1, e_2^2\}

$$

> [!Note]
> If $e \rightarrow e' \Rightarrow \theta(e) \subseteq \theta(e')$
It’s true also in the other direction, since $\theta(e) \subseteq \theta(e') \Rightarrow e \in \theta(e') \Rightarrow e \rightarrow e'$
So it’s true that $e \rightarrow e' \Leftrightarrow \theta(e) \subseteq \theta(e')$

In order to avoid the problems that the solution above raised, we can timestamp the messages with their causal history. 

This obviously can bring problems with efficiency, since the causal history of an event can be very big.

## Vector clock

To solve the problem of the causal history is big, we can timestamp an event not with the entire history, but with just the last event that’s part of the history, In this way all the other past processes in history become implicit.

> [!Note]
🕰️ Vector clock:
$VC[i] = \text{internal clock of the latest event inside process }i$

This type of clock has a strong clock condition.

![Computed vector clocks for all the events in the processes](Untitled%208.png)

Computed vector clocks for all the events in the processes

If the vector is of the type $[0,0,2]$, $P_0$ know that this is the 2nd message sent by $P_3$, and it knows that that message doesn’t depend on $P_1$ or $P_2$, since the values on those positions are zeros.

In case the last $VC$ is $[0,1,2]$ and $P_0$ receives $[2,2,1]$ it cannot receive it because the message depends on two messages of $P_1$ that it didn’t receive yet.

With the Vector Clock, $P_0$ can deliver all the messages that can be delivered, different from before.

The vector that $P_0$ keeps to keep track means $[i,j,k]$ i received $i$ messages from $P_1$, $j$ messages from $P_2$, and $k$ messages from $P_3$. The vector that $P_0$ keeps is not a TS, but it’s only a vector to make a comparison with the VC it will receive.

# Atomic Commit

When a client connects to the server, maybe it’s an ATM and it has to decice if the user can or cannot withdraw some money, it can commit the transaction or abort it. In order for a commit to be valid, there are some properties that have to be followed:

1. All processes that reach a decision (commit or abort) must reach the same one.
2. A process cannot change decision after reaching one.
3. That “commit” decision can be reached only if all processes vote yes (if just one process doesn’t agree the commit cannot be reached) ($\text{commit} \Rightarrow \text{all voted yes}$)
4. If there are no failures and all processes voted yes, then the decision must be “commit”. 

### System synchronous and no failures

![0-failures.png](0-failures.png)

This is the simplest case, since all the nodes broadcast their decision to all the other nodes. Since there are no failures, all nodes know all the votes, and so they commit only if all the votes are yes, otherwise they abort. 

### System synchronous and 1 failure

![1-failures.png](1-failures.png)

> [!TODO]
SEE AGAIN THIS PART: How can a single node know that an error has occurred?

### System synchronous and $n$ failures

![n-failures.png](n-failures.png)

## 2-Phase Commit

2-Phase commit is an atomic commit protocol.

This protocol contains a coordinator and many participants. The coordinator is chosen before runtime, that’s because choosing a coordinator at runtime is a problem of consensus and so it would be another problem.

The protocol works like this:

- The coordinator sends a “vote request” message to the participants, in which it asks the vote of a participant, that would be yes or not;
- When the participant receives the “vote request”, it chooses its vote and:
    - If it’s yes, sends Yes
    - If it's no, sends No or abort the process
- When the coordinator receives all the votes from the participants:
    - If all the votes are yes, it sends a “commit” message to the participants;
    - Otherwise, it sends an “abort” message to the participants.
- When the participant receives the “commit” or “abort” message from the coordinator, they do the action.

![Senza titolo-2022-10-11-1322.png](Senza_titolo-2022-10-11-1322.png)

The protocol has to be tolerant to failures. Let’s assume there could be a lost message or a process crash.

Both the coordinator and the participants cannot wait forever for a message, so they embed a timeout after which they do something.

If a partecipant don’t receive a message from the coordinator once the timeout is over, they abort (it’s safe to do so).

If the coordinator doesn’t receive the message of a partecipant once the timeout is over, they send an “abort” message. This solution is safe since it doesn't go against the properties. (The fourth property assumes there would be no failures).

What if a partecipant doesn’t receive the final “commit” or “abort” message? What should it do? Aborting would not be safe since the message could be “commit” and all the other processes would commit.

If the process has voted “Yes”, the solution is to ask to another process if they’ve committed or aborted and follow their lead. If also the other process it’s waiting the protocol it’s stuck.

If the process has voted “No”, it have already aborted or the message would surely be “abort, so there is no problem. 

The probability of being stuck is low but possible, since the problem cannot be solved in any case.

### Safety vs Liveness

- A process is **safe** if it doesn’t do anything wrong
- A process is **live** if it does something (wrong or not)

A dead computer is safe but not live. Safety came before liveness, but they’re both very important.

### 2-Phase Commit Recovery

If a process crashes, it should be able to reboot and recover its state after a certain interval of time in order to complete the transaction anyway. This could be achived by logging.

The log is local to the process, since we cannot have a global log. This log is called DTLog and it works like this:

1. When the coordinator C starts the transaction, `DTLOG <- start2PC` and adds some details like the partecipants list, the id of the transaction and other things.
2. When a partecipant P votes, there are two cases:
    1. It votes “Yes”, then `DTLOG <- yes` **before** sending the vote.
    It’s important to log before sending the vote because if the process sends the vote and then crashes, it would recover, look at the log, see nothing and then abort. This will not be safe since the message sent is yes and the cordinator may send commit.
    2. When P votes No, then `DTLOG <- no` either **before or after** sending the vote.
    In this case it's not important to log before because either the process crashes or not it will abort anyway.
3. When C sends the “commit” or “abort” messgae, there are again two cases:
    1. When C sends commit, then `DTLOG <- commit` before sending the message.
    Before because if C crashes, it finds only `start2PC` and if it sends an abort it would not be safe.
    2. When C sends abort, then `DTLOG <- abort` before of after sending the message.
4. When P receives the decision, then it logs it in `DTLOG`.

## Chandy-Lamport Protocol for Distributed Snapshot

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

# Paxos protocol

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

![paxows.png](paxows.png)

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
# Bitcoin

The concept of Bitcoin relies on cryptographic methods, such as hash functions and public key crypto.

## Hash function

An hash function is a function with these properties:

- Given $H(x)$ is very hard to find $x$;
- It’s hard to find a $y \ne x$ such that $H(y) = H(x)$;
- It''s very hard to find a $z$ such that $z = H(x)$.

The hash function can take a large input and map it to a relatively small hash, so it can be used to map large domains to small domains.

It’s not possible to know if a function with those property exist, there are some functions that seem to have those but we cannot be sure. (For example RSA now seems a secure algorithm, but also MD5 seemed safe and now it’s completely broken).

### Public Key crypto

A process has two keys, one private $k_1$ and one public $k_2$. The keys are connected, in a sense that if you encrypt a message $m$ with the public key you obtain $m'= E_{k_2}(m)$ and if you encrypt $m'$ again with the private key you obtain $m$ back $m = E_{k_1}(m')$ and vice versa.

The public key can be available to everybody, meanwhile the private key must be a secret. If someone want to send a secret message that only the one with the private key can decrypt, they encrypt it with the public key, in this way only the person with the private key can get the original message.

This method also allows to sign a message, by just doing the process the other way around, meaning I encrypt the message with the private key, and who wants to read it decrypt it with the public key. Since I am the only person with the private key, the message could only be signed by me.

Signing can also be used to prove that the message hasn’t been compromised: I can hash the message, encrypt it with the private key and attatch this sign at the end of the message. Who wants to read it can decrypt the sign with the public key in order to get the hashed message, to see if the message has been compromised they can just hash the message with the public key and compare the two hashes, and if they’re equal the message is the same that I’ve sent, otherwise it has been compromised.

A bitcoin is represented by a file that embeds the following informations:

- Numbers of bitcoins
- The owner, represented by the public key
- The hash of the file (in order to protect the integrity of the message)

![Bitcoin structure](BTC.png)

### Bitcoin structure

If I want to make a transaction and give the bitcoin to someone else, let’s assume the other person’s public key is $k_3$, I have to prepare a new file that embeds the following informations:

- The same hash of the file I own;
- The new owner, represented by the public key $k_3$
- The signature, meaning the hash of the entire file encrypted with my private key

To make a transacton you need the private key, to check it just the public key is needed. If the private key is lost, then those bitcoin are lost and cannot be given to anyone anymore. If someone steals your private key, also those bitcoin are lost since they can make a transaction.

![Transaction](BTC_transaction.png)

### Transaction

There is a fundamental problem in this procedure, that’s called double spending. Nothing prevents me from giving the same bitcoin to two different people. This problem is solved with the construction of a blockchain.

![Double spending](BTC_double_spending.png)

### Double spending
[[Double Spending]]

## Blockchain

The blockchain consists in a public ledger where everybody can add a transaction but nobody can remove it. This public ledger solves the problem of double spending since if a transactiojn it’s registered there, those bitcoins cannot be spent anymore by the same owner.

A single block on the blockchain is a file containing a fixed amounts of bitcoin transactions and the hash at the end. The transaction is commited only when it appears in the blockchain.

Since the bitcoin is based on the fact that there is no central authority, many copies of the blockchain are stored in many servers, in order to distribute the system. The next block to put in the blockchain is decided with a consensus protocol. As seen previously, paxos cannot be used since it’s not tolerant to byzantine failures, and since everyone can own a blockchain server, those server cannot be trusted. 

The consensus protocol uses a concept called proof of work.

### Proof of Work

There is a property that tells us that a valid block have an hash $H$ with the $k$ least significant bits set to zero.

Every new proposed block has to be valid.

Every block has also a Nonce, that’s a value that has some arbitrary value that makes the hash satisfy the property. The only way to find this value is by brute-forcing all the values, so it’s a computational hard operation. 

A node that tries to compute this value in order to try to add a new block into the blockchain is called a miner (the process is called mining).

The number $k$ of lest significant bits that have to be set to zero is changed every few weeks in order that a new value is found every 10 minutes by one of the nodes in the system.

When a node find a valid block, it can propose it to all other nodes in the network, and since the only way to discover a nonce that make the block valid is through work, this is called Proof of Work.

Let’s assume that $k=32$, in I have to do $2^{32}$ tries. The typical server has to do $2^{32} \sim \text{4 billion}$ hashes in order to make the block valid, and send it to other servers.

All the transactions that are made in between the computations are inserted into a pool, and inserted in the block whenever is possible.

Only the most powerful and luckiest computers in the network can extend the blockchain with a new block. Every time a node insert a new block, it gets a reward of about 6.25 BTC.

### Fork

It can happen that two servers around the world find the new block in the same time, broadcast it to everybody and half of the server think block 1 is the new one, and the others think block 2 is the new block. This is called a fork of the blockchain.

Half of the servers try to extend block 1 and the other half try to extend block 2.

It can happen that the two forks go on in parallel, but probabilisticly at one point one branch of the blockchain will be longer, the new block will be broadcasted to everybody, and they’ll see that that branch is longer, and they stop to work on the previous branch, so the blockchain is not forked anymore. The branch becomes a dead branch.

All the servers work on the longest branch, so forks probabilisticly don’t last long. Transaction in dead branches aren’t valid anymore. They’re put again in the pool and they will appear in the current branch.

### Proof of Stake

The problem of Proof of Work is that it takes long to commit a transaction.

On average a new block is inserted every 10 minutes, but you don’t ever know when your transaction will be inserted in the new block. You need to wait at least 60 minutes to be sure that you're not on a dead branch (you should have 6 blocks more in the blockchain after the transaction), but the transaction coul be inserted in the pool everytime a new block is proposed.

Proof of Stake solves this problem and the problem of forking. This becase the new block don’t need to have the hash property that the miners brute-forced to obtain, but the server that can push a new block is chosen probabilistically from all the servers that have some quantity of coin in their wallet.

In a more detailed way, every coin is like a lottery ticket, and more coins a server has, more probability of being chosen. 

Proof of stake requires less energy and transactions are committed faster.

# Anonimity in the Internet

There are some ways to achieve anonimity in the Internet, every method guarantee some level of anonimity from someone.

For anonimity to work, there is always something that has to be trusted.

1. Incognito mode in the browsers: in this case you don’t get anonimity from your Internet Service Provider or the Government. You’re getting anonimity from other people that want to use the same computer.
The trusted entity that guarantees anonimity is the browser.
2. VPN: in this case you don’t connect directly to the final server, but you connect first to a proxy, and than this connects to the server. 
You get anonimity from ISP but not on the Government, since they still can get a log of connections from the VPN provider. 
The trusting entity is the VPN provider.
3. TOR provides anonimity from both the ISP and the Government.

## TOR - The Onion Router

Inside TOR there is a list of arunt 7.000 TOR servers, spread everywhere in the world.

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

The decision about the session key happens with the Authenticated Diffie Hellman protocol. Before that, we should look at how the classic Diffie Hellman protocol works.

### Diffie Hellman protocol

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

---

We use authenticated Diffie Hellman with the guard server $A$ to agree on a session key and encrypt messages faster. Than I can talk to $B$ through $A$ and to $C$ through $B$ in order to agree on two more session keys.

Latency is not very good. Bandwidth can be the same as the direct connections.The problem is that some nodes are not very fast, so it depends on the service of every node in the circuit.

### TOR Vulnerabilities

The anonymity is lost if the guard and the exit node is owned by the same person. This person can notice that everytime a message is sent to $A$, it arrives to $C$ very fast, so the connection can be de-anonymized.

In order to overcome this vulnerability, it’s important for TOR to choose the guard and the exit node in order that they’re not owned by the same person. This can be achieved by choosing two nodes in very different geographical zones.

## Dark Web

The Dark Web is a list of secret servers whose location is unknown.

A TOR server it’s chosen as a randez-vous point, in order to connect to the final secret server, you talk through the randez-vouz server using TOR, and that server talks to the final server using TOR.

The url of the servers in the Dark Web ends with .onion.

# Algorand
If you want a more in-detail description, check out [[Algorand|Blockchain and Distributed Ledger Technologies - Algorand]]

---
Algorand is a cryptocurrency that was founded to solve the “blockchain trilemma”, that claims that any blockchain can have at most two out of the three desirable properties: decentralization, scalability and security.

Most blockchain based on proof of stake use delegated proof of stake. This is a variation of the pure PoS in which only a certain subset of validators can decide a new block, and each node in the network delegates its power to the validator. This technique is faster than the classic PoS, but decreases the decentralization of the system.

Algorand uses pure proof of stake. The nodes in the network communicate using the gossip protocol.

In order to solve the problem of pure PoS being slow, Algorand uses relay nodes.

A relay node is a very fast computer with a very fast network hosted in some trust entity. The purpose of those relay nodes is to forward the information to all the other nodes in the neighborhood. The relays are distributed in a logical way all around the globe.

Algorand uses another optimization technique, introducing the archival nodes. All the nodes only stores a part of the blockchain (e.g. 1000 blocks). Only the archival nodes store the whole blockchain. They can be either relays or participant, and they're logically geographical distributed too.

For reasons regarding decentralization and security, not all nodes can partecipate to the consensus protocol.

For example relays shouldn’t partecipate to the consensus protocol since they are much more powerful than all the other nodes.

Archival nodes also shouldn’t partecipate to the consensus protocol. 

| Relay? | Archivial? | Partecipates? | Comment |
| --- | --- | --- | --- |
| Relay | Archivial | Partecipation | It’s not secure. |
| Relay | Archivial | Non patecipant | It’s the normal configuration for a relay |
| Relay | Non archivial | * | Impossible |
| Non relay | Archivial | parecipation | It’s discouraged, since nodes that partecipate to the consensus shouln’t be archivial |
| Non relay | Archivial | Non parecipant | Normal configuration for an archivial node |
| Non relay | Non archivial  | Partecipant | Normal configuration for a partecipant node |
| Non relay | Non archivial  | Non partecipant | Normal configuration for a node that is used to submit transaction to the blockchain and access the current state, but not the historical state. |

Algorand needs $2 \over 3$ of the majority, instead of the $\frac{1}{2}$ used by Bitcoin.

## Consensus protocol

Algorand uses a decentralized Byzantine Agreement protocol, in which it’s possible to achieve consensus without a central authority and malicious users are tolerated as long as the supermajority ($2 \over 3$) of the stake is non-malicious.

Algorand’s consensus protocol is divided in three phases:

1. Sortition (or block proposal)
2. Vote casting (or soft vote)
3. Agreement (or certify vote)

Before going deeper into the three phases, it’s important to define what’s a verifiable random function VRF.

### VRF - Verifiable Random Function

Since the nodes have to be chosen at random, it should be impossible in advance to know who are the members of the committee. The nodes also must have the possibility to randomly choose themselves.

A verifiable random function is a function that takes in input the secret key $sk$ of the node, the random seed, the role from which to choose a node (Proposers or Committee) and outputs a pseudo-random Hash and a proof.

$$
VRF_{sk}(\text{seed}|\text{role}) = (\text{hash}, \text{proof})
$$

The proof is used to verify that the generated hash is truly random. We can do this by applying another function:

$$
\text{Verify}VRF_{pk}(\text{hash}, \text{proof}, \text{seed}) = \text{true|false}
$$

where $pk$ is the public key.

### Sortition

We need to form a set of proposers, committee and observers. 

Each ALGO has a set of $\langle sk, pk \rangle$ keys, and every node runs the function of every ALGO it owns. As result, we’ll have the same numbers of $\langle \text{hash}, \text{proof}\rangle$.

The algorithms then divides the domain in an $[0,1]$ interval by dividing every hash by $2^{\text{hash}}$. 

Given a threshold value $t \in [0,1]$, a node is member of the group only if it’s hash is lower than $t$. This procedure is done for every role, and in the interval there are only the hashes of the same role.

The threshold $t$ is set in order to have the right number of proposers and committee (in the case of committee the number is around 1000).

This is done since Algorand uses PBFT, and this protocol cannot be execute with a large number of nodes.

### Vote casting
The purpose of this phase is to filter the number of votes that go around the network, in order to prevent an eccessive flooding.

Every node can have more than one ALGOs, so it can be multiple proposers at the same time. We want the node to cast only the vote, that will be the one with the highest priority.

In order to determine the vote’s priority, we compute the hash of the result of the $VRF$, concatenated with the algo index, for every algo.

$$
H(VRF|ALGO_{\text{index}}) = \text{hash}
$$

The node will broadcast only the hash with the highest numeric value.

When a node receives an hash from another node, it sorts the hashes it has received, and only broadcasts the hash with the highest value.

If a node gets partially disconnected because some errors, and doesn’t receive any vote for the other nodes. After a certain timeout It broacasts an Empty value.

### Agreement

In this phase, the proposer have to agree on the same proposed value, or on the empty value.

The consensus on the next block is then chosen with PBFT between the nodes. (?) and once the block is decided by the committee, the information is broadcasted to the rest of the network.

From Algorand Website:

> A new committee checks the block proposal that was voted on in the soft vote stage for overspending, double-spending, or any other problems. If valid, the new committee votes again to certify the block. This is done in a similar manner as the soft vote where each node iterates through its managed accounts to select a committee and to send votes. These votes are collected and validated by each node until a quorum is reached, triggering an end to the round and prompting the node to create a certificate for the block and write it to the ledger. At that point, a new round is initiated and the process starts over.

# Failure Detector

Let’s assume some process $p$ exists with a failure detector library $D_p$. Process $p$ can ask to $D_p$ if a certain process $q$ is crashed.

- If $q \in D_p(t, \sigma)$ (time $t$ and run $\sigma$) then $D_p$ believes that $q$ is crashed’
- $\text{crashed}(t, \sigma)$ is the set of all the processes that have crashed at time $t$ with run $\sigma$;
- $\text{up}(t, \sigma)$ is the set of all the processes that are running at time $t$ with run $\sigma$.

### Failure detector properties

1. **Strong completeness**: (For every process $p$ crashed in any run, if another process $q$ is up, then in some time in the future $q$ is going to know that $p$ is crashed.)
Formally: $\forall \sigma \forall p \in \text{crashed}(\sigma) \forall q \in \text{up}(\sigma) \exists t' > t : D_q(t', \sigma) \ni p$
2. **Weak completeness**: If $q$ is crashed, not every process is going to know it.
Formally: $\forall \sigma \forall p \in \text{crashed}(\sigma) \exists q \in \text{up}(\sigma) \exists t' > t :D_q(t', \sigma) \ni p$
3. **Strong Accuracy**: If the failure detector says that a process is crashed, then it’s true for every crashed process.
Formally: $\forall \sigma \forall t \forall p, q \in \text{up}(t, \sigma):p \notin D_q(t,\sigma)$
4. **Weak Accuracy**: If the failure detector says that a process is crashed, for some processes this is true, for other’s not.
Formally: $\forall \sigma \forall t \exists p \in \text{up}(t, \sigma) \forall q \in \text{up}(t, \sigma): p \notin D_q(t,\sigma)$
5. **Eventually strong accuracy**: It’s the same as strong accuracy, but it's not true at every time $t$, but it assures that some time $t'$ where it's true exists.
Formally: $\forall \sigma \exists t \forall t' > t \forall p, q \in \text{up}(t', \sigma):p \notin D_q(t',\sigma)$
6. **Eventually weak accuracy**: Same as the eventually strong accuracy but with weak accuracy.
Formally: $\forall \sigma \exists t \forall t' > t \exists p \in \text{up}(t', \sigma) \forall q \in \text{up}(t', \sigma): p \notin D_q(t',\sigma)$

It’s easy to make a failure detector that’s complete, since you just can always say that a process $p$ is crashed. 

Both the strong and weak accuracy has to be valid for every $t$, differently for completeness, otherwise we have eventually strong and weak accuracy.

### Failure detector taxonomy

|  | Strong accuracy | Weak accuracy | Eventually strong accuracy | Eventually weak accuracy |
| --- | --- | --- | --- | --- |
| Strong completeness | $P$ (Perfect) | $S$ (Strong) | $\diamond P$ (Diamond P) | $\diamond S$ (Diamond S) |
| Weak completeness | $\Theta$ | $W$ (Weak) | $\diamond \Theta$ | $\diamond W$ |

### Failure detector for leader election in Paxos

A perfect failure detector can make paxos live.

One way to do it is to elect a leader, meaning a proposer that’s not crashed.

We take the process with the smallest id that’s not crashed and elect it as leader. In general, there is no way to be sure if the process is crashed or not, and there is the risk that two or more partecipants could be elected as a leader. This because maybe the process with id $i$ responds with a very slow message, so we think that’s crashed and elect as leader $i'$, but also $i$ thinks to be the leader.

This problem is solved with the perfect failure detector, since the process with id $i$ asks to $D_p$ if all the other processes with id $i'<i$ are dead, if they are, then it’s sure to be the leader.

If a failure detector says that a process it’s up, than it's not sure it’s true. I’m sure that completeness would evetually work, so It’s probable that for some time I won’t get a leader, but after some time it’s sure a leader will be elected, and it’s sure that there will never be two leaders.

If the system is asynchronous, then a failure detector cannot exists, otherwise it will make paxos live and this is impossible in case of asynchronous systems.

### How to code a failure detector

Let’s assume the **system is synchronous** and we know the delay $\Delta t$.

```
For every process q:
	ping q
If q doesn't respond in time 2 * delta_t:
	add q to D_p
Repeat prediodically (like every 2 * delta_t)
```

In a synchronous system, we have strong completeness and strong accuracy, and so the failure detector is in $P$.

If we are in a synchronous system, but we don’t know the maximum delay $\Delta t$, we get strong completeness and eventally strong accuracy.
What we can do to update the delay is to double it everytime some process $p$ that was believed to be crashed it’s actually not. Since the system is synchronous, it will exist some time in the future when we reach a delay that’s greater than the maximum delay of the system, and so there will be accuracy. At the start the failure detector could give false positives.

If we are in an **asynchronous system**, we still have completeness, because if a process doesn’t respond it can be believed as crashed.
We don’t get accuracy, not even eventually, since the delay could be very high so that it’s impossible to reach it. In asynchronous systems it’s impossible to get accuracy (Otherwise we could make Paxos live, and this is impossible because of the FLP result).

### Real scenarios

In real distirbuted systems all systems are never really synchronous or asynchronous, but generally they’re synchronous for the most time and then go asycnhronous after a while, so an algorithm like that it’s usually useful.

It’s useful for example in case of a duplicated server: if the master goes down, the copy could automatically replace it. It cannot be perfect, but it’s usefull in the real world.

# Peer to Peer

P2P comes handy when we have a large file to share that some people want to download at the same time. A normal architecture would overload the single server that has the file.

The idea is to make a distributed system in which every person (peer) that downloads the file, also makes it available to other peers. The server has just the role of distributing the file initially, and then the system should work between the clients.

A file in BitTorrent is distributed in different blocks inside many clients, and those blocks can be downloaded in parallel.

The file that has to be downloaded is described in a file with the `.torrent` extension. Inside this file the hashes of all the blocks that make the file are described. The size of the block is usually 0.25MB.

The `.torrent` file also stores the url of the tracker, that is a peer that has the informations about all the peers that share the file. You can ask the trackers for a list of peers that have the file, and download it. The tracker also has the information about the blocks and the statistics about the peers. The tracker can be chosen by the peers or sometimes there are some other servers that are trackers for several files. 

The list that the tracker gives us is a partial list of peers, that is a subset of the entire list. Tipically this subset is chosen randomly.

When you start downloading, you should start from a certain block. One idea is to select the rarest block first, in order that rare blocks are shared a little bit more than the others in order to assure avaliability. 

Another policy is just by choosing it randomly. This because there is a problem with the rarest block: you can take a long time to start, since the rarest block can be anywhere in some computer with a low bandwitdth.

## Problems with P2P

### Last block (Endgame Mode)

The last blocks of the file could be rare, and so their download could be a lot slower. In order to solve this problem, the last blocks or the last one is split in other sub-blocks that are downloaded in parallel. This is called endgame mode.

### Choking

If a certain peer has to upload a file to too many peers, its bandwidth could be saturated.

A solution is to choke (interrupt) some of the connections to some particular peers. Usually only 4 peers are unchoked and selected for the upload. The problem here is how to select them:

- **This-for-that**: this method is about unchoking a peer only if they unchoke you back. The idea is to avoid free-riders, meaning the peers that download the file and then leave without uploading it, since they are bad for the entire system.
- **Optimistic unchoking**: when a new peer wants to download a file, it starts without any block. Using the previous strategy, the peer wouldn’t have any block to upload and so would be choked by all the other peers. With optimistic unchoking 1 out of 4 peers is randomly chosen, otherwise it couldn’t download the file.

## Vulnerabilities

The peer to peers system has some vulnerabilities, meaning it’s possible in some way to distrupt the system in these ways:

- Track the trackers and take them down;
- Inject some nodes in the system that don't do anything;
- Poisoning, meaning inserting fake blocks in order to corrupt the whole file. This is not easy since the .torrent file stores the hashes of the block, that allwos to discard a fake block by checking the hash.
- Poisoning the whole file, by inserting a file with the same name of the original but with different “garbage” content. For a peer to realize the content is different, it has to download it, but it will also upload it and the file would be distributed in the system. This is done mainly when you don’t want a certain content to be available.

# Lower Bounds in Consensus

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

# Akamai

If there is a CDS (Content Delivery Service) like CNN and users that want to get the service, there is the problem of overload, since a lot of users want to access to the CDS.

A better way to do this is having many servers around the world, and the user will somehow connect to the nearest ones. This can be achieved with an ad hoc solution, but Akamai found a generalized solution.

The problem with Internet protocols is that once the protocol is deployed, it’s very hard to change it in the future.

The idea is to use DNS, and whenever an user asks for the CDS server, the IP given to them is the IP of another copy server. This is done without ever changing the DNS domain mapping, otherwise there will be problems with caching.

Every time there is a link to a picture or a video or something like that in the HTML file in the CDN, the link it's akamaized, this means that they add `[akamai.com](http://akamai.com)` before the link. (www.cnn.com → akamai.com/www/cnn/com)

The Akamai DNS server, it can see your IP and estimate the location, and so give the IP of one of the nearest Akamai server that contains the content. Akamai copy the content from CNN to their servers.

Akamai is a type of Content Delivery Network (CDN).

### Availability and Consistency trade-off

There is always a trade-off between availability and consistency.

- Availability: the service is always available;
- Consistency: the content is always the most updated.

The choice between the two heavily depends on the application. For banking applications, consistency is more important. For media applications like news, availability is more important, since a news that's not the most updated is not a problem.

# Other content

## Pump and dump fraud

Pump and dump is a market manipulation organized by a group of individuals in order to rise the price of something to trick people into buying it, and then selling it to restore it to its original price and make a profit.

This frauds happens multiple times every day with uncommon crypto coins. It’s possible to detect a pump and dump scheme when the price of a coin goes up and then goes down very quickly.

## Privacy on the Internet

## GPDR

GPDR is an european regulation that aims to protect privacy and data protection. A website can take your data and use if for other reasons such as marketing only if it has your consent.

The article 15 of the law says that the users have the right to request to websites a copy of all the personal data that they have about them.
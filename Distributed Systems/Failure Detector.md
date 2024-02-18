---
Exam:
  - Distributed Systems
---
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
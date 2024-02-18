---
Exam:
  - Distributed Systems
---
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
### 2-Phase Commit Recovery

If a process crashes, it should be able to reboot and recover its state after a certain interval of time in order to complete the transaction anyway. This could be achieved by logging.

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

---
Exam:
  - Distributed Systems
---
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
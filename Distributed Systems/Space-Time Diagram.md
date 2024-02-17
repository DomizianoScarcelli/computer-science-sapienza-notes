---
Exam:
  - Distributed Systems
---
During the processes, events occur, and we model these events with the space-time diagram.

![Untitled](assets/Untitled.png)

### Some questions

**Question**: Does $e_1^1$ happen before $e_2^1$? It cannot be said, because the question has no meaning. The order depends on the run. 

**Question**: Does $e_1^1$ happen before $e_1^2$? Yes, since these two events happen in the same process, so there is an order. That’s because $e_1^1$ can influence the following events.

**Question**: Does $e_1^3$ happen before $e_2^2$? Yes because since $e_1^3$ sends a message to $e_2^2$, the second process depends on the first one and since it has to happen after.  
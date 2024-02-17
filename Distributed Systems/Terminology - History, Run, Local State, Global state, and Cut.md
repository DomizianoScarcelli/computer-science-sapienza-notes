---
Exam:
  - Distributed Systems
---
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
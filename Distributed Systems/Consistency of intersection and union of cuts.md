---
Exam:
  - Distributed Systems
---
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

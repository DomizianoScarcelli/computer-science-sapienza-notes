First some notation:
- $id(p_i)$: returns the real identity of the probe $p_i$ or the template $g_x$ in the gallery.
- $topMatch(p_j, identity)$: returns the best match between $p_j$ and the possibly more than one templates associated to the claimed identity in the gallery.
- $s(t_1, t_2)$: returns the similarity between two templates.

---

- **False Acceptance Rate** (FAR): defines how many impostors access the system, out of all the impostors attempts to access the system.
It’s better defined as $\frac{\text{Num of probes with non genuine identity and similarity above t}}{\text{Number of non genuine attempts}}$:

$$
FAR(t) = \frac{|\{p_j: s_{xj}\geq t \land id(g_x) \neq id(p_j) \}|}{|\{p_j:id(g_x) \neq id(p_j)\}|}
$$

- **False Rejection Rate** (FRR): defines how many genuine users cannot access the system because they’re rejected, out of all the genuine users attempts  to access the systems.
It’s better defined as $\frac{\text{Num of probes with genuine identity and similarity below t}}{\text{Number of genuine attempts}}$

$$
FRR(t) = \frac{|\{p_j: s_{xj}\leq t \land id(g_x) = id(p_j) \}|}{|\{p_j:id(g_x) = id(p_j)\}|}
$$

If we want to use Machine Learning terms, we can define $FRR = \frac{FN}{TP + FN}$ and $FAR = \frac{FP}{FP+TN}$. We can see how they’re very different from other ML performance evaluation measures such precision an recall, since these last two are based on correct results, and FRR and FAR are based on errors (that’s the thing to minimize more in biometric systems). 

**N.B.** Impostors can come from $P_G \cap P_N$ but genuine users can only come from $P_G$. 
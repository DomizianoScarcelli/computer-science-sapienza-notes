---
Exam:
  - Deep Learning
  - Advanced Machine Learning
---
Given two distributions $p$ and $q$, we can measure how their dissimilarity in terms of their entropy with the Kullback-Leibler divergence, defined as:

$$
\begin{align*}
KL(p\|q) \approx H(q) - H(p) \\
= - \sum_\boldsymbol{x}q(\boldsymbol{x})\log q(\boldsymbol{x}) + \sum_\boldsymbol{x}p(\boldsymbol{x})\log p(\boldsymbol{x})
\end{align*}
$$

Since this difference of entropies can return a negative distance, the authors of the measure decided to substitute $q$ with $p$ in the first part, and so the final formula is:

$$
\begin{align*}
KL(p\|q) = - \sum_\boldsymbol{x}p(\boldsymbol{x})\log q(\boldsymbol{x}) + \sum_\boldsymbol{x}p(\boldsymbol{x})\log p(\boldsymbol{x}) \\
= -\sum_\boldsymbol{x}p(\boldsymbol{x})\log\frac{q(\boldsymbol{x})}{p(\boldsymbol{x})}\ge 0
\end{align*}
$$

Which makes the divergence not symmetric. 
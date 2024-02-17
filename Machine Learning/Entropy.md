---
Exam:
  - Deep Learning
---
The information carried by an event $\boldsymbol{x}$ can be quantified as:

$$
I(\boldsymbol{x}) = -\log p(\boldsymbol{x})
$$

This means that the less the event is likely to happen (low $p(\mathbb{x})$) the higher the information it carries (high $\log p(\mathbb{x})$). In fact if $p(\mathbb{x})$ is high, its $\log$ will be near $0$, since a very probable event doesn’t carry much information.

Given a probability distribution $p$ on some set of events $\mathbb{x}$, we define its entropy as the probability-weighted average of information:

$$
H(p)= -\sum_\boldsymbol{x}p(\boldsymbol{x})\log p(\boldsymbol{x})
$$

## 
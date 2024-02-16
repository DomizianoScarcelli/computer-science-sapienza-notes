---
Exam:
  - Biometric Systems
---
In order to define these distributions, we have to define the two hypothesis:

- $H_0$: the person is a different person as the claimed identity;
- $H_1$: the person is the same person as the claimed identity.

The impostor distribution describes the probability of a similar value $s$ given that the hypothesis $H_0$ is true.

The impostor distribution is the same as the FAR distribution, and it’s given by the probability of having a decision $D_1$ in the presence of an hypothesis $H_0$ that’s true. 

$$
FAR = P(D_1|H_0)
$$

On the other hand, the client score distribution (genuine distribution) is described as the FRR distribution, given by the probability of having a decision $D_0$ in the presence of an hypothesis $H_1$ that’s true.

$$
FRR = P(D_0|H_1)
$$

Both the distributions are normal distributions, meaning that most of the genuine and impostor acceptance will concentrate on two different values.

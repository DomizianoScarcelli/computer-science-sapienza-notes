---
Exam:
  - Biometric Systems
---
**In the closed set identification** we don’t have a threshold at all, since we know that all the probe belong to an subject in the gallery. The only mistake the system can do is identify the wrong person.

In order to quantify the performance of the system in this type of error, we define:

- $CMS(k)$  - Cumulative Match Score at rank $k$: the probability of correct identification at rank $k$, meaning the probability of finding the sample associated with the correct identity in the top $k$ similarity scores. Formally (*don’t know if this formula is actually correct btw*):

$$
CMS(k) = \frac{|{P_j:rank(p_j)\le k, id(p_i) = id(p_j)} \forall p_j \in P|}{|P|}
$$

- $CMC$ - Cumulative Match Characteristic curve: the curve obtained by calculating the $CMS(k)$ for every $k$. In closed sets, $k$ is equal to the number of subjects in the gallery.

We can calculate the AUC for the CMS, but this heavily depends on the maximum $k$ value, so it’s necessary to divide the AUC by the maximum $k$ in order to get a normalized unit, otherwise it would only make sense to compare the AUCs of systems with similar maximum values of $k$. 

In general the steepest the CMC, the better the system.

$CMS(1)$ is also called Recognition Rate, since it’s the probability of having the sample associated with the correct identity at the top position in the similarity score.
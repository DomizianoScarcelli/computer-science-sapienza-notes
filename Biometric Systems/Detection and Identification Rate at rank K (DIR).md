---
Exam:
  - Biometric Systems
---
### Rank
The rank of a certain sample or templatate is its position in the list of the matched templates in the gallery.

## Detection and Identification Rate at rank K (DIR)
We are in the case of identification open set. 

$DIR$  at rank $k$ measures the probability of correct identification at rank $k$, meaning that the correct subject is returned at position $k$ in the list of the matched templates in the gallery.

Formally:

$$
DIR(t,k) = \frac{|\{P_j: rank(p_j) \le k, s_{ij}\ge t, id(g_i) = id(p_j)\}|\forall p_j \in P_G}{|P_G|} 
$$

Note that $FRR(t) = 1-DIR(t,1)$.

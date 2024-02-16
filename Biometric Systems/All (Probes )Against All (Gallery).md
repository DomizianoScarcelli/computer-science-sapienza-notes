---
Exam:
  - Biometric Systems
---
The only time probes and sample can overlap is when we make a “all against all” comparison.

There are a few types of all against all, that depends on the type of recognition (Verification, Identification closed set or open set). One example is to compare all probes against all the gallery. 

In all against all, we want to experiment the most cases possible, for example in verification we want to choose different claims for each probe, different thresholds and different partition between probes and gallery (in case we’re comparing all probes against all gallery).

For every experiment, we calculate the FAR and FRR. Then we variate the threshold, and we calculate the others FAR and FRR and then we take the average. When we change partition, we re-calculate the FAR and FRR average and we can take the overall average at the end when we tried all possible cases.

The matrix that describes the comparison between probes and gallery can be computed just one since the distances (or similarities) are always the same (because we have the ground truth in the dataset).

Once we’ve computed the matrix, we can vary the claims and threshold to see how the evaluation changes.

Of course, when we partition the probe and gallery set in a different way, the distance matrix will change.

### Verification

When we’re talking about verification, there are three variables in the evaluation process: the probe and gallery set partition, the claim and the threshold.

When we do an experiment, we choose a value for each of these variables, and we calculate the FAR and FRR in the following way:

- If a probe P1 belongs to identity A and claims the identity B (it’s an impostor) and the top match is B, we have a False Acceptance, otherwise we have a Genuine Rejection.
- If a probe P2 belongs to identity C and claims the identity C (it’s a genuine user) and the top match ic C, we have a Genuine Acceptance, otherwise we have a False Rejection;
- If a probe P3 belongs to identity D and it’s not enrolled in the system, whatever identity it would claim, it would always be an impostor.

As we have seen, in a single operation the comparison takes place only between the claimed identity and the template in the gallery that belongs to the claimed identity. The real identity is only used to know if the user is genuine or an impostor.

Based on the number of impostors, and the number of FA, GA, FR, GR we have computed, we can calculate the FAR and FRR for this round.

We repeat the process with as many combinations as possible, and then we take the FAR and FRR average.

We can also have multiple templates of the same identity inside the gallery set, in order to be more generalized. This scenario decreases the FRR, because we have more possibilities to recognize a genuine identity, but it increases FAR, since it’s more possible for an impostor to look like a genuine user.

### Identification Open Set

The method is similar to the one seen for verification, but in this case we don’t have a claim. The variables in this case is the partition between probe and gallery and the different thresholds. 

We can calculate the FAR and FRR as following:

- If a probe P1 belongs to identity $A$ and is in the gallery (it’s a genuine user), we compute the ordered list of distances for P1. Let’s say it’s $[d(A1), d(C1), d(D1), d(B1)]$. As we can see, the first element refers to the correct identity, so we have a Genuine Acceptance (Detection and Identification at rank 1 $DI(t, 1)$).
In case we had a list like $[d(C1),d(A1),d(D1), d(B1)]$ we'd have a False Rejection, since the first element doesn’t refer to the correct identity. If the correct identity distance is below the threshold and it's at the second place, it would contribute to the count of $DI(t, 2)$. (This would not happen if the distance is greater than the threshold).
- If a probe P2 belongs to identity B and it’s not in the gallery it's an impostor. We compute the ordered list and if the top match is B, we have a False Acceptance, otherwise if there isn’t any distance below the threshold, we have a Genuine Rejection.

Remember that the ordered list of distances doesn’t change according to the threshold, we can only observe which distances are above and below the threshold.

As before, we can have multiple templates referring to the same identity inside the gallery set.

### Identification Closed Set

This is the easies scenario, becasue there cannot be impostors, since we make the assumption that all the probe belongs to some identity that’s enrolled in the system.

We don’t have a threshold, but the only variable is the partition between probes and gallery set.

Everytime we have a Genuine Acceptance at rank $k$, meaning the template belonging to the correct identity is in position $k$ in the list, we increment the Cumulative Match Score at rank $k$. (Recognition Rate in case $k=1$).

Also here we can have multiple templates for each identity in the gallery. In general, using all the templates, gives a finer evaluation, but using just one template for identity is more than acceptable.
## All against all probe vs gallery different sessions

In case we have samples from different session, we can do the following:

- If the sessions are just two, we can use an entire session as our gallery and the other as probe.
- If the session are more than two, we can use a subset of sessions as gallery and the remaining sessions as probe.

We can calculate the distance matrix in advance, and compare all the probes templates with the gallery templates. This time, there cannot be a template that’s both in the probe set and in the gallery set.

We can also try to see what happens if we swap the gallery and the probe, meaning we do the evaluation all over swapping the templates that were in the gallery set with the one that were in the probe set.

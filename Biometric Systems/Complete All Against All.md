---
Exam:
  - Biometric Systems
---
As we’ve seen [[All (Probes )Against All (Gallery)|in the previous case]], we would compute the distance matrix every time we take a different partition of probe and gallery set.

That’s not necessary all the time, since we can compute the distance matrix for every possible partition.

This kind of matrix will be of dimension $G\text{x}G$ where $G$ is the cardinality of the gallery, that in this case is the total number of samples. We also define $N$ as the number of subjects and $S$ the number of templates per subject. We can calculate $|G| = S \cdot N$.

In this case, we don’t have a division in probes and gallery, since each template plays in turn the role of either probe or gallery. We don’t consider the main diagonal of the matrix because we would compare a template with itself.

Every probe is consider either as genuine or as an impostor, so a probe will play once the role of genuine user, and all the other times the role of an impostor. (We we'll have many more impostors attempts than genuine attempts in the evaluation).

Each row can represent more than just one experiment (not as before).

**Pros**:

- It’s easy to program, since we compute the overall distance matrix and then make different experiments with different values for the threshold;
- Since there are more impostors attempts then genuine ones, it’s possible to over-stress the system.

**Cons**:

- The time to compute the full distance matrix can be very high if the dataset is large,
- It’s not a good evaluation technique if the dataset has been acquired during different sessions, this because the samples captured in the same sessions are usually more similar then those from different sessions, due to small variations happening with time and environmental condition such as light and sensor performance.

As before, we now see how the technique can be applied to all the scenarios.

We define the function $label(i)$ as the associated identity with the sample in row or column $i$. 

### Verification single-template

We can calculate:

- **Number of operations per row**: $|G| -1$, since the probe is compared to each template but itself. Each time it declares a different identity.
- **Number of genuine attempts per row**: $S-1$, since it’s compared to all the templates with the same identity ($S$) minus itself.
- **Number of impostor attemps per row**: $(N-1)S$, since it’s compared to all the templates of the other identities. $S$ templates per identity, $N-1$ identities because the matching identity is genuine.
- **Total genuine attempts**: $TG = |G| \cdot (S-1)$, since there are $S-1$ genuine attempts for each row.
- **Total impostor attempts**: $TI = |G| \cdot (N-1)S$, since there are $(N-1)S$ impostor attempts for each row.

```
for each threshold t
	for each cell M[i,j] with i != j
		if M[i,j] <= t then
			if label(i) == label(j) then GA++
			else FA++
		else if label(i) == label(j) then FR++
		else GR ++
	GAR(t) = GA/TG
	FAR(t) = FA/TI
	FRR(t) = FR/TG
	GRR(t) = GR/TI
```

### Verification multiple-templates

We use the same distance matrix, but we’re now comparing each probe template not with all other templates, with groups of templates, meaning that for all the templates for a certain identity, we’ll only take the identity with the best result.

As before, we can calculate:

- Number of operations per row: $N$, since the probe is compared with the group of templates for each identity, and the total number of identities in the gallery is $N$.
- Number of genuine attempts per row: $1$, since only $1$ is the matching identity
- Number of impostor attempts per row: $N-1$, since the other $N-1$ are the different identities in the gallery.
- Total genuine attempts: $|G| \cdot 1$
- Total impostor attempts:  $|G|\cdot(N-1)$

```
for each threshold t
	for each row i
		for each group M_label of cells M[i,j] with same label(j) excluding M[i,i]
			diff = min(M_label)
			if diff <= t then
				if label(i) = label(M_label) then GA++
				else FA++
			else if label(i) = label(M_label) then FR++
			else GR++
	GAR(t) = GA/TG
	FAR(t) = FA/TI
	FRR(t) = FR/TG
	GRR(t) = GR/TI
```

### Identification open set

Considering the templates one by one as for verification single template, the pseudocode would be too complicated, so we only take in consideration the multiple-template variation of identification.

We can calculate:

- Number of operations per row: $2$, since a probe can be enrolled or not.
- Number of genuine attempts per row: $1$, the subject is in the gallery.
- Number of impostor attempts per row: $1$, the subject is not in the gallery.
- Total genuine attempts: $|G|$;
- Total impostor attempts: $|G|$.

```
for each threshold t
	for each row i
		{L[i,m] | m = 1,...,|G|-1} = {M[i,j] | j = 1,...,|G|} - M[i,i] ordered by increasing value
		if L[i,j] <= t then
			if label(i) == label(L[i,1]) then DI(t,1)++
			find the first L[i,k] such that label(i) != label(L[i,k]) and L[i,k] <= t
			if such k exists then FA++
			else: 
				find the first L[i,k] such that label(i) == label(L[i,k]) and L[i,k] <= t
				if such k exists then DI(t,k)++
				else: FA++
		else: GR++
	DIR(t,1) = DI/TG
	FRR(t) = 1 - DIR(t,1)
	FAR(t) = FA/TI
	GRR(t) = GR/TI
	
	k = 2
	while DI(t,k) != 0:
		DIR(t,k) = DI(t,k)/TG + DIR(t, k-1)
```

### Identification closed set

In identification open set there is no threshold and there are no impostors, since every probe belongs to an identity that’s enrolled in the system.

We can calculate:

- Numer of operations per row: $1$, since only the first position on the list is considered;
- Number of genuine attempts per row: $1$
- Number of impostor attempts per row: $0$
- Total number of genuine attempts: $|G|$
- Total number of impostor attempts: $0$

```
for each row i
	{L[i,m] | m = 1,...,|G|-1} = {M[i,j] | j = 1,...,|G|} - M[i,i] ordered by increasing value
	find the first L[i,k] such that label(i) != label(L[i,k])
	CMS(k) ++
	CMS(1) = CMS(1) / TA
	RR = CMS(1)
	
	k = 2
	while k < |G| -1:
		CMS(k) = CMS(k)/TA + CMS(k-1)

```

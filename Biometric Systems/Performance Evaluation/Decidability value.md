The decidability value is useful to know how much a certain individual can be recognized using a certain algorithm. A low decidability means that, no matter the precision of the algorithm, the user will always have a low match with themselves. 

Decidability Value is calculated as $\frac{avg(D^I) - avg(D^E)}{\sigma}$ where $avg(D^I)$ is the intra-class dissimilarity value average and $avg(D^E)$ is the inter-class dissimilarity value average and $\sigma$ is the standard deviation in such two sets which purpose is to have a normalized value.

The dissimilarity value is the distance value of the chosen template with the compared template.

This value can vary a lot depending on the users we have in the system, and this means that, no matter the algorithm that are used, the measures seen so far are not enough to give a complete evaluation of the system. 

> [!Note]
> SEE TORRALBA QUOTE AND SEMIMETRIC OF DISTANCE MATRIX
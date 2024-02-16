---
Exam:
  - Biometric Systems
---
To solve the problems of PIE variations in PCA, we can use Linear Discriminant Analysis, that’s a particular case of the generalized Fisher’s linear discriminant (FLD). This technique allows to build fisherfaces that are more robust in case of PIE variations.

In this case, LDA perform a linear transformation (just like PCA) but with the objective to separate in the best way possible the classes in the reduced dimensions space.

The idea is to consider the mean vector $\mu_i^j$ for each class $i$ and each dimension $j$. An idea would be to choose the axis that maximise the distance between the projected means, but this isn’t a good measure since it doesn’t take care of the standard deviation within classes.

What we can do is maximise the ration of between-class variance to within-class variance. 

> [!TODO]
> Inclomplete!

## Difference from PCA and LDA

The main difference from [[PCA - Principal Component Analysis |PCA]] is that LDA is a supervised method.

Supervised in this contest means that while in PCA we are not interested in the real identity of the training subjects, but all the training images are collected togheter in the same training set; in LDA we label the samples for each subject that participates in the training set.
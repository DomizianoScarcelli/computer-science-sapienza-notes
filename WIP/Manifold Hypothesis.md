---
Exam:
  - Deep Learning
---
## The manifold hypothesis (just an intuition…)

Deep learning makes a big assumption, which is that the input data lives on an underlying non-Euclidean structured called a manifold.

In this manifold there are subspaces where the same type of objects exists. For example in a certain subspace there may be only photos of mountains.

In the [[Autoencoders|autoencoder]] architecture, the decoder performs a mapping from a low-dimensional latent space $\mathbb{R}^k$ to an high-dimensional embedding space $\mathbb{R}^d$ of observed data.

The latent space is Euclidean, while the embedding space is curved (not Euclidean).
## Manifolds
> [!TODO]
> This has to be REVIEWED

A manifold can be seen as a union of charts (atlas).

A chart is a mapping $\phi : \mathbb{R}^k \to \mathcal{S} \subset \mathbb{R}^d$ with $k < d$.

An example of a chart is the mapping that happen when we want to represent the earth on a flat surface.

- The domain of $\phi$ (the space in which the flat surface is) is the parametric space (Euclidean);
- The codomain of $\phi$ (the sphere that represents the earth) is the embedding (not Euclidean).

$\phi$ has to be:

- **Smooth**: if two points are close in the parametric space, then they have to be close also in the embedding. The distance may be different, but the proximity has to be maintained.
Being smooth means to be **continuous** and **differentiable**.
- **Invertible**

A function that is smooth and invertible takes the name of ***diffeomorphism.***

For each manifold, we have infinitely many ways to construct a chart.

Back to the cartography example, we can represent the earth as a map that better maintains the distances, or maybe the areas or the angles. Each time we will have a different chart, but they encode the same exact geometric information.

## Relationship between Manifolds, Autoencoders and PCA

The decoder $D: \mathbb{R}^k \to \mathbb{R}^d$ is a chart that maps the *latent space* spanned by the codes $\mathbb{z}$ to the *data space* of the inputs $\mathbb{x}$.

It’s both differentiable and continuous (smooth) and it’s invertible via the encoder $E$, so it’s in all and for all a chart.

<aside>
💡 Being linear, PCA puts the data on a flat manifold, since the decoder (reconstruction) simply performs a linear combination of the orthogonal vectors.

</aside>

Finding the map $\phi$ is achieved by training an autoencoder.
---
Exam:
  - Deep Learning
---
## Features

We assume that each data point $x$ is the result of a process $\sigma$ that takes in input a set of features $F$ (feature space) and composes them to form the data point $x$.

$$
\sigma:F \to x
$$

Both $\sigma$ and $F$ are unknown.

### Example of $\sigma$ for image representation

![Screenshot 2023-03-01 at 6.38.46 PM.png](Screenshot_2023-03-01_at_6.38.46_PM.jpeg)

In this case the image is the data point, and each pixel $x$ is a feature. The $\sigma$ function just scales each pixel by a certain factor (all the pixels here have the same value) and then sums everything up to obtain the final image.

The representation in this case is very inefficient, since the image has as many dimensions as pixels. Ideally we want the features to depend only on the semantic of the image, and not on the number of pixels.

In this case $F$ is a vector space, and $\sigma$ is linear. Generally, the transformation $\sigma$ gets in input much less features and non-linearly transforms them in order to obtain the image.

Features are *task-driven*, meaning that a certain representation may make sense only if it makes sense in that particular task.
For example it’s useless to represent a certain card with the rank and the color if the rank it’s not important for the task.

### Embeddings

The output of $\sigma$  is called an embedding of the data point. In general, multiple embeddings are possible for each data point.

**Example:**

A sheet can be embedded as a 2D sheet, and so it will live in $\mathbb{R}^2$, but it may be represented with other 3D shapes, and will live in $\mathbb{R}^3$.

![Screenshot 2023-03-01 at 6.05.07 PM.png](Screenshot_2023-03-01_at_6.05.07_PM.jpeg)

In this case three different embeddings are representing the same intrinsic object. In this particular case, it’s possible to prove that the intrisic object underneath the embedding is the same because it mantains some intrinsic properties, for example the distance between each pair of points. This property is called isometry.

The challenge here is to discover which are the intrisic properties that are preserved, since those are the properties that characterize the data.

Most of the time we have only access to the embedding, and not the intrinsic object (for example a photo of a dog can be an embedding, but the instrinsic idea of a dog is not so clear).

### Latent Features

Features are not always localized in space, nor evident in the embedding. These type of features are called latent features. 

An exemple can be the directional illumination on a certain object, that can be expressed with only 4 parameters (3 for the coordinates and 1 for the intensity).
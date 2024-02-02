## PCA - Principal Component Analysis

The curse of dimensionality is solved in the feature space with dimensionality reduction methods, such as Principal Component Analysis (PCA).

What PCA does is to transform the data by creating a new space in which the axis are the $n$ principal components of the data, where $n$ is the number of dimensions.

These principal components are the eigenvectors with the highest eigenvalues, this models the direction where the data variance is higher. The first PC is the one with the highest eigenvalue, the second is the one just under that and so on. A PC is just a linear combination of all the features.

We can compute all the principal component and by the definition of eigenvectors, every $PC_n$ will be orthogonal to all the other ones before that. As said, the maximum number of PC is the maximum number of dimentions the data is described in.

To perform dimensionality reduction, it’s possible to remove some of the last principal components, since they are the axis that carries the least amount of information. A general idea is to keep the first $k$ principal components, where their cumulative proportion of variance, meaning the variance they express in relationship with the total variance, is 99%.

We then can project the data onto the new $k$-dimensional space, by representing the data with new axis and by maintaining most of the information.

So, in general, PCA is not by itselfe a dimentionality reduction method, but a data transformation method. But since the new space is constructed by principal components that are ordered by the level of variance, it’s possible to delete some of the last one to reduce the number of features

### PCA in face recognition

When used in face recognition, principal components gets the name of *eigenfaces*. Now let’s see in more details how this is used in order to perform face recognition.

We define the traning vector as the vector of dimensions $1 \text{ x } n$ that is obtained stretching the images from the trainig set all in one column.

We can form the matrix of training vectors of dimensions $m \text{ x } n$ where $m$ is the number of images in the training set.

We can create the Mean Vector $\bar{x}$ starting from the matrix of training vector by just averaging the value of all the rows. The mean vector will be of dimensions $1 \text{ x } n$.

$$
\bar{x} = \frac{1}{m}\sum_{i=1}^mx_i
$$

The mean vector can be represented as an image, and can represent the face that has the most common traits among the all traning set faces.

We can compute the covariance matrix:

$$
C = \frac{1}{m}\sum_{i=1}^m(x_i-\bar{x})(x_i-\bar{x})^T
$$

The covariance matrix $C$ has dimension $n \text{ x } n$, and so each column can be represented as an image itself.

What we want now is to reduce the dimensionality from $n$ to $k$, where $k$ is the smallest possible number of dimensions that preseve most of the information.

Once we have $C$, we proceed to get the its eigenvectors, which will be our eigenfaces. In order to find an eigenvector $v$, we have to find the eigenvalues $\lambda$ such that $Cv = \lambda v$. We can see that the equation can be rewritten as $|C - \lambda I| = 0$ where $I$ is the identity matrix.

Once we have the eigenvalues $\lambda_1, \lambda_2...$, we put it in the original equation and find the eigenvectors. [Source](https://www.mathsisfun.com/algebra/eigenvalue.html)

In order to obtain a $k$-dimension subspace, we order the $k$ eigenvectors that correspond to the highest $k$ values of the matrix. The projection matrix $\phi_k$ is built using the $k$ eigenvectors as columns, and has dimensions $k \text{ x }n$.

The projection of a vector $x$ onto the new $k$-dimension sub-space is defined as following:

$$

\text{Proj}(x) = \phi_k^T(x-\bar{x}) \text{ where } \text{Proj}: \Re^n \to \Re^k

$$

And represent the new feature vector for the image.

The basic idea of PCA for face recognition is that, instead of comparing faces pixels by pixel, which is a technique that gives unreliable results, we can compare images onto the new $k$-dimensional subspace. We can just compare the projetion coefficients $\text{Proj}(x_i)$ corresponding to each image $i$.

The most similar face will have the $\text{Proj}(x')$ and calculate the distance between every other feature vector for the images in the gallery. The face more similar will be the least distant to $\text{Proj}(x')$.

### PCA problems

The main problem of PCA is that it very sensitive to intra-class variations. Meaning that if there are multiple faces of the same subject in the gallery, maybe in different poses (PIE variations), it will be less precise, meaning it may be not able to recognize the same invidivual under different conditions, and lead to false rejections.  
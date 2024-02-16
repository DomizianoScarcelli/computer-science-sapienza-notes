---
Exam:
  - Deep Learning
---
## Matrices

> Linear algebra is about matrices as much as astronomy is about telescopes.

Consider a linear map $T: V \to W$ and two basis, one $v_1\dots,v_n \in V$ and another $w_1,\dots,w_n \in W$:

The matrix of $T$ in these bases is the $m \times n$ array of values in $\mathbb{R}$

 

$$
T = \begin{pmatrix}
T_{1,1} && \dots && T_{1,n} \\
\vdots && \ddots && \vdots \\
T_{m,1} && \dots && T_{m,n} \\
\end{pmatrix}
$$

Where each column contains the linear combination coefficients that describes how the basis vectors are mapped from one vector space to another.

In fact, the $T_{i,j}$ entries are defined by:

$$
Tv_j = T_{1,j}w_1+\dots+T_{m,j}w_m
$$

Matrices are just a representation the linear maps, which depends on the basis that are chosen. Whenever we have to do operation between matrices, the bases have to be the same, otherwise we’re dealing with coefficient that represent different things.

### Matrix of a vector

Just how matrices represent how the basis vectors are mapped from a vector space to another, the matrix of a vector (that has size $n \times 1$ where $n$ is the length of the vector) describes the vector in terms of coefficient of the basis vectors (so it describes how the basis vectors has to be stretched in order to obtain that particular vector).

Once again, the matrix depends on the choice of the basis for that particular vector space where the vector is.
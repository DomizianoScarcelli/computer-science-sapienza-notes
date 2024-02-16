---
Exam:
  - Deep Learning
---
A linear map from $V$ to $W$ is a function $T:V \to W$ with the properties of:

Given any vectors $\mathbb{u}$ and $\mathbb{v}$

A linear map is a function $T$ that satisfies the following properties for any vectors $\mathbb{u}$ and $\mathbb{v}$ in a vector space $\mathbb{V}$ and any scalar $\lambda$:

- Additivity: $T(\mathbb{u}+\mathbb{v}) = T\mathbb{u} + T\mathbb{v}$
- Homogeneity: $T(\lambda\mathbb{v}) = \lambda(T\mathbb{v})$

In other words, a linear map preserves vector addition and scalar multiplication. Additionally, the composition of two linear maps is also a linear map, and the identity function is a linear map.

A linear map can be represented by a matrix in a specific basis, and the matrix of a linear map can be used to transform vectors from one basis to another.

Examples of linear maps are:

- The identity function $I:V \to V$ defined as $Iv = v$
- The differentiation operation $D: F(\mathbb{R})\to F(\mathbb{R})$ defined as $Df = f'$
- The integration operation $T: F(\mathbb{R}) \to \mathbb{R}$ defined as $Tf = \int_0^1f(x)dx$
- A map $T: \mathbb{R}^n \to \mathbb{R}^m$ defined as $T(x_1,\dots,x_n) = (A_{1,1}x_1 + \dots+A_{1,n}x_n,\dots,A_{m,1}x_1 + \dots + A_{m,n}x_n)$

**Example - The equation of a line**

The general equation of a line

$$
y = ax+b
$$

Is not a linear map since it doesn’t have the homogeneity property:

$$
f(\lambda x) \neq \lambda(f(x))
$$

Because of the $b$ term, that in machine learning lingo is called *bias*.

**Another example**

Other equations may not be a linear map with respect to certain variables, but they can with respect to others.

For example the equation $y = z\sin(x)+z^2\sin(x)$ is not a linear map w.r.t. $z$ or $x$, but it is w.r.t. $\sin(x)$.

---

Linear maps form a vector space with addition and multiplication defined trivially. We also have the definition of product between linear maps.

Let $T:U \to V$ and $s: V \to W$ be two linear maps, their product $ST: U \to W$ is defined as:

$$
(ST)(u) = S(Tu)
$$

Keep in mind that composition of linear maps is not commutative: $ST \neq TS$.

Since linear maps for a vector space, they have also associativity, identity and distributive properties.
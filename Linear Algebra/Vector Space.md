---
Exam:
  - Deep Learning
---
A vector space $V$ is a set along with addition and scalar multiplication operations, such that it satisfies:

- Commutativity:
- Associativity:
- Additive identity:
- Additive inverse:
- Multiplicative identity:
- Distributive properties:

In a few words, a set of generic objects (that can be numbers, functions or other things) is a vector space if, after applying the operations, the result is always in that vector space.

### **Example of vector space - Real number sequences**

An example of vector space is the set of $n$-long sequences of numbers in $\mathbb{R}$:

$$
\mathbb{R}^n=\{(x_1,\dots,x_n) :x_j\in\mathbb{R} \quad \text{for }j=1,2,\dots,n\}
$$

Along with the addition and multiplication operations, defined as expected.

### **Another example of vector space - Functions**

Another example of a vector space is the set of all functions

$$
f:[0,1] \to \mathbb{R}
$$

with the standard definition for sum and scalar product:

$$
(f+g)(x) = f(x) + g(x) \\
(\lambda f)(x) = \lambda f(x)
$$

With additive identity and inverse defined as:

$$
0(x) = 0\\
(-f)(x) = -f(x)
$$

---

Each element inside of a vector space is a vector.

Curved surface are not a vector space, since summing two coordinates doesn’t assure us that the new coordinate will lay on the surface. (2D surfaces are a vector space).

For this reason, curved surfaces (such as the manifold) cannot be studied with linear algebra, but they need differential geometry.

We can still use linear algebra to study the functions that can be applied on surfaces, since as we’ve seen the set of all functions is a vector space.

N.B.: The domain doesn’t have to be $[0,1]$, but can be a generic finite set $A$.

## Bases

A basis of a vector space $V$ is the minimal collection of vectors in $V$ that are linearly independent from each other and spans $V$.

In other terms, it’s the minimal set of vectors that generates the entire space.

<aside>
💡 The **span** of a list of vectors is the set of their all possible linear combinations, and it’s denoted as $\text{span}(v_1,\dots,v_n)$.

</aside>

The basis vectors $v_i \in V$ are linearly independent if and only if each $v\in \text{span}(v_i,\dots,v_n)$ has only one representation as a combination of $v_i,\dots,v_n$ (hence **minmal collection**).

This means that the number of vectors in the basis is the same as the dimensionality of the vector space.

Every vector $v \in V$ can be expressed uniquely as a linear combination of the basis vectors:

$$
v = \sum_{i=1}^n\alpha_iv_i
$$

The standard basis of $\mathbb{R}^n$ is the collection of one-hot vectors (or indicator vectors): $\{(1,0,\dots,0), (0,1,0,\dots,0),\dots,(0,\dots,0,1)\}$.
### More about dimensions

Linear algebra can only be used to study vector space with finite dimensions. If the vector space is infinitely dimensional (for example the set of all functions that map real numbers to other real numbers) than we need functional analysis. 

In the case of the vector space made of functions, for it to be finite dimensional, the domain has to be finite.

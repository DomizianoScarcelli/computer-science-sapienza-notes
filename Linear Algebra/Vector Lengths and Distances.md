---
Exam:
  - Deep Learning
---
### Euclidean distance

The Euclidean distance measures the length of a straight line connecting two points.

Pythagoras’ theorems says:

$$
d(a,b) = (|x_b - x_a|^ 2 + |y_b-y_a|^2) ^ \frac{1}{2}
$$

In matrix notation we can write the same thing:

$$
d(\mathbb{a}, \mathbb{b}) = \|\mathbb{a} - \mathbb{b}\|_2
$$

The Euclidean distance can also be called the $L_2$-Norm.

The norm (or length) of a vector is simply its distance from the origin:

$$
\|\mathbb{x} - \mathbb{0}\|_2 = \|\mathbb{x}\|_2 = \sqrt{\sum_{i=1}^k|x_i|^2} = \sqrt{\mathbb{x}^T\cdot\mathbb{x}}
$$

### $L_p$ distance

The $L_p$ distance is a generalization with differnt $p$ coefficient of the Euclidean distance.

$$
\|\mathbb{x} - \mathbb{y}\|_p=  \left( \sum_{i=1}^d(x_i-y_i)^p \right) ^{1 \over p}
$$

![$L_p$ distance in $R^2$ with different values for $p$.](Screenshot_2023-03-15_at_5.09.48_PM.png)

$L_p$ distance in $R^2$ with different values for $p$.

>[!Note]
Note that the number of dimensions $k$ for points in $\mathbb{R}^k$ and the $p$ coefficient are two different things.

---
Exam:
  - Deep Learning
---
The problem of fitting a polynomial curve to the data is called polynomial regression, or better “linear regression with polynomial features”, since the problem is still the same of linear regression, but we have a polynomial function.

Note that the polynomial function is polynomial with respect to the data, but is still linear in the parameters.

$$
y_i = \sum_{j=1}^k a_jx^j_i + b \quad \forall i = 1, \dots, n
$$

In matrix notation we can express the function as:

$$
\underbrace{
\begin{pmatrix}
y_1 \\
y_2 \\
\vdots \\
y_n
\end{pmatrix}}_\mathbb{y}
=
\underbrace{
\begin{pmatrix}
x_1^k & x_1^{k-1} & \dots & x_1 & 1 \\
x_2^k & x_2^{k-1} & \dots & x_2 & 1 \\
\vdots & \vdots  & \vdots & \vdots  & \vdots \\
x_n^k & x_n^{k-1} & \dots & x_n & 1 
\end{pmatrix}}_\mathbb{X}
\underbrace{
\begin{pmatrix}
a_k \\
a_{k-1} \\
\vdots \\
a_1 \\
b
\end{pmatrix}}_\theta

$$

The solution is the same as the linear regression solution, with the requirements that $k < n$.

In the matrix $\mathbb{X}$ we have a row for each data point, and a column for each parameter.
### Is polynomial regression all we need?
Since we can approximate every continuous function with a polynomial, as stated by [[The Stone-Weierstrass theorem]], is polynomial regression all we need in order to fit the data?

The answer to this question is **NO**, since polynomial regression is kind of limited, and we cannot perform some useful thing with it, for example:

- If we want different loss functions than MSE;
- If we want to apply regularization;
- If we have additional priors;
- If we want to compute intermediate features;
- If we want more flexibility;
- If we want to perform classification instead of regression.
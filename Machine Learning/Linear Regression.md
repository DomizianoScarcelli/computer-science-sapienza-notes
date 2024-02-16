---
Exam:
  - Deep Learning
  - Fundamentals of Data Science
---
The most basic machine learning case is linear regression.

The model is linear plus a bias. If we include the bias then the model wouldn’t be linear in the parameters. (We don’t have homogeneity and additivity)

The function is the function of a line:

$$
f_\Theta(x_i) = y_i
$$

The $n$ pairs of data points $(x_i, y_i)$ are given. The $x_i$ are called regressors.

The goal is to find the parameters $\theta$ that when plugged into the equation give out a line of best fit.

A good choice for a loss function, in this case, is the mean squared error (MSE) between the input (that is the ground truth) and the predicted output.

$$
\epsilon = \min_{a, b \in \mathbb{R}} \frac{1}{n}\sum_{i=1}^n(y_i - f_\Theta(x_i))^2
$$

(Note that we can ignore the $1\over n$ factor since it reduces the sum by a constant, so the minimum will change but not the chosen parameters).

When $f_\Theta$ is linear, we can call the error the least-squares approximation.

We can rewrite the function as:

$$
\epsilon = \min_\Theta \ell_\Theta(\{x_i, y_i\})
$$

or more generally:

$$
\epsilon = \min_\Theta \ell(\Theta)
$$

Note that the loss is defined on the entire dataset and not only a single data point. Also, note that $f_\Theta$ is linear but $\ell_\Theta$ is quadratic.

Today there is no unified theory that allows us to do constrained learning. The constraint is on the parameters, for example, constrain them to be positive.
We will mostly deal with unconstrained problems.

Another constraint is to make the model output a probability distribution, meaning that all the possibilities in the output vector sum to 1.
## Closed form solution for Linear regression

A closed form solution means that we have a formula to solve a certain problem. Most of the times in real world’s problems this is not possible.

Starting from the MSE problem, we can set the gradient of the loss to zero and solve for the parameters in order to find a closed form solution. Remember that the loss is convex so we are guaranteed to find the global minimum.

After some calculations that can be found on the slides (Lecture 4 - 63 to 68) we find the closed form solution:

$$
\mathbb{\theta} = (\mathbb{X}^T\mathbb{X})^{-1}\mathbb{X}^T\mathbb{y}
$$

### Equivalent for more dimensions

Until now we have seen the case in which each data point is just one number, meaning is one dimensional.

In the more general case, the data points are vectors in $\mathbb{R}^d$ where $d$ is the dimensionality.

The linear regression formula can be expressed as:

$$
\mathbb{y}_i = \mathbb{A}\mathbb{x}_i + \mathbb{b}
$$

The closed form solution is:

$$
\mathbb{\Theta} = (\mathbb{X}\mathbb{X}^T)^{-1}\mathbb{X}\mathbb{Y}^T
$$

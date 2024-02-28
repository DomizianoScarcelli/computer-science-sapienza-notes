---
Exam:
  - Deep Learning
---
Let’s once again rewrite the function $g_\Theta(x)$ as:

$$
\boldsymbol{y} = f \circ \sigma(\dots)(x)
$$

In this case we assume that the $\sigma$ functions are all the same, and are all [[Activation Functions#ReLU (and its variants)|ReLU]] functions, and so the network can be also called a Deep ReLU network.

We can see that $\mathbb{y}$ is expressed as a big linear combination combination of ridge functions $\sigma(\dots)$. With ReLU we’ll have that $\mathbb{y}$ is a piecewise-linear function, meaning that the whole function would not be linear, but each single ReLU output will be linear.

For example let’s imagine a deep network that has 2-layers and for each 2D point returns a real scalar. The output of the network will be something like this:

![Output of $\mathbb{y}$. On the right there is the above view.](Screenshot_2023-03-31_at_10.12.14_AM.jpeg)

Output of $\boldsymbol{y}$. On the right there is the above view.

The blue edges are produced by the first layer, while the red ones by the second.

We can see that the function is linear in each activation region, and so is a piecewise-linear function.

Also note that the sharp edges of the output shape are due to the discontinuity of the gradient of the ReLU.

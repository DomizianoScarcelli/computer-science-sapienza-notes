---
Exam:
  - Deep Learning
---
A neural network can be thought out as a function with a complex structure and a high number of parameters $\theta$. The name *deep neural network* comes from the fact that there are many different hidden layers, that are just smaller blocks. Each of these blocks has a predefined structure, for example, a linear map (remember that a matrix is just a representation of a linear map).

When we *train* a neural network, we are just solving the function for the parameters $\theta$. We are able to do this by minimizing a function that’s called *loss*, by computing the gradients and using *backpropagation.*

Let for example $f_\Theta(x) = ax + b$ be our function, then we need to find $\Theta = \{a, b\}$.

The most basic machine learning case is [[Linear Regression]].
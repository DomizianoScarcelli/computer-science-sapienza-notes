---
Exam:
  - Deep Learning
  - Fundamentals of Data Science
---
Classification is the task of predicting a category instead of a value.

In particular, a binary classification function is of the type:

$$
f_\Theta(\mathbb{X}) = \{0,1\}
$$

A possible solution is to use linear regression and then do some post-processing, such as thresholding, in order to convert the real value to a binary label. This is not an optimal solution since the function is optimized for the MSE loss, but once the output is converted, this is not true anymore.

The idea is to modify the loss in order to minimize the error over categorical values directly.
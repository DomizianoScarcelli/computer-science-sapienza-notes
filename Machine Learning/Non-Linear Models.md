---
Exam:
  - Deep Learning
---
A function could not be linear with respect to the input $x$, but we’re interested in the linearity with respect to the parameters $\theta$.

With little data points, we can arrive at the wrong assumption, for example we think that the data is linear (linear prior) but with more data points we see that this is not true.

In general more data points allow us to confirm or confute our hypothesis. Most of the time realizing that our assumption is not true is a difficult problem, because in the real world the model has a lot of parameters with an high dimensionality.

In fact, the more the structure of the function is complex, the more parameters we need in order to encode that complexity. Just think that for a $i$-th polynomial function we need $i+1$ parameters ($a_1, \dots a_n, b$).
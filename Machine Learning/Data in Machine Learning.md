---
Exam:
  - Deep Learning
---
Machine learning means learning from the data, so that’s the most important part. The first thing that has to be done is to look at the data, since it can be structured or not.

If we don’t look at the data, it may happen that we miss the underlying structure and so we don’t understand the results, or we can make some mistakes. 

![Screenshot 2023-02-28 at 6.07.21 PM.png](Screenshot_2023-02-28_at_6.07.21_PM.png)

In this example we can see that all the quadrants but $I$ has some structure, but the statistics are exactly the same for every dataset. This shouldn’t be the case since they have very different structures, so statistics alone cannot be trusted.

Sometimes data cannot be visualized because of the highly dimentional space in which it’s defined, or because there isn’t a physical access to it.

Learning means describing the process (or the model) that yields a given output from a given input.
### Functions vs Parameter curve

Data sometimes can be described as a function. For example a line can be described as $y = ax+b$. In the case of machine learning, the input and output $x$ and $y$ are known, and the unknown are the parameters (or weights) $a$ and $b$. This means that, given the $x$ and $y$, we want to find the $f$ that describes the data.

The data can be described in a lot of ways, no one is the correct way, but it can affect the result and the computation.

Parametric equations are another way of describing the data. The same line as before can be expressed as:

$$
\begin{pmatrix}
x \\
y
\end{pmatrix} = 
\begin{pmatrix}
a_x \\
a_y
\end{pmatrix} t
+ \begin{pmatrix}
b_x \\
b_y
\end{pmatrix}
$$

The parameter $a_i$ describes how $t$ scales with respect to the $i$ coordinate, and the parameter $b_i$ describes how much it’s shifted with respect to the $i$ coordinate.

The weights in this case are $2$ for the function representation, and $4$ for the parametric curve.

This is useful since sometimes data cannot be represented with a function of the coordinates. Sometimes both representation are possible, and we need to make trade-off between the number of weights and the simplicity of the representation.

In a nutshell, building a machine learning model (or a neural networks) means choosing a certain function from an infinite number of functions and solve it for the parameters. Most of the times defining a function that describes the data can be challenging.
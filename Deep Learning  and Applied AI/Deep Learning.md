# Data

Machine learning means learning from the data, so that’s the most important part. The first thing that has to be done is to look at the data, since it can be structured or not.

If we don’t look at the data, it may happen that we miss the underlying structure and so we don’t understand the results, or we can make some mistakes. 

![Screenshot 2023-02-28 at 6.07.21 PM.png](Screenshot_2023-02-28_at_6.07.21_PM.png)

In this example we can see that all the quadrants but $I$ has some structure, but the statistics are exactly the same for every dataset. This shouldn’t be the case since they have very different structures, so statistics alone cannot be trusted.

Sometimes data cannot be visualized because of the highly dimentional space in which it’s defined, or because there isn’t a physical access to it.

Learning means describing the process (or the model) that yields a given output from a given input.

### Prior knowledge

The prior knowledge is the knowledge that is known a priori, before the learning. This can make the data representation and the model construction easier.

Some forms of prior knowledge is:

- Data distribution
- Energy function
- Constraints (for example if the data is defined in a certain range)
- Invariances
- Input-output examples: this is called data prior. The data is a prior knowledge and sometimes is the only prior knowledge we have.

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

<aside>
💡 In the slide 02_data, from page 21 is possible to find how the first image of the black hole was constructed using machine learning techniques.

</aside>

### Reliability of the prior and fairness

The data provided by human can be highly biased. For example the AI that’s responsible to assign a score to each resume that a certain popular company receives can be biased and assign scores that are not based on the actual potential of the person, but may be on the gender or the ethnicity. This means that the model is not *fair*.

Sometimes is the observation that is biased. For example if a certain zone of the earth is monitored for crimes more than other, it can seem like in that area more crimes are commited, when in fact it’s just monitored more and so more crimes are detected, but it doesn’t mean that they happen more frequently. In this case, the data is not reliable. 

### Curse of Dimensionality

An image can be represented as a grid of pixels, as an histogram of pixel’s frequency etc. It can also be seen as a point in a $d$-dimensional space, where $d$ is the total number of pixels of the image.

In this space, there are all the possible images with that numbers of pixels. In case of a $1$ megapixel image, the number of pixels (and so dimensions) is $1$ million.

In this highly dimensional space, the number of images to cover all the space is $2^{1.000.000}$ that is a huge number.

This is the curse of dimensionality, which is a phenomenon where as the dimensions increases, the number of datapoints to cover the space increases in a quadratic way. This makes the space sparse, meaning that the probability of two random points being close to each other is very very low. This is a problem since it makes machine learning models struggle to fit the data.

To overcome this, it’s possible to represent the data with less dimension, using dimensionality reductions methods as PCA; or add more data. The first one being better than the second.

Another important concept is orthogonality. This happens when the inner product between two vector is $0$. In a sparse space, it’s much more probable that two random points are orthogonal between each other than not, since if they’re not it means that they’re very close to each other.

## Features

We assume that each data point $x$ is the result of a process $\sigma$ that takes in input a set of features $F$ (feature space) and composes them to form the data point $x$.

$$
\sigma:F \to x
$$

Both $\sigma$ and $F$ are unknown.

### Example of $\sigma$ for image representation

![Screenshot 2023-03-01 at 6.38.46 PM.png](Screenshot_2023-03-01_at_6.38.46_PM.png)

In this case the image is the data point, and each pixel $x$ is a feature. The $\sigma$ function just scales each pixel by a certain factor (all the pixels here have the same value) and then sums everything up to obtain the final image.

The representation in this case is very inefficient, since the image has as many dimensions as pixels. Ideally we want the features to depend only on the semantic of the image, and not on the number of pixels.

In this case $F$ is a vector space, and $\sigma$ is linear. Generally, the transformation $\sigma$ gets in input much less features and non-linearly transforms them in order to obtain the image.

Features are *task-driven*, meaning that a certain representation may make sense only if it makes sense in that particular task.
For example it’s useless to represent a certain card with the rank and the color if the rank it’s not important for the task.

### Embeddings

The output of $\sigma$  is called an embedding of the data point. In general, multiple embeddings are possible for each data point.

**Example:**

A sheet can be embedded as a 2D sheet, and so it will live in $\mathbb{R}^2$, but it may be represented with other 3D shapes, and will live in $\mathbb{R}^3$.

![Screenshot 2023-03-01 at 6.05.07 PM.png](Screenshot_2023-03-01_at_6.05.07_PM.png)

In this case three different embeddings are representing the same intrinsic object. In this particular case, it’s possible to prove that the intrisic object underneath the embedding is the same because it mantains some intrinsic properties, for example the distance between each pair of points. This property is called isometry.

The challenge here is to discover which are the intrisic properties that are preserved, since those are the properties that characterize the data.

Most of the time we have only access to the embedding, and not the intrinsic object (for example a photo of a dog can be an embedding, but the instrinsic idea of a dog is not so clear).

### Latent Features

Features are not always localized in space, nor evident in the embedding. These type of features are called latent features. 

An exemple can be the directional illumination on a certain object, that can be expressed with only 4 parameters (3 for the coordinates and 1 for the intensity).

## Optimal dimensionality

Even just discovering the intrinsic dimensionality is a challenge.

<aside>
💡 Manifold learning is a field of machine learning that aims to solve this problem.

</aside>

This problem is so difficult that today the procedure usually is to fix one dimensionality and try to find the rest of the unknowns. If everything works well than it’s ok, otherwise we try again with another dimensionality.

![Screenshot 2023-03-01 at 6.15.54 PM.png](Screenshot_2023-03-01_at_6.15.54_PM.png)

This phenomenon describes how increasing the dimensionality of the data, the model performs better, until a certain peaking point. (Each line is a different model, that can be seen as a different $\sigma$).

<aside>
💡 The double ascent phenomenon, seen for the first time just a couple of years ago, states that there will eventually exists another peak if the dimensions continue to increase, but this is very computationally expensive.

</aside>

## The manifold hypothesis (just an intuition…)

Deep learning makes a big assumption, which is that the input data lives on an underlying non-Euclidean structured called a manifold.

In this manifold there are subspaces where the same type of objects exists. For example in a certain subspace there may be only photos of mountains.

---

<aside>
💡 After all these concepts, deep learning can be described as: “A task-driven paradigm to extract patterns and latent features from given observations”

</aside>

Features are not always the focus of deep learning, but they’re the tool that allows to arrive to a certain decision.

# Linear Algebra Revisited

<aside>
💡 Linear algebra is the study of linear maps of finite dimensional vector spaces.

</aside>

## Vector Space

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

In the case of the vector space made of functions, for it to be finite dimentsional, the domain has to be finite.

## Linear Maps

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

## Matrices

> Linear algebra is about matrices as much as astronomy is about telescopes.
> 

Consider a linear map $T: V \to W$ and two basis, one $v_1\dots,v_n \in V$ and another $w_1,\dots,w_n \in W$:

The matrix of $T$ in these bases is the $m \times n$ array of values in $\mathbb{R}$

 

$$
T = \begin{pmatrix}
T_{1,1} && \dots && T_{1,n} \\
\vdots && \ddots && \vdots \\
T_{m,1} && \dots && T_{m,n} \\
\end{pmatrix}
$$

Where each column contains the linear combination coefficients that describes how the basis vectors are mapped from one vector space to another.

In fact, the $T_{i,j}$ entries are defined by:

$$
Tv_j = T_{1,j}w_1+\dots+T_{m,j}w_m
$$

Matrices are just a representation the linear maps, which depends on the basis that are chosen. Whenever we have to do operation between matrices, the bases have to be the same, othewise we’re dealing with coefficient that represent differnet things.

### Matrix of a vector

Just how matrices represent how the basis vectors are mapped from a vector space to another, the matrix of a vector (that has size $n \times 1$ where $n$ is the length of the vector) describes the vector in terms of coefficient of the basis vectors (so it describes how the basis vectors has to be stretched in order to obtain that particular vector).

Once again, the matrix depends on the choice of the basis for that particular vector space where the vector is.

# Linear Models

A neural network can be thought out as a function with a complex structure and a high number of parameters $\theta$. The name *deep neural network* comes from the fact that there are many different hidden layers, that are just smaller blocks. Each of these blocks has a predefined structure, for example, a linear map (remember that a matrix is just a representation of a linear map).

When we *train* a neural network, we are just solving the function for the parameters $\theta$. We are able to do this by minimizing a function that’s called *loss*, by computing the gradients and using *backpropagation.*

Let for example $f_\Theta(x) = ax + b$ be our function, then we need to find $\Theta = \{a, b\}$.

## Linear Regression

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

### Jensen’s inequality

Jensen’s inequality states:

$$
f(\alpha x + (1-\alpha)y) \le \alpha f(x) + (1-\alpha)f(y)
$$

Meaning that taking two points $(x, f(x))$ and $(y, f(y))$ of a convex function, every point on their linear convex combinations (meaning the set of all points on the line that crosses the two points) is bigger than the point at that coordinate taken on the actual curve.

![Visual representation of Jensen’s inequality](Screenshot_2023-03-15_at_4.58.03_PM.png)

Visual representation of Jensen’s inequality

> If Jensen’s inequality is true for each possible pairs of points of a function, than the function is convex.
> 

We can find the minimum by computing the derivative of the function and putting it to zero. If the function is convex, than we have the guarantee that there is only a minimum; if the function is non-convex, than there may be multiple minima, and only one global minimum.

In a convex function, the global minimizer $x$ is where $\frac{df(x)}{dx} = 0$.

The Jensen’s inequality principle is true also for more than two dimensions. In this case the notion of derivative is replaced with the notion of gradient, that is the vector of partial derivative with respect to each single parameter.

$$
\nabla_xf(x) = 
\begin{pmatrix}
\frac{\partial f}{\partial x_1} \\
\vdots \\
\frac{\partial f}{\partial x_n} \\
\end{pmatrix}
$$

We also have the global optimality condition, that states:

$$
\nabla_xf(x) = 0 \rightarrow f(x) \le f(y) \quad \forall y \in \mathbb{R}^n 
$$

### Gradient

The gradient $\nabla_xf(x)$ encodes the direction of the steepest ascent of $f$ at point $x$. It aways lives on the domain of the function $f$.

In case of a 1D function, encodes the direction on the $x$ or $y$ axis where the function grows the most.

In case of a 2D function, it encodes the direction on the plane.

<aside>
💡 Note that even if we visualize the 2D function in a 3D plane, the function is still 2D. As we visualize a 1D function on a 2D plane.

</aside>

The length of the gradient vector encodes the strongness of the steepest ascent, meaning how much fast the function grows.

## Vector lengths

### Euclidean distance

The Euclidean distance measures the length of a straigth line connecting two points.

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

<aside>
💡 Note that the number of dimensions $k$ for points in $\mathbb{R}^k$ and the $p$ coefficient are two different things.

</aside>

---

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

# Non Linear Models

As we’ve seen before, a function could not be linear with respect to the input $x$, but we’re interested in the linearity with respect to the parameters $\theta$.

With little data points, we can arrive at the wrong assumption, for example we think that the data is linear (linear prior) but with more data points we see that this is not true.

In general more data points allow us to confirm or confute our hypothesis. Most of the time realizing that our assumption is not true is a difficult problem, because in the real world the model has a lot of parameters with an high dimensionality.

In fact, the more the structure of the function is complex, the more parameters we need in order to encode that complexity. Just think that for a $i$-th polynomial function we need $i+1$ parameters ($a_1, \dots a_n, b$).

### Polynomial regression (linear regression with polynomial features)

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

### The Stone-Weierstrass theorem

The *Stone-Weierstrass* theorem tell us that:

> If $f$ is continuous on the inverval $[a,b]$, then for every $\epsilon > 0$ there exists a polynomial $p$ such that $|f(x) - p(x)| < \epsilon \quad \forall x$.
> 

In other terms, every continuous function can be approximated by some polynomial with a certain level of accuracy. This is why in ML polynomial are used so much. 

### Overfitting vs Underfitting

![Underfitting - Just right fit - Overfitting](Screenshot_2023-03-15_at_5.45.18_PM.png)

Underfitting - Just right fit - Overfitting

Overfitting and Undefitting are two phenomenons that may happen during the construction of the model that we want to avoid.

Underfitting (the image on the leftmost part) is when the model poorly fits the data, because of a too much generalization. We can notice that because we have a large MSE.

Overfitting (the image on the rightmost part) is when the model fits too well the training data, but isn’t able to generalize on different data. This translated on little or zero MSE error on the training data, but large error with different data. This also means that the model is “learning the noise”.

Generalization is an important concept in machine learning, and it means that the model performs well on data that is not part of the training set.

In order to see if the model is able to generalize, we should reserve some data for the “validation set”, that is a part of the data that we use to measure the error of the model. The important part is that the validation data, as well as the test data, is data that the model has never seen. 

In general we can see if we’re building the model in a good way by following this path

![Untitled-2023-02-04-1558.png](Untitled-2023-02-04-1558.png)

---

Since we can approximate every continuous function with a polynomial, is polynomial regression all we need in order to fit the data?

The answer to this question is **no**, since polyinomial regression is kind of limited, and we cannot perform some useful thing with it, for example:

- If we want different loss functions than MSE;
- If we want to apply regularization;
- If we have additional priors;
- If we want to compute intermediate features;
- If we want more flexibility;
- If we want to perform classification instead of regression.

# Classification

Classification is the task of predicting a category instead of a value.

In particular, a binary classification function is of the type:

$$
f_\Theta(\mathbb{X}) = \{0,1\}
$$

A possible solution is to use linear regression and then do some post-processing, such as thresholding, in order to convert the real value to a binary label. This is not an optimal solution since the function is optimized for the MSE loss, but once the output is converted, this is not true anymore.

The idea is to modify the loss in order to minimize the error over categorical values directly.

## Logistic Regression

We can define the new loss as:

$$
\ell_\Theta(\{x_i, y_i\}) = \sum_{i=1}^n(y_i - \sigma(ax_i+b))^2
$$

where the nonlinear $\sigma$ function is called *logistic sigmoid*

$$
\sigma(x) = \frac{1}{1+e^{-x}}
$$

![Screenshot 2023-03-15 at 5.58.58 PM.png](Screenshot_2023-03-15_at_5.58.58_PM.png)

The sigmoid function is used to *squash* the output of $f$ into a value between $(0,1)$. This means that the function has a *saturation* effect as it maps $\mathbb{R} \to (0,1)$.

Note that this new loss is non-linear with respect to the parameters, since they appear in the non-linear sigmoid function, and it’s also non-convex.

We want the loss to be convex, so we can write a new loss function with this property that will output an high value if the output label is wrong, and a low value if it’s true.

$$
c(x_i, y_i) = 
\begin{cases}
- \ln(\sigma(ax_i+b)) & y_i = 1 \\
- \ln(1-\sigma(ax_i+b)) & y_i = 0
\end{cases}
$$

This works well because if the prediction $\sigma(ax_i+b)$ is near the $0$, and the true label is $1$, then $-\ln(\sigma(ax_i+b)) \to \infty$.
On the other hand, if the true label is $0$, then $-\ln(1-\sigma(ax_i+b)) \to 0$.

We can rewrite the function on a single line:

$$
c(x_i, y_i) = -y_i \ln(\sigma(ax_i+b)) - (1-y_i)\ln(1-\sigma(ax_i+b))
$$

The function is still non-linear with respect to the parameter, but is convex.

The loss for the entire dataset will be:

$$
\ell_\Theta(\{x_i, y_i\}) = \sum_{i=1}^nc(x_i, y_i)
$$

### Closed form solution for Logistic Regression

As we did for the Linear Regression case, we want to find a closed form solution by putting the gradient of the loss equal to zero. Since the loss is convex, we will find the global minimum.

- Finding theta such as $\nabla_\Theta\ell_\Theta = 0$
    
    We set the gradient to zero and we want to solve it for $\Theta$.
    
    $$
    \begin{align}
    \nabla_{\Theta} \sum_{i=1}^n y_i \ln \left(\sigma\left(a x_i+b\right)\right)+\left(1-y_i\right) \ln \left(1-\sigma\left(a x_i+b\right)\right)=0 \\
    
    \end{align}
    $$
    
    Since the gradient operation is linear, the gradient of the summation is just the sum of the gradient of each term, so we can consider just the gradient of a single term.
    
    $$
    \begin{align}
    \nabla_{\Theta}  y_i \ln \left(\sigma\left(a x_i+b\right)\right)+ \left(1-y_i\right) \ln \left(1-\sigma\left(a x_i+b\right)\right)
    \\
    \nabla_{\Theta}  y_i \ln \left(\sigma\left(a x_i+b\right)\right)+\nabla_{\Theta} \left(1-y_i\right) \ln \left(1-\sigma\left(a x_i+b\right)\right)
    \\
    y_i\nabla_{\Theta}   \ln \left(\sigma\left(a x_i+b\right)\right)+\left(1-y_i\right)\nabla_{\Theta}  \ln \left(1-\sigma\left(a x_i+b\right)\right)
    \\
    y_i\nabla_{\Theta} \underbrace{\ln \left(\sigma\left(a x_i+b\right)\right)}_{f(g(h(\Theta)))}+\left(1-y_i\right)\nabla_{\Theta}  \ln \left(1-\sigma\left(a x_i+b\right)\right)
    \end{align}
    $$
    
    We can apply the chain rule in order to take the derivative of the composition of three function.
    
    $$
    \begin{align}
    \frac{\partial}{\partial a}f(g(h(a,b))) = \frac{\partial f}{\partial g} \cdot \frac{\partial g}{\partial h} \cdot \frac{\partial h}{\partial a}
    \end{align}
    $$
    
    We solve the first partial derivative:
    
    $$
    \begin{align}
    \frac{\partial h}{\partial a} =\frac{\partial}{\partial a} ax_i+b = x_i 
    \end{align}
    $$
    
    We solve the second partial derivative:
    
    $$
    \begin{align}
    \frac{\partial g}{\partial h} =\frac{\partial \sigma(ax_i+b)}{\partial (ax_i+b)} = \frac{\partial}{\partial\left(a x_i+b\right)} \frac{1}{1+e^{-\left(a x_i+b\right)}} = \frac{e^{-\left(a x_i+b\right)}}{\left(1+e^{-\left(a x_i+b\right)}\right)^2} \\
    =
    \frac{1}{1+e^{-\left(a x_i+b\right)}} \frac{e^{-\left(a x_i+b\right)}}{1+e^{-\left(a x_i+b\right)}} \\
    = \frac{1}{1+e^{-\left(a x_i+b\right)}} \frac{\left(1+e^{-\left(a x_i+b\right)}\right)-1}{1+e^{-\left(a x_i+b\right)}} \\
    = \frac{1}{1+e^{-\left(a x_i+b\right)}}\left(1-\frac{1}{1+e^{-\left(a x_i+b\right)}}\right) \\
    =
    \text { - } \sigma\left(a x_i+b\right)\left(1-\sigma\left(a x_i+b\right)\right)
    \end{align}
    $$
    
    Finally we solve the third partial derivative:
    
    $$
    \begin{align}
    \frac{\partial f}{\partial g} =
    \frac{\partial \ln \left(\sigma\left(a x_i+b\right)\right)}{\partial \sigma\left(a x_i+b\right)} =\frac{1}{\sigma\left(a x_i+b\right)}
    \end{align}
    $$
    
    Plugging everything in the equation at $(6)$:
    
    $$
    \begin{align}
    \frac{\partial}{\partial a} f(g(h(a, b)))=\frac{1}{\sigma\left(a x_i+b\right)} \cdot \sigma\left(a x_i+b\right)\left(1-\sigma\left(a x_i+b\right)\right) \cdot x_i \\
    = \left(1-\sigma\left(a x_i+b\right)\right) \cdot x_i
    \end{align}
    $$
    
    And so:
    
    $$
    \frac{\partial}{\partial a} \ln \left(\sigma\left(a x_i+b\right)\right)=\left(1-\sigma\left(a x_i+b\right)\right) x_i
    $$
    
    Now this should be done also for the left ther of $(5)$, and everything should be repeated w.r.t. $b$ in order to compute the full gradient.
    

We can see from a part of the partial derivative which consistutes the gradient:

$$
\frac{\partial}{\partial a} \ln \left(\sigma\left(a x_i+b\right)\right)=\left(1-\sigma\left(a x_i+b\right)\right) x_i
$$

that the system of equations that we have when we set the gradient to $0$ wouldn’t be a linear system, since both $a$ and $b$ are involved in a non-linear function and so it cannot be easily solved.

Furthermore, the system is a transcendental equation, because it involves the exponential function inside the sigmoid function, which definition is the sum of an infinite series. Because of that, an analytical solution, and so a closed form solution, doesn’t exist.

In order to find the parameters that minimize the loss, we need to use an iterative method like stochastic gradient descent.

![Screenshot 2023-03-15 at 6.11.06 PM.png](Screenshot_2023-03-15_at_6.11.06_PM.png)

# Gradient Descent

Gradient descent is an iterative algorithm that allows to find the minimum of a certain function. This is useful in order to find the parameters that minimize a certain loss function that cannot be solved analitically.

The algorithm uses tha fact that the gradient of a function is a vector defined of the domain of the function which encodes the direction of its steepest ascent. This mean that we should be able to follow the direction of the negative gradient at each point in order to go towards the minimum of the function.

The general idea is:

- Start from some point $\mathbb{x} \in \mathbb{R}^n$;
- Iteratively compute the $\mathbb{x}$ at the next step:

$$
\mathbb{x}^{(t+1)} = \mathbb{x}^{(t)} - \alpha \nabla \ell _\mathbb{x^{(t)}}
$$

- Stop when the minimum is reached.

We can write the formula in this way:

$$
\mathbb{x}^{(t+1)} = \mathbb{x}^{(t)} - \alpha \nabla f(\mathbb{x^{(t)}})
$$

Remember that is possible to perform the subtraction because the gradient of the function lives in the domain of the function, and so the dimensionality will match.

In order to visualize the gradient, assuming $f: \mathbb{R}^2 \to \mathbb{R}$, we can both visualize the 2D function in a 3D space, or we can inspect its iso-lines.

An iso-line (or level curve) is the line of the function projected into the plane where the function has the same value. Each function has infinitely many iso-lines. Note that an iso-line is always a closed path.

This is useful since we can see the gradient as a vector field in a 2D surface.

![The 2D function and some of its iso-lines](Screenshot_2023-03-22_at_4.15.39_PM.png)

The 2D function and some of its iso-lines

We can zoom on the iso-lines in order to better inpect the negative gradient.

![Screenshot 2023-03-22 at 4.15.54 PM.png](Screenshot_2023-03-22_at_4.15.54_PM.png)

From this image we can see that the vector field is smooth, that’s because the function is smooth. Also we can notice that the arrows points towards a lower zone of the function, that’s because we are dealing with the negative gradient.

The gradient in each point has different direction and magniture.

This representation is also valid for 3D functions, meaning $f: \mathbb{R}^3 \to \mathbb{R}$. In this case the projection of the function will be a surface, and so they will be called iso-surfaces (or level surfaces).

![Screenshot 2023-03-22 at 4.34.55 PM.png](Screenshot_2023-03-22_at_4.34.55_PM.png)

### Orthogonality of the gradient

From the 2D gradient vector field, we can also notice that each arrow on the iso-line is orthogonal to that line. Since there are infinitely many iso-lines, each arrow is orthogonal to a certain iso-line.

The proof is done by introducing the concept of directional derivative, that is the derivative of a multidimensional function with respect to a certain vector in that space. The vector encodes also the direction.

This because in a 1D function we can only compute the derivative in two directions, but in a 2D (or more) function we have infinitely many directions in which we can compute the derivative.

The directional derivative of the function $f$ with respect of the vector $\mathbb{v}$ is written as $\frac{\partial f}{\partial \mathbb{v}}$, and it’s equal to the inner product $\langle \nabla f, \mathbb{v}\mathbb{R}angle$ between the gradient and the vector.

![Screenshot 2023-03-22 at 4.40.22 PM.png](Screenshot_2023-03-22_at_4.40.22_PM.png)

The directional derivative will be a vector tangent to the iso-line, and by definition the iso-line is made out of the points in which the function has the same value, and so in that direction the value won’t change. This means that the derivative is zero, and so the inner product also is zero.

The fact that $\langle \nabla f, \mathbb{v}\mathbb{R}angle = 0$ means that $\nabla f$ is orthogonal to $\mathbb{v}$, and so is orthogonal to the iso-line.

### Differentiability

In order to apply gradient descent the function $f$ must differentiable.

For a function in 1D being differentiable means that we can compute its derivative. For a function with more dimensions, if we can compute all its partial derivatives doesn’t mean that the function is differentiable. 

$f$ is differentiable only if it has a continuous gradient.

### Stationary points

A stationary point is a point in which the gradient tends to zero. Gradient descent “gets stuck” at stationary point.

These points can be part of a local minimum or a saddle point.

Gradient descent will always end up in a stationary point, which stationary point depends on the initialization point.

In general we don’t want to find the global minimum of the function, since this would lead to bad performances (overfitting), but if you really want to optimize a function you can perform gradient descent with a lot of different initialization point, get to the same amount of minima, and then get the minimum of those minima.

![Screenshot 2023-03-22 at 4.59.08 PM.png](Screenshot_2023-03-22_at_4.59.08_PM.png)

### Learning Rate

The $\alpha$ parameter is called *learning rate* in the machine learning field, because it allows to scale up or down the step that we take on each iteration. Note that $\alpha$ is not the step, but $\alpha \|\nabla f\|$ is.

A small $\alpha$  means that we take small steps in the direction of the steepest descent, and so we will surely end up into a stationary point, but it may take a while.

A large $\alpha$ means that we take big steps, which means that we might arrive to the minimum faster, but we also risk to overshoot it, meaning we always surpass it because the step is too big.

Another way is to find the optimal $\alpha$ by a line search algorithm. This algorithm uses the fact that we can fix a direction and then solve the equation of the gradient in that direction, that would be 1D, in order to find the best $\alpha$. Formally we want to find $\text{argmin}_\alpha f(x^{(t)} - \alpha \nabla f(x^{(t)})$.

![Screenshot 2023-03-22 at 5.09.39 PM.png](Screenshot_2023-03-22_at_5.09.39_PM.png)

### Decay

Since a big learning rate is good at the start in order to speed up the descent, but it’s bad when the point is near the minimum because of the risk of overshooting, a good idea could be to make the $\alpha$ dynamic.

We call this type of $\alpha$ adaptive. This is done by decreasing it according to a decay parameter $\rho$, which defines the rate of the decay.

Examples of functions used to implement the decay are:

$$
\alpha^{(t+1)}=\frac{\alpha^{(t)}}{1+\rho_t}
$$

This function makes the learning rate decay according to an hyperbolic behaviour, because of the $\frac{1}{1 + \rho t}$ factor.

$$
\alpha^{(t+1)}=\alpha^{(0)} e^{-\rho_t}
$$

With this function the learning rate decreases exponentially.

$$
\alpha^{(t+1)}=\left(1-\frac{t}{\rho}\right) \alpha^{(0)}+\frac{t}{\rho} \alpha^{(\rho)}
$$

This function linearly scales the learning rate starting from $\alpha^{(0)}$ to $\alpha^{(\rho)}$ when the iterations increase.

## Momentum

With momentum we mean an extension of gradient descent in which we modify the trajectory of the point by accumulating past gradients.

The momentum is defined as:

$$
\mathbf{v}^{(t+1)}=\lambda \mathbf{v}^{(t)}-\alpha \nabla f\left(\mathbf{x}^{(t)}\right)
$$

Where $\lambda$  is (another) hyperparameter that affects the strength of the momentum, and so the acceleration of the point.

We can use the momentum to define the extended gradient descent:

$$
\mathbf{x}^{(t+1)}=\mathbf{x}^{(t)} + \mathbf{v}^{(t+1)}
$$

<aside>
💡 For $\lambda = 0$, then we have the standard gradient descent equation.

For $\lambda = 1$, in the first equation we will have the standard gradient descent, but from the second step we will accumulate the previous gradients. Also each lambda will be multiplied by the previous lambda, so we will have a power coefficient.

</aside>

We can re-define the step that we take at each iteration as:

$$
\frac{1}{1-\lambda}\alpha \|\nabla f\|
$$

We can see that the step is proportional to $\alpha$ and inversely proportional to $\lambda$.

The step length would be maximized when the new gradient has the same orientation as the previous one. This means that the point will accelerate, differently from standard GD in which the “speed” of the descent is always the same.

The physics interpretation of momentum can be thought like a ball that is put on the starting point of a surface. It will descend the surface according to gravity, but because of momentum it won’t change the direction instantly, but after some time.

With momentum the direction of each gradient is not orthogonal to the function iso-lines anymore.

Momentum is useful because it allows to speed up the descent in case the direction is unchanged, it also reduces the noise in case there are multiple changes of orientations, and also makes the point able to escape from local minima that aren’t strong enough.

This because, as a ball will surpass a small bump, the same will happen with a point that goes in a not so deep minimum. In case the point will go on a deeper minimum and doesn’t have too much momentum, it will stay there and stabilize after some time.

![Difference between GD with a fixed number of iterations with and without momentum.](Screenshot_2023-03-22_at_5.36.59_PM.png)

Difference between GD with a fixed number of iterations with and without momentum.

<aside>
💡 Note that we can use both decay and momentum togheter, but more things we put in the model, more difficult it will be to use it. A simple reason is that we always add more hyperparameters, and so adjust them in order for the model to behave in a optimal way is not trivial.

</aside>

### First-order acceleration methods

We can unroll the gradient descent, meaning we iterate over the steps and we write down the expression. We can see that in the general case, we can define the $\mathbb{x}^{(t+1)}$ as:

$$
\mathbf{x}^{(t+1)} =\mathbf{x}^{(0)}-\alpha \sum_{i=1}^t \nabla f\left(\mathbf{x}^{(i)}\right)
$$

- Unrollment process
    
    $$
    \begin{aligned}\mathbf{x}^{(1)} & =\mathbf{x}^{(0)}-\alpha \nabla f\left(\mathbf{x}^{(0)}\right) \\\mathbf{x}^{(2)} & =\mathbf{x}^{(1)}-\alpha \nabla f\left(\mathbf{x}^{(1)}\right) \\& =\mathbf{x}^{(0)}-\alpha \nabla f\left(\mathbf{x}^{(0)}\right)-\alpha \nabla f\left(\mathbf{x}^{(1)}\right) \\& \vdots \\\mathbf{x}^{(t+1)} & =\mathbf{x}^{(0)}-\alpha \sum_{i=1}^t \nabla f\left(\mathbf{x}^{(i)}\right)\end{aligned}
    $$
    

And with the use of momentum:

$$
\mathbf{x}^{(t+1)}=\mathbf{x}^{(0)}-\alpha \sum_{i=1}^t \frac{1-\lambda^{t+1-i}}{1-\lambda} \nabla f\left(\mathbf{x}^{(i)}\right)
$$

In a more general case, we can see that the gradient inside the summation is being multiplied by a certain coefficient. We can call this coefficient $\gamma_i$ and so we can rewrite the expression as:

$$
\mathbf{x}^{(t+1)}=\mathbf{x}^{(0)}-\alpha \sum_{i=1}^t \gamma_i^t \nabla f\left(\mathbf{x}^{(i)}\right)
$$

So in the case of momentum, we have $\gamma_i^t = \frac{1-\lambda^{t+1-i}}{1-\lambda}$ .

Instead of just multiplying the gradient by a vector, and so scaling it by a certain factor, we also may want to apply some transformation to it. This can be done by multiplying a matrix $\Gamma$, and so the even more general equation becomes:

$$
\mathbf{x}^{(t+1)}=\mathbf{x}^{(0)}-\alpha \sum_{i=1}^t \Gamma_i^t \nabla f\left(\mathbf{x}^{(i)}\right)
$$

<aside>
💡 Note that $\Gamma$ in the case of simple GD is just the identity matrix. Meanwhile for the case of momentum, it’s a diagonal matrix in which the elements on the diagonal are the elements of the $\gamma$ vector.

</aside>

These variations of gradient descent are called first-order acceleration methods, and they differ from each other because of a different $\Gamma$ matrix. Examples of this optmiziation algorithms are Adam and AdaGrad.

<aside>
💡 Note that gradient descent can be used to solve problems where no closed form solution exists, like Logistic regression, but can also be used where the solution exists, like Linear regression, since it may be more efficient.

In particular with linear regression we need to invert the $\mathbb{X}$ matrix, which is not an efficient operation if this matrix is huge, and that’s what happens most of the time.

</aside>

## Stochastic gradient descent

Gradient descent requires to compute the loss over $n$ training examples, which requires computing the gradient for each term in the summation.

In real world problems, $n$ can be very big, and also the number of parameters that we have to optimize, hence the dimensionality of the gradient, can be very big (order of millions). This can scale very quickly.

The idea is to not compute the loss for every single example, but randomly take a subset of a fixed size from the training set $\mathcal{T}$, for example $10$, that takes the name of mini-batch $\mathcal{B}$.

Even if the dimensionality of the gradient remains unchanged, we just have to do a limited and fixed number of operations on the small $\mathcal{B}$ set.

This means that we will approximate the gradient for each point, and so the step we take won’t be orthogonal to the iso-lines of the function anymore. Furthermore, if we plot how the loss changes during the various iterations, the curve won’t be monotonous anymore, since sometimes we might take the step in the wrong direction because of the approximation.

Another thing to consider it that we won’t ever stop at the point of minimum, but the point will always oscillate around it because of the noise that is introduced by the random sampling.

Even after this approximation the result is very good, and the speed up with respect to the vanilla GD is significant.

Once we’ve sampled all the examples in $\mathcal{T}$ taking small mini-batches each time, we have an epoch. The algorithm proceeds for many epochs.

<aside>
💡 An epoch is defined only if, for each epoch, the samples we use in a mini-batch won’t be used in the next mini-batches. In other words only if the sampling is done without replacement.

</aside>

### SGD Computational Cost

Let $n$ be the number of training examples and $d$ the number of parameters (dimensionality of the gradient).

Let also $\kappa$ and $\nu$ be two costants related to the *conditioning* of the problem.

Let also $\rho$ be the accuracy of the approximation with respect to the true value of the loss with the optimal minimizer:

$$
|\underbrace{\ell\left(f_{\Theta}\right)}_{\text {GD/SGD }}-\underbrace{\ell\left(f^*\right)}_{\text {true }}|<\underbrace{\rho}_{\text {accuracy }}
$$

We can prove that the computational cost of the SGD and the GD is the following:

|  | Cost per iteration | Iteration to reach $\rho$ |
| --- | --- | --- |
| GD | $O(nd)$ | $O(\kappa \log \frac{1}{\rho})$ |
| SGD | $O(d)$ | $\frac{\nu \kappa^2}{\rho} + O(\frac{1}{\rho})$ |

From this table we can see that SGD is better than standard GD because of many reasons:

- It doesn’t depend on the number of examples;
- It assures the convergence to a minimum in a finite number of steps, differently of GD which can take infinitely many steps before converging to a certain minimum. (WHY THIS?)

# Multilayer Perceptron

A multilayer perceptron (or deep feed-forward neural network) can be seen as a deep nested composition of functions, with a non-linear function (activation function) that produces the output of each single layer.

$$
\text{output}\leftarrow (\sigma \circ f) \circ(\sigma \circ f) \circ \dots \circ (\sigma \circ f) (x) \leftarrow \text{input}
$$

Note that the function composition operator $\circ$ is associative, so partentheses are not actually necessary.

$\sigma$ denotes the activation functions. If we have just one layer with the logistic function, then we have the logistic regression model. In general the $\sigma$s will be different across the layers, and can be of various types.

A popular sigma is the *ReLU* (Rectifier Linear Unit) that is defined as

$$
\sigma(x) = \max\{0, x\}
$$

And note that this is a continuous function but it has a discontinuous gradient in the point $0$, since on the left of that point the derivative is $0$, and on the right is $x$. So exactly in that point we have a singularity. This means that if the ReLU is present in any layers, the function will be non differentiable, and so we have to take care of it.

### Hidden layers

Let’s rewrite the composition of functions $g_\Theta(\mathbb{x})$, defined as:

$$
g_\Theta(\mathbb{x}) = (\sigma \circ f_{\Theta_n}) \circ(\sigma \circ f_{\Theta_{n-1}}) \circ \dots \circ (\sigma \circ f_{\Theta_1}) (x) 
$$

Each set $\Theta_i$ is the set of parameters of the $i$-th layer. Each intermediate layer can be expressed as:

$$
\mathbb{x}_{\ell+1} = \sigma_\ell(\mathbb{W}_\ell\mathbb{x}_\ell + \mathbb{b}_\ell)
$$

Where $\ell$ denotes the layer, $\mathbb{W}$ is the matrix of weights ($\Theta$), $\mathbb{x}$ is the input vector to the layer and $\mathbb{b}$ is the bias. Sometimes the bias can be included inside the $\mathbb{W}$ matrix, but in this case we must add a dimension full of $1$s in the $\mathbb{x}$ in order to match the shapes.

### Neurons

Each row of the weight matrix $\mathbb{W}$ is called a *neuron* or a *hidden unit*.

$$
\mathbb{W} \mathbb{x}=\left(
\begin{array}{c}- \text { unit }- \\\vdots \\- \text { unit }-\end{array}\right)
\left(
\begin{array}{c}\mid 
\\\mathbf{x} \\\mid\end{array}\right)
$$

<aside>
💡 In some papers the *neuron* might refer to the output of the $\mathbb{Wx}$ matrix multiplication.

</aside>

We can see the matrix multiplication $\mathbb{Wx}$ as a collection of $q$ vector-to-scalar functions $\mathbb{R}^p \to \mathbb{R}$ made in parallel, resulting in a new $\mathbb{R}^q$ vector.

### Single layer illustration

A single layer may be illustrated also with a graph where the first layer represents the components of $\mathbb{x}$, the second layer represents the output of the product $\mathbb{Wx}$, that is the linear combination between the vector $\mathbb{x}$ and the $i$-th row $\mathbb{w}_i$ of $\mathbb{W}$. We can see that the neuron will be a fully connected with the inputs, this is a fully connected layer. (There will also be cases of non-fully connected layers)

![A graph of the fully connected layer](Screenshot_2023-03-30_at_2.04.41_PM.png)

A graph of the fully connected layer

![Adding the non-linear function $\sigma$](Screenshot_2023-03-30_at_2.04.33_PM.png)

Adding the non-linear function $\sigma$

### Output Layer

The output layer determines the co-domain of the network. For example if $\sigma$ of the last layer in the network it’s the logistic sigmoid, then the entire network will map:

$$
\mathbb{R}^p \to (0,1)^q
$$

That might be a good idea in case of classification, but in a more general case it’s commont ot have a linear layer $f$ at the end of the network in order to map:

$$
\mathbb{R}^p \to \mathbb{R}^q
$$

### Deep ReLU Networks

Let’s once again rewrite the function $g_\Theta(x)$ as:

$$
\mathbb{y} = f \circ \sigma(\dots)(x)
$$

In this case we assume that the $\sigma$ functions are all the same, and are all ReLU functions, and so the network can be also called a Deep ReLU network.

We can see that $\mathbb{y}$ is expressed as a big linear combination combination of ridge functions $\sigma(\dots)$. With ReLU we’ll have that $\mathbb{y}$ is a piecewise-linear function, meaning that the whole function would not be linear, but each single ReLU output will be linear.

For example let’s imagine a deep network that has 2-layers and for each 2D point returns a real scalar. The output of the network will be something like this:

![Output of $\mathbb{y}$. On the right there is the above view.](Screenshot_2023-03-31_at_10.12.14_AM.png)

Output of $\mathbb{y}$. On the right there is the above view.

The blue edges are produced by the first layer, while the red ones by the second.

We can see that the function is linear in each activation region, and so is a piecewise-linear function.

Also note that the sharp edges of the output shape are due to the discontinuity of the gradient of the ReLU.

### Universal Approximation Theorems

There is a class of theorems called Universal Approximation Theorems (UAT) which answers to the question: “What class of functions can we represent with a MLP?

One of the first ever theorems of this class, if not the first one, tells us that:

> If $\sigma$ is sigmoidal, then for any compact set $\Omega \sub \mathbb{R}^p$, the space spanned by the functions $\phi(x) =  \sigma(\mathbb{Wx} + \mathbb{b})$ is dense in $\mathcal{C}(\Omega)$ for the uniform convergence. Thus, for any continuous function $f$ and any $\epsilon > 0$, there exists $q \in \N$ and weights s.t.:
> 
> 
> $$
> |f(x) - \sum_{k=1}^q u_k\phi(x)| \leq \epsilon \quad \text{for all }\mathbb{x \in \Omega}
> $$
> 

Being dense in $\mathcal{C}(\Omega)$ it means that if we take all linear combinations of $\phi$, they allow to represent all the possible continuous functions in a $p$-dimensional euclidean space.

Said that, the theorem tells us that we can approximate each continuous function with the desired accuracy using a MLP that has as few as just one layer. The larger is $q$, the smaller can the error between the real function and the approximator be.

Note that taking linear combinations of all the $\phi(x)$ means to just add a final linear layer.

There are also other UAT theorems that extends the universality for other $\sigma$s.

From this theorem we could think that a single hidden layer MLP is everything we need since it can approximise every existing continuous function, but we actually can’t. That’s because the theorem just says that those MLPs exist, but doesn’t tell us anything on how to do it.

### MLP Training

Given a certain loss $\ell_\Theta$, solving for the weights $\Theta$ is referred to as **training**.

In linear and logistic regression problems we’ve seen that the loss was always convex, but in general this isn’t the case. In fact the convexity of the loss comes from how $g_\Theta(\mathbb{x})$ is made. So if the neural network approximates a function that is very non-linear and very complex, the loss probably wouldn’t be convex, and so we cannot compute the gradient and set it to $0$ in order to minimize.

Also remember that we don’t want to find the global optimum, otherwise we will risk to overfit the training data.

<aside>
💡 The loss is convex for very specific cases, for example:

- Linear Regression: One layer, no activation function, MSE loss;
- Logistic Regression: One layer, sigmoid activation, logistic loss.
</aside>

Note also that the dimensionality of the gradient of $\Theta$ is determined by the dimensionality of the output of $g$.

## Backpropagation

We train the model using gradient descent-like algorithms. The bottleneck of the whole execution is computing the gradients of the loss $\nabla \ell_\Theta$.

Let’s evaluate the different solutions:

- Computing the gradients by hand will require an infeasible amount of time, and may produce some errors.
- We can use finite difference, meaning we compute an approximation of the derivative plugging in a very small number for the increment $h$, line $10^{-7}$ and then we compute the rate of change.
This is a better solution, but it would require $O(\text{\#weights})$ number of steps per datapoint, per iteration.
- We can create our custom software that takes a function an returns the symbolic expression that represent the derivative of that function, but also this would require the same amount of compuation steps as the solution before.

A better and efficient solution exists, and in order to explain that, we have to introduce ***computational graphs***.

### Computational Graph

Consider a generic function $f: \mathbb{R} \to \mathbb{R}$.

A computational graph is a directed acyclic graph (DAG) representing the computation of $f(x)$ with intermediate steps that are stored in intermediate variables.

Let’s see what’s the computational graph of the function

$$
f(x) = \log x + \sqrt{\log x}
$$

![Screenshot 2023-03-31 at 10.46.51 AM.png](Screenshot_2023-03-31_at_10.46.51_AM.png)

If you would write a program that solves that equation, you will store intermediate results (for example $\log x$) into a variable ($y$ in the graph) in order to reuse it later. What’s a computational graph does is exactly the same things, keeping also track of what’s the variables that produced that specific result.

Let’s see another example for the function:

$$
f(x)=\frac{\log \left(x+\sqrt{x^2+1}\right)}{x^2}-\frac{\log ^3\left(x+\sqrt{x^2+1}\right)}{\sqrt{x^2+1}}
$$

![GIF animation of the computational graph](output.gif)

GIF animation of the computational graph

![Final computational graph](Screenshot_2023-03-31_at_10.51.12_AM.png)

Final computational graph

We can evaluate $f(x)$ by traversing the graph from the input $x$ to the output $f(x)$.

In PyTorch and other frameworks, the computational graph is constructed when we make the operations, like:

```python
z = torch.sqrt(torch.sum(torch.pow(x, 2),1))
```

The computational graph gets big very quickly for compelx and highly dimensional functions.

### Automatic differentiation: Forward mode

We want to use the computational graph not only to evaluate $f(x)$, but also to evaluate the derivative $\frac{\partial f}{\partial x}$, and w.r.t all the intermediate nodes ($\frac{\partial y}{\partial x}, \frac{\partial z}{\partial x}$). We can do that by forward traversing the graph, and compute the derivatives using the other derivatives we compute along the way.

<aside>
💡 In the forward mode we compute the derivative of the intermediate nodes w.r.t. the input $x$.

</aside>

Let’s see how we can compute the $\frac{\partial f}{\partial x}$ by doing the forward-pass on the computational graph of the function $f(x) = \log x + \sqrt{\log x}$.

![Screenshot 2023-03-31 at 10.46.51 AM.png](Screenshot_2023-03-31_at_10.46.51_AM.png)

$$
\begin{aligned}& \frac{\partial x}{\partial x}=1 \\& \frac{\partial y}{\partial x}=\frac{\partial y}{\partial x} \frac{\partial x}{\partial x}=\frac{\partial \log x}{\partial x} \frac{\partial x}{\partial x}=\frac{1}{x} \frac{\partial x}{\partial x} \\& \frac{\partial z}{\partial x}=\frac{\partial z}{\partial y} \frac{\partial y}{\partial x}=\frac{\partial \sqrt{y}}{\partial y} \frac{\partial y}{\partial x}=\frac{1}{2 \sqrt{y}} \frac{\partial y}{\partial x} \\& \frac{\partial f}{\partial x}=\frac{\partial f}{\partial y} \frac{\partial y}{\partial x}+\frac{\partial f}{\partial z} \frac{\partial z}{\partial x}=\frac{\partial(y+z)}{\partial y} \frac{\partial y}{\partial x}+\frac{\partial(y+z)}{\partial z} \frac{\partial z}{\partial x}=\frac{\partial y}{\partial x}+\frac{\partial z}{\partial x}\end{aligned}
$$

The assumption we make is that each partial derivative is a primitive, that has a closed form solution and so can be computed on the fly. This is implemented using a lookup table ($O(1)$ cost for the look up) that maps each type of primitive derivative to its closed form solution in order to get the result efficiently.

If the input has only one dimension, than the cost of computing $\frac{\partial f}{\partial x}$ is the same as computing $f(x)$.

In general though, if the input has $p$ dimensions, the cost of computing $\nabla f(x)$ has a multiply factor of $p$, since we have to compute $p$ different derivatives w.r.t all the parameters ($p \times \text{cost of computing }f(x)$ ).

### Automatic differentiation: Reverse mode

The solution to compute the gradient of $f$ in an efficient way that doesn't depend on the input dimensionality $p$ is by traversing the graph in the reverse mode, meaning from the output $f$ to the input $\mathbb{x}$, computing all the derivatives of $f$ w.r.t. the inner nodes ($\frac{\partial f}{\partial z}, \frac{\partial f}{\partial y}, \dots\frac{\partial f}{\partial x}$).

<aside>
💡 In the reverse mode we compute the derivative of the output $f$w.r.t. the intermediate nodes.

</aside>

Let’s again see how we can compute $\frac{\partial f}{\partial x}$ of the same function $f$, but this time traversing the graph in the reverse order:

![Screenshot 2023-03-31 at 11.22.07 AM.png](Screenshot_2023-03-31_at_11.22.07_AM.png)

$$
\begin{aligned}& \frac{\partial f}{\partial f}=1 \\& \frac{\partial f}{\partial z}=\frac{\partial f}{\partial f} \frac{\partial f}{\partial z}=\frac{\partial f}{\partial f} \frac{\partial(y+z)}{\partial z}=\frac{\partial f}{\partial f} \\& \frac{\partial f}{\partial y}=\frac{\partial f}{\partial z} \frac{\partial z}{\partial y}+\frac{\partial f}{\partial f} \frac{\partial f}{\partial y}=\frac{\partial f}{\partial z} \frac{\partial \sqrt{y}}{\partial y}+\frac{\partial f}{\partial f} \frac{\partial(y+z)}{\partial y}=\frac{\partial f}{\partial z} \frac{1}{2 \sqrt{y}}+\frac{\partial f}{\partial f} \\& \frac{\partial f}{\partial x}=\frac{\partial f}{\partial y} \frac{\partial y}{\partial x}=\frac{\partial f}{\partial y} \frac{\partial \log x}{\partial x}=\frac{\partial f}{\partial y} \frac{1}{x}\end{aligned}
$$

<aside>
💡 Note that $\frac{\partial f}{\partial y}$ is the sum of the derivatives of the two path on the graph because $f$ is obtained like the sum of $y$ and $z$.

</aside>

Reverse mode requires computing the values of the internal nodes first, which can be done by doiing a forward pass, in which we just evaluate the function and its inner node, but we don’t autodifferentiate. Once done that, we can do a backward pass in order to compute the derivatives of the output w.r.t. to each inner node and the input.

### Forward mode vs Reverse mode computational cost

When we train neural networks, we’ll always have a loss function of the type:

$$
\ell: \mathbb{R}^p \to \mathbb{R}
$$

That maps a $p$ dimensional vector to a scalar. Even if the output of the network has $q$ dimensions, the output of the loss function will always be a scalar.

In a general way, we can write the forward-mode autodifferentiation and the reverse-mode autodifferentiation in this way:

Let $\mathbb{J}_k$ be the Jacobian (generalization of the gradient: matrix of partial derivatives) at layer $k$, then:

- **Forward-mode** autodiff**:**
    
    $$
    \nabla \ell = \mathbb{J}_{t-1}(\mathbb{J}_{t-2}(\cdots(\mathbb{J}_{3}(\mathbb{J}_{2}\mathbb{J}_{1}))))
    $$
    
    The parenthesis in this case defines how we store the operation into a new variable. Each operation that is inside of parenthesis will be stored and then reused in the chain rule.
    
    In this case (reading from right to left) since the first layer has a dimensionality of $p$, this dimensionality will be carried throughtout all the computation, and so we need to a number of operations more or less equal to:
    
    $$
    p \sum_{k=2}^{t-1}d_kd_{k+1}
    $$
    
- **Reverse-mode** autodiff:
    
    $$
    \nabla \ell = ((((\mathbb{J}_{t-1}\mathbb{J}_{t-2})\mathbb{J}_{t-3})\cdots)\mathbb{J}_{2})\mathbb{J}_{1}
    $$
    
    In this case we start from the last layer, that we know being a scalar, so we will carry out through the computation only the single dimension, and so we need to compute a number of operations that don’t depend on the dimensionality of the input.
    
    $$
    1 \sum_{k=1}^{t-2}d_kd_{k+1}
    $$
    
    <aside>
    💡 Backpropagation is the reverse mode automatic differentiation applied to deep neural networks.
    
    Autodifferentiation is a general computational technique that allows to efficiently compute derivatives. This is different from symbolic differentiation (tools like Mathematica) that returns the symbolic formula that describes the derivative.
    
    </aside>
    

# Convolutional Neural Networks

What makes Convolutional Neural Networks (CNN) interesting is the fact that they exploit data priors in order to obtain great results with much less parameters than MLP.

# Priors

Since deep neural networks can be very complex, have a huge number of parameters and so can be difficult to optimize, we need additional priors as a partial remedy. 

For each piece of data that we want to learn, we assume that it has a structure underneath that has to be learned.

Images that are completely random don’t have a structure, and so there is nothing to learn. In real world examples images always have some structure, so this can be considered as a prior: structure in terms of repeating patterns, compositionality, locality and more.

<aside>
💡 For example, if we want to solve a small-piece jigsaw puzzle, where an image is tassellated and each piece is in a random position, we can just rearrange the pieces in order for them to be close to the ones that have the lower jump in color. By doing this, we will obtain the original image.

![Result.png](Result.png)

</aside>

This of course is valid not only for images, but for every type of data.

## Self-Similarity

![Screenshot 2023-04-05 at 3.19.49 PM.png](Screenshot_2023-04-05_at_3.19.49_PM.png)

Data tends to be self-similar across the domain. For example in the image above, we can see that patches of pixels, even if they semantically represent different things, are very similar between each other.

This is also true at different scales, meaning that the phenomenon will appear even if we consider larger or smaller patches of pixels.

### An example: PatchMatch

![three.png](three.png)

Here we can see an example on applied self similarity. The purpose of the algorithm is to remove the eagle from the image. It works by letting an user drawing a mask that represent the region where the eagle is, and then replacing each region of the mask with the patch (taken from within the image) that is the most similar to the borders of the mask.

## Translation Invariance

Being invariant with respect to an operator means that the result of the operation doesn’t change if that operator is applied.

If we build a classificator $\mathcal{C}$ that tells us if the image contains a cat or not, the result should be the same if the cat is translated inside the image.

![Screenshot 2023-04-05 at 3.34.50 PM.png](Screenshot_2023-04-05_at_3.34.50_PM.png)

We define the (linear) translation operator $\mathcal{T}$ along a vector $v \in \mathbb{R}^2$ as:

$$
\mathcal{T}_vf(x) = f(x-v)
$$

Where $v$ lives in the same domain of the function $f$, that is, in this case, the function that represent the image. $v$ is just the displacement vector, that translate each pixel to another point in the space.

For $\mathcal{C}$ to be translation-invariant, means that:

$$
\mathcal{C}(\mathcal{T}_vf) = \mathcal{C}(f) \quad \forall f, \mathcal{T}_v
$$

Both the domain and codomain of $\mathcal{T}$ is a function space, because it takes in input a function (the image) and returns another function (the translated image).

We can prove that the operator is linear, since it is homogeneous and additive. 

<aside>
💡 The operator will be still linear with respect to $f$ even if inside $f$ we would have some non-linear complex function instead of $x-v$.

</aside>

### Extra: other types of invariances

Other types of invariances are possible, for example invariance to partiality and isometric deformations. This is useful if we have a 3D morphable model of a dog, and we want to be invariant if the model is morphed in another position. This is an hard problem.

![Screenshot 2023-04-05 at 3.42.04 PM.png](Screenshot_2023-04-05_at_3.42.04_PM.png)

---

We want translation invariance across multiple scale, and in fact we expect local features to be invariant to their location in the image (since they’re local, and so we don’t care where in the image they are).

This means that:

$$
z(\mathcal{T}_vp) = z(p) \quad \forall p, \mathcal{T}_v
$$

Where $p$ are the patches of variable size (local features).

<aside>
💡 Note that CNNs only give us translation invariance, and not rotation invariance, since rotation is not translation.

</aside>

# Convolution

Given two functions $f, g:[-\pi, \pi] \to \mathbb{R}$, their convolution is defined as:

$$
\underbrace{(f \star g)(x)}_\text{feature map} = \int_{-\pi}^\pi f(t)\underbrace{g(x-t)}_\text{filter}dt
$$

![Screenshot 2023-04-05 at 3.49.34 PM.png](Screenshot_2023-04-05_at_3.49.34_PM.png)

<aside>
💡 The convolutional filter $g$ is also called convolutional kernel in the calculus terminology.

</aside>

We can image this operation as taking the function $g$, flipping it to obtain $g(-t)$, and then adding $x$ for each possible $x$, that is equal to sliding the function over the function $f$, and taking the element-wise product between the two.

<aside>
💡 We have $\pi$ in this definition because in case of $f$ and $g$ are signals, we assume that they have a period of $\pi$, but this only in the definition.

</aside>

### Commutativity

Note that convolution is symmetric, meaning that the convolution operator is commutative, so the order of the function doesn’t change the final result.

$$
(f \star g)(x)=\int_{-\pi}^\pi f(t) g(x-t) d t \stackrel{z:=x-t}{=} \int_{-\pi}^\pi f(x-z) g(z) d z=(g \star f)(x)
$$

### Shift-equivariance

Furthermore, convolution is translation-equivariant (or shift-equivariant), meaning that the result doesn't change if we first apply translation, and then convolution or vice-versa:

$$
f\left(x-x_0\right) \star g(x)=(f \star g)\left(x-x_0\right)
$$

<aside>
💡 Watch out that invariance and equivariance are two very different things!
Being invariant from an operator means that the result doesn’t change; being equivariant means that we can invert the order of the operations and the result won’t change.

</aside>

![Shift-equivariance: if I invert the order of the translation-convolution operation the result remains the same](Screenshot_2023-04-05_at_3.58.35_PM.png)

Shift-equivariance: if I invert the order of the translation-convolution operation the result remains the same

This type of equivariance allow us to define in another way convolutions:

> Any linear operator that is shift-equivariant is a convolution
> 

### Linearity

We can see convolution as the application of a linear operator $\mathcal{G}$, and so we can define it as:

$$
\mathcal{G} f(x)=(f \star g)(x)=\int_{-\pi}^\pi f(t) \underbrace{g(x-t)}_{\text {filter }} d t
$$

It’s easy to show that $\mathcal{G}$ is linear:

- **Homogeneity**:

$$
\mathcal{G}(\alpha f(x))=\alpha \int_{-\pi}^\pi f(t) g(x-t) d t=\alpha \mathcal{G} f(x)
$$

- **Additivity**:

$$
\begin{align*}
\mathcal{G}(f+h)(x)= \\ \int_{-\pi}^\pi f(t) g(x-t) d t+\int_{-\pi}^\pi h(t) g(x-t) d t \\=\mathcal{G} f(x)+\mathcal{G} h(x)
\end{align*}
$$

And translation-equivariance can be phrased as:

$$
\mathcal{G}(\mathcal{T}f) = \mathcal{T}(\mathcal{G} f)
$$

# Discrete Convolution

Since we have to implement the convolution operation, we need to change the setting from continuous to discrete. We define the convolution as:

$$
(\mathbf{f} \star \mathbf{g})[n]=\sum_{k=-\infty}^{\infty} \mathbf{f}[k] \mathbf{g}[n-k]
$$

Where $\mathbb{f}$ and $\mathbb{g}$ are two vectors, and $\mathbb{g}$ is the kernel.

## 2D Discrete Convolution

On 2D domains, for example in the case we are working with RGB images, for each channel the convolution is defined as:

$$
(\mathbf{f} \star \mathbf{g})[m, n]=\sum_k \sum_{\ell} \mathbf{f}[k, \ell] \mathbf{g}[m-k, n-\ell]
$$

We can interpret the convolution as a window (kernel) that slides on each discrete point of the image, and computes the summation as a result.

In matrix notation:

Let:

- $\mathbb{F}$  be the input matrix of size $M \times N$.
- $\mathbb{G}$  be the kernel (filter) matrix of size $*K \times L*$.
- $\mathbb{H}$  be the output (convolved) matrix of size $(M−K+1)\times(N−L+1)$.

## Padding and stride

### No padding (no strides)

![no_padding_no_strides.gif](no_padding_no_strides.gif)

In case the image is not padded, meaning no values are added on the border, the convolutional kernel is directly applied on the image, and so the result will be smaller, since the kernel can’t go out of the borders of the image.

### Full zero-padding (no strides)

![full_padding_no_strides.gif](full_padding_no_strides.gif)

In this case the image is padded with zeros in order to compute each single summation, meaning the kernel center point overlaps on each point of the image. This inevitably produces a larger image.

### Arbitrary zero-padding with stride

![padding_strides.gif](padding_strides.gif)

In this case we have just a single “layer” of zero-padding, but we also have a stride of 2, meaning that each time the kernel is moved, we skip one pixel.

---

The dimension of the image after the convolution can be confusing, as it depends on the size of the kernel, the amount of stride and the padding that we choose.

<aside>
💡 Not always zero-padding is the best choice, for example in case of periodic data, we want to pad with the same data in order to replicate it over and over. In this case we will be convoluting over a cilinder. In this case zero-padding would not give good results.

</aside>

# CNN vs MLP

Introducing CNNs, we are replacing the large matrices inside of MLPs with small local filters, that are the convolutional filters.

Since we are solving by the numbers inside the convolutional filters, meaning they are the weight that will change according to the loss function, we have much less parameters compared to the MLP.

<aside>
💡 Because of the fact that the filters change according to the loss function, if the problem is of classifying images that contains eyes to the one that don’t, the filters will probably be very similar to eyes.

This is due also because of the fact that the convolution between the patch and the image is the same as taking the inner product, so if the two matrices are aligned (pointing in the same direction in the space they’re represented, meaning they’re very similar) the inner product will be higher; if they are orthogonal it will be 0; and if they are aligned but with opposite direction, the inner product will be very negative.

So when the kernel, that’s similar to an eye, is convolved on a patch that contains an eye, it will have an high value, and that indicates that that feature is present.

</aside>

Furthermore, the weights of the convolutional kernels are shared, meaning that they’re present only in the filter, and they’re the same when the filter is convolved with different patches of the image.

The number of parameters also doesn’t depend on the input size, differently from an MLP, since the first linear map has to be the size of the input.

![MLP fully connected layer](Screenshot_2023-04-05_at_4.32.00_PM.png)

MLP fully connected layer

In a MLP fully connected layer, we have that each input dimension contributes to each output dimension, and so each ouput dimension has a contribute to each input dimensions. Each edge is a different weight, which represent the matrix that we apply at a certain level.

![Convolutional layer](Screenshot_2023-04-05_at_4.33.18_PM.png)

Convolutional layer

In a convolutional layer there are less weights. In this case the kernel size is $3 \times 3$, and so each input dimension contributes only to $3$ output dimension. The weight are shared, meaning that the three arrow that exits from each dimension are always the same.

So in this case we have 25 parameters for the MLP and only 3 for the CNN.

# Pooling

Since deeper we go into the network, more higher level are the features (meaning they’re closer to the final output), it means that there is some scaling process in the middle.

The scaling process is the pooling operator, which takes non-overlapping patches of the image, and produces another smaller image.

Max pooling for example takes only the max for each patch. This is sensible to noise, since if there is a peak, only the peak will be considered.

Another type of pooling is the average pooling, that returns the average value of the patch.

![Screenshot 2023-04-05 at 4.37.50 PM.png](Screenshot_2023-04-05_at_4.37.50_PM.png)

Pooling allows to capture higher and higher features deeper in the network.

![Screenshot 2023-04-05 at 4.38.24 PM.png](Screenshot_2023-04-05_at_4.38.24_PM.png)

# Regularization

Regularization is a mechanism that reduces overfitting, and so improves generalization.

> Any modification that is intended to reduce the generalization error but not the training error can be considered as regularization.
> 

## Weight Penalties

$$
\underbrace{\ell(\Theta)}_\text{loss} + \lambda\underbrace{\rho(\Theta)}_\text{regularizer}
$$

The idea behind weight penalties is to add a regularizer, that is a function weighted by the factor $\lambda$, that increases the loss when the parameters don’t have certain properties.

$\lambda$ controls the trade-off between data fidelitity (that is the part of the loss that directly involves the data) and the regularization part. (Trade off between data fidelity and model complexity).

### Tikhonov (or Ridge) regularization ($L_2$)

In this case:

$$
\rho(\Theta) = \|\Theta\|_2 = \sum\theta^2
$$

![Each bin represent the amount of parameters having that particular value](Screenshot_2023-04-12_at_4.43.13_PM.png)

Each bin represent the amount of parameters having that particular value

This type of regularization promotes values for $\theta$ that are in the $[-1,1]$ interval, and so promotes the shrinkage of the parameters $\Theta$.

This because all the $\theta$ that are not in that interval, when squared will result in a quadratically larger value, and so the loss will be incremented.

On the other hand, for values between $-1$ and $1$, the value squared will be smaller, and so the loss will be decremented, and the values promoted.

### Lasso regularization ($L_1$)

In this case:

$$
\rho(\Theta) = \|\Theta\|_1 = \sum|\theta|
$$

![Screenshot 2023-04-12 at 4.46.13 PM.png](Screenshot_2023-04-12_at_4.46.13_PM.png)

This type of regularization promotes sparsity, meaning that most of the parameters will be equal to $0$.

This because differently from $L_2$ regularization, all the values will be discouraged in proportion with their value, so both numbers far from zero and near zero.

---

We can also use both $L_1$ and $L_2$ regularization, weighting one more than the other using $\alpha$ and $(1-\alpha)$ factors, in order to control the amount of sparsity in $\Theta$. This goes by the name of *Elastic net* regularization.

In general, we can also bound a type of regularization only to some specific layers.

## Early Stopping

For early stopping we mean stop training the model as soon as the performance on the validation set decreases, meaning when the error goes up again.

### Note on overfitting

Note that the number of parameters and overfitting are not directly correlated. Usually when a polynomial regression model has many parameters, it has the higher change to overfit, but this is not true for MLPs and other models.

Overfitting is a local phenomenon. The model can overfit in some regions of the data, and fit right on other.

![Screenshot 2023-04-12 at 4.59.33 PM.png](Screenshot_2023-04-12_at_4.59.33_PM.png)

### Double Descent (Capacity-wise)

Early stopping can be done in with respect to two dimensions: capacity of the model and training time.

![Screenshot 2023-04-12 at 5.01.07 PM.png](Screenshot_2023-04-12_at_5.01.07_PM.png)

From this plot we can see how is the trend of training and validation data, varying the capacity $\mathcal{H}$ of the model, meaning each time we increase the number of parameters of the model, train it for a fixed number of epochs, and see what is the final validation error.

In order to perform early stopping, we will choose the model that yields the validation error that is in the *sweet spot*. However, if we carry on for a long time, it can happen that the validation error will go down again, in a phenomenon known as *double descent*.

This makes sense since increasing the capacity of the model to a very large value, the model will be always more expressive, and at one point will express perfectly the true unknown function that describes the data.

The surprising fact is that SGD is able to find such good models.

### Double Descent (Epoch-wise)

As said before, early stopping can also happen with respect to training time, meaning that if we train the model long enough, the validation error will go down again.

![Bluer the color, lower the validation error.](Screenshot_2023-04-12_at_5.11.34_PM.png)

Bluer the color, lower the validation error.

# Batch Normalization

Let $\mathbb{x}^{(k)}$ be the output of the $k$-th layer in the network defined as:

$$
\mathbb{x}^{(k)} = \sigma \left(\mathbb{W}^{(k)}\mathbb{x}^{(k-1)}\right)
$$

If you compute the average and the standard deviation of the data points at the layer $k$ and those of the data points at layer $k+1$, these would be different. This is expected since it means that the network is doing something with the data, but researchers said that is not good for the network.

The phenomenon is called internal covariate shift, meaning that the distribution of the data shifts across the layers of the network.

Researchers showed that by re-normalizing $\mathbb{x}^{(k)}$ before passing it to the next layer, the results were better.

This procedure takes the name of *batch normalization.*

Formally:

$$
\hat{\mathbb{x}}^{(k)} = \text{normalize}(\mathbb{x}^{(k)}, \mathcal{X})
$$

where $\mathcal{X}$ is the training set that has reached level $k$ of the network. 

Note that since we are applying the normalization in the forward pass, we must be able to backpropagate through it, and so the $\text{normalize}$ operation has to be differentiable, meaning we have to be able to compute

$$
\frac{\partial}{\partial \mathbb{x}}\text{normalize}(\mathbb{x}^{(k)}, \mathcal{X}),\quad \frac{\partial}{\partial \mathcal{X}}\text{normalize}(\mathbb{x}^{(k)}, \mathcal{X})
$$

The normalization happens in this way:

$$
x_i \mapsto \frac{x_i -\mathbb{E}[x_i]}{\sqrt{\text{var}(x_i)}}
$$

Where the expected value (mean) and variance are computed over the training set. After the transformation, the data points will have mean $0$ and variance $1$.

### Trainable weights

Generally, in a neural network is should be possible that one layer does nothing to the data, meaning it will represent the identity. With batch norm this isn’t possible, since the data is normalized, and so modified.

In order to allows this, we introduce two trainable weights $\gamma$ and $\beta$ in the transformation:

$$
x_i \mapsto \gamma_i\frac{x_i - \mathbb{E}[x_i]}{\sqrt{\text{var}(x_i)}} + \beta_i
$$

In this way the network can learn those weights, and if $\gamma_i$ is equal to the variance and $\beta_i$ is equal to the mean, then the normalization won’t happen, hence the layer represent the identity ($x_i \mapsto x_i$).

<aside>
💡 Note that the parameters are two for each data point. The $\beta$ factor removes the need of the $\mathbb{b}$ bias factor.

</aside>

### Mini-batches

Since now we always normalize the data points with respect to the entire training set. Since most of the time we use SGD with mini-batches, we should be capable to use batch normalization with mini-batches.

We can do that by simply taking each time the mean and variance with respect to the current mini-batch. This also increases the robustness of the network, since normalizing means expressing each datapoint in terms of the other data points in the mini batch. The interaction is each time local to the mini-batch, but since the mini-batch changes each time, each time the data points interact with different other datapoints.

<aside>
💡 Batch normalization leads to more stable gradients, meaning there are less fluctuations and so we can take larger steps (incrementing the learning rate), thus we have a faster training.

</aside>

At test time mini-batches don’t exist anymore, so it’s not clear with respect to who we have to normalize. The solution is to remember and aggregate the means and variances computed during the training step, and use those also in the testing set.

### Batch Norm Variants

Batch normalization performs the normalization across the datapoints. There are variants of the batch norm in which you can normalize the data with respect to other things.

- Layer norm normalizes across the channels of the data.
- Instance Norm normalizes across the dimensions of the data;
- Group Norm is like layer norm but with a subset of the channels.

Normalizing with respect to something means to compute the mean and variance with respect to that something.

Everytime you change what is being normalized, that is a variant of the Batch Normalization. 

![Screenshot 2023-04-16 at 1.48.40 PM.png](Screenshot_2023-04-16_at_1.48.40_PM.png)

# Dropout

<aside>
💡 Ensemble Learning is a technique in which different model are trained, and the final decision is just an aggregation of the decisions made by the single models. Ensemble methods are most of the time always more precise than a decision of a single model. 

However, for deep nets this comes at a high computational cost.

</aside>

The main idea behind dropout is to randomly drop some units in each layer (dropping means to set their value to $0$) and see if the result is better.

![Screenshot 2023-04-16 at 1.54.24 PM.png](Screenshot_2023-04-16_at_1.54.24_PM.png)

Note that this can be seen like an ensemble, because each time dropout is applied, we have a kind of different network, but the crucial part is that the weights are shared.

If there are $n$ nodes, we have $2^n$ possible ways to sample a different network (a network with some nodes dropped out), so exploring all the networks space is too costly.

To simplify, we drop out some nodes only when new training data is presented, for example at each mini-batch. We train the network just for one step, and then we apply dropout again. 

Most of the time dropout is applied just before the non-linearity.

### Testing

During testing, we should be able to average the trained weights from each model in the ensemble. The idea is to consider each weight that exits the node $i$ as $p\mathbb{w}$ where $p$ is the probability that the node has of staying in the network. 

This works because if a node has probability of staying very low, then it was almost never present in the network, and so it’s contribution shouldn’t be considered so much, and so the weights will be decreased.

On the other hand, if $p$ is near the maximum value $1$, the node contribution will be considered more, since it should be more important.

![Screenshot 2023-04-16 at 2.02.54 PM.png](Screenshot_2023-04-16_at_2.02.54_PM.png)

Note that $p$ is different at each layer.

## Properties

Dropout has two key features:

- **Bagging**: each model is trained on random data
- **Weight sharing:** the weights are shared between all the models, that is something that doesn’t happen in ensemble methods and that makes dropout efficient.

Some properties of dropout as a regularizer:

- Reduces co-adaptation (the phenomenon in which small errors in a unit are absorbed by another unit) by making units unreliable (with the $p$ weighting). This improves generalization to unseen data, hence reduces overfitting;
- The middle representation are sparse, meaning that the value after the activation function is sparse.
- Performs almost the same result as averaging all the $2^n$ models (this was proved experimenting).
- The training times are longer, since the parameter updates are noisier. The noise in the data is needed in order to improve generalization and avoid overfitting.

In conclusion, dropout is a simple and efficient way to improve the result of a neural network and reduce the overfitting.

![Screenshot 2023-04-16 at 2.11.17 PM.png](Screenshot_2023-04-16_at_2.11.17_PM.png)

### Monte Carlo Dropout

# Generative Models

The overall idea behind generative models is to learn a distribution from some training samples, in order to generate new samples by sampling from that distribution.

For instance if I sample an image from the space of all possible images in $\mathbb{R}^{320 \times 240}$, most of the time I will get an image that’s only noise. The images that are natural and make sense are way less than the noisy images, and we assume they live in a portion of the entire space, and we are only interested in this subspace (this is the Manifold hypothesis).

Learning a distribution means that natural images will have more probability to be sampled with respect to noisy images that do not make sense in the real world.

![Screenshot 2023-04-19 at 4.12.55 PM.png](Screenshot_2023-04-19_at_4.12.55_PM.png)

# PCA - Principal Component Analysis

As we already know, PCA is a dimensionality reduction technique that aims to represent the data points with the first $k$ principal components, where principal components are ordered by the amount of variance they describe.

In matrix notation we represent the $n$ $d$-dimensional data points with the matrix $\mathbb{X}$, the $d$ $k$-dimensional principal components with the matrix $\mathbb{W}$, and the new $n$ $k$-dimensional points, that are the projection of the original points onto the principal components, with the matrix $\mathbb{Z}$.

$$
\overbrace{\underbrace{\left(\begin{array}{ccc}
- & \mathbf{x}_1^{\top} & - \\ &
\vdots & \\
- & \mathbf{x}_n^{\top} & -
\end{array}\right)}_{n \times d}}^\mathbb{X}

\overbrace{\underbrace{\left(\begin{array}{ccc}
| & & \mid \\
\mathbf{w}_1 & \cdots & \mathbf{w}_k \\
| & & \mid
\end{array}\right)}_{d \times k}}^{\mathbb{W}}

=

\overbrace{\underbrace{\left(\begin{array}{ccc}
- & \mathbf{z}_1^{\top} & - \\ &
\vdots \\
- & \mathbf{z}_n^{\top} & -
\end{array}\right)}_{n \times k}}^{\mathbb{Z}}
$$

Assuming $\mathbb{W}^T\mathbb{W} = \mathbb{I}$, for $k < d$ we have:

- **Projection**: we generate the $\mathbb{Z}$ matrix by projecting the data points onto the principal components.

$$
\underbrace{\mathbb{X}^T\mathbb{W}}_\text{projection} = \mathbb{Z}^T
$$

- **Reconstruction**: starting from the reduced representations $\mathbb{Z}$, we want to obtain the original data points $\mathbb{X}$. Of course we won’t exactly get the same $\mathbb{X}$ since we have lost some information.
    
    $$
    \mathbb{X} \approx \underbrace{\mathbb{W}\mathbb{Z}}_\text{reconstruction}
    $$
    

PCA finds the principal components (rows of $\mathbb{W}$) by maximising the sum of orthogonal projections of the data points, that is the same as maximising the variance.

<aside>
💡 Note that this is fundamentally different from how logistic regression finds the line of best fit, and that the two like won’t be the same most of the time.

With linear regression we measure the error along the $y$ coordinate, with PCA we measure the error orthogonal to the principal direction.

![LR vs PCA.png](LR_vs_PCA.png)

</aside>

## PCA as a generative model

We can use PCA as a generative model by sampling a $\mathbb{z_{\text{new}} \in \mathbb{R}^k}$ (for example we can take the average of two $\mathbb{z_1},\mathbb{z_2} \in \mathbb{R}^k$) and using reconstruction in order to obtain the $\mathbb{x_{\text{new}}}$ associated.

![Screenshot 2023-04-19 at 4.43.19 PM.png](Screenshot_2023-04-19_at_4.43.19_PM.png)

PCA alone is completely linear, since both the projection and reconstruction operations are linear, so in order to generalize this idea and generate more accurate or complex representations, we will replace the projection and reconstruction operations with two (highly non-linear) neural networks.

# Autoencoders

When we generalize the idea, we call the projection and reconstruction procedures respectively *encoding* and *decoding*.

The encoder will be a function (neural net) that takes a data point $\mathbb{x}$ in input and outputs a low-dimensional code $\mathbb{z} \in R^k$ that is the intermediate representation of $x$.

The decoder will take the code $\mathbb{z}$ and return the $\mathbb{x}$ that is the most similar to the one that generated $\mathbb{z}$.

An architecture like this, in which encoder and decoder put together generate an output $\mathbb{x}$ that is the most similar to the input. (If this doesn’t happen, then it’s just an encoder-decoder architecture).

![Screenshot 2023-04-19 at 4.52.19 PM.png](Screenshot_2023-04-19_at_4.52.19_PM.png)

In order to enforce the Autoencoder to learn the encoder and decoder such that it will output a vector that is very similar to the input, we have to enforce it into the loss function:

$$
\underbrace{\ell_\theta = \sum_i\|\mathbb{x}_i - D_\Theta(E_\Theta(\mathbb{x}_i))\|}_\text{reconstruction loss}
$$

The type of norm depends on the data, if we have data that lives in the euclidean space, than we can use the $L_2$ norm.

<aside>
💡 If the layers of the NN are linear, than the codes $\mathbb{z}_i$ span the same space as PCA.

</aside>

### Importance of the bottleneck

The bottleneck in the architecture, meaning the fact that $k < d$ is important in order to avoid trivial solutions.

- If $k = d$, then $\mathbb{z} \in \mathbb{R}^d$ and so we risk that both the encoder and decoder will learn the identity function (meaning that $\mathbb{z} = \mathbb{x}$)
- If $k > d$, then we risk that the encoder and decoder will just create the $\mathbb{z}$ as $\mathbb{x}$ concatenated with as much $0$ needed in order to arrive to the $k$ dimensions.

# Manifold hypothesis

The decoder performs a mapping from a low-dimensional latent space $\mathbb{R}^k$ to an high-dimensional embedding space $\mathbb{R}^d$ of observed data.

The latent space is Euclidean, while the embedding space is curved (not Euclidean).

## Manifolds

A manifold can be seen as a union of charts (atlas).

A chart is a mapping $\phi : \mathbb{R}^k \to \mathcal{S} \sub \mathbb{R}^d$ with $k < d$.

An example of a chart is the mapping that happen when we want to represent the earth on a flat surface.

- The domain of $\phi$ (the space in which the flat surface is) is the parametric space (Euclidean);
- The codomain of $\phi$ (the sphere that represents the earth) is the embedding (not Euclidean).

$\phi$ has to be:

- **Smooth**: if two points are close in the parametric space, then they have to be close also in the embedding. The distance may be different, but the proximity has to be maintained.
Being smooth means to be **continuous** and **differentiable**.
- **Invertible**

A function that is smooth and invertible takes the name of ***diffeomorphism.***

For each manifold, we have infinitely many ways to construct a chart.

Back to the cartography example, we can represent the earth as a map that better maintains the distances, or maybe the areas or the angles. Each time we will have a different chart, but they encode the same exact geometric information.

## Relationship between Manifolds, Autoencoders and PCA

The decoder $D: \mathbb{R}^k \to \mathbb{R}^d$ is a chart that maps the *latent space* spanned by the codes $\mathbb{z}$ to the *data space* of the inputs $\mathbb{x}$.

It’s both differentiable and continuous (smooth) and it’s invertible via the encoder $E$, so it’s in all and for all a chart.

<aside>
💡 Being linear, PCA puts the data on a flat manifold, since the decoder (reconstruction) simply performs a linear combination of the orthogonal vectors.

</aside>

Finding the map $\phi$ is achieved by training an autoencoder.

# Variational Autoencoders (VAE)

When dealing with simple autoencoders, we can have some regions of the space space in which the codes are immersed that have blanks, and so when we sample out of that blank and then decode the result, we won’t obtain an image that is natural. This because there aren’t enough points near that point.

![Screenshot 2023-04-19 at 5.28.03 PM.png](Screenshot_2023-04-19_at_5.28.03_PM.png)

The idea to resolve this problem is to enforce the latent space to be packed within a smaller area, and so to be dense, in order to avoid blanks.

Variational autoencoders are a type of autoencoders that allow to do that, in particular they allow to enforce a distribution in the latent space, meaning that it will produce codes that can be seen as samples from that probability distribution. In other words, if we sample the code from the latent space, then the sampling should respect the probability distribution that we enforced. 

The distribution is chosen a priori, and most of the time it’ll be a Gaussian.

<aside>
💡 There is no proof that we are loosing information by going from autoencoders to variational autoencoders. We are just placing the embeddings in a different way.

</aside>

---

## Entropy

The information carried by an event $\mathbb{x}$ can be quantified as:

$$
I(\mathbb{x}) = -\log p(\mathbb{x})
$$

This means that the less the event is likely to happen (low $p(\mathbb{x})$) the higher the information it carries (high $\log p(\mathbb{x})$). In fact if $p(\mathbb{x})$ is high, its $\log$ will be near $0$, since a very probable event doesn’t carry much information.

Given a probability distribution $p$ on some set of events $\mathbb{x}$, we define its entropy as the probability-weighted average of information:

$$
H(p)= -\sum_\mathbb{x}p(\mathbb{x})\log p(\mathbb{x})
$$

## Kullback-Leibler divergence

Given two distributions $p$ and $q$, we can measure how their dissimilarity in terms of their entropy with the Kullback-Leibler divergence, defined as:

$$
\begin{align*}
KL(p\|q) \approx H(q) - H(p) \\
= - \sum_\mathbb{x}q(\mathbb{x})\log q(\mathbb{x}) + \sum_\mathbb{x}p(\mathbb{x})\log p(\mathbb{x})
\end{align*}
$$

Since this difference of entropies can return a negative distance, the authors of the measure decided to substitute $q$ with $p$ in the first part, and so the final formula is:

$$
\begin{align*}
KL(p\|q) = - \sum_\mathbb{x}p(\mathbb{x})\log q(\mathbb{x}) + \sum_\mathbb{x}p(\mathbb{x})\log p(\mathbb{x}) \\
= -\sum_\mathbb{x}p(\mathbb{x})\log\frac{q(\mathbb{x})}{p(\mathbb{x})}\ge 0
\end{align*}
$$

Which makes the divergence not symmetric. 

---

## Variational inference

In our scenario $\mathbb{x}$ is a given data point and $\mathbb{z}$ is a latent code.

In a variational autoencoder architecture, the encoder take in input a data point and returns the probability distribution of all possible latent codes. 

$$
p_\theta(\mathbb{z}|\mathbb{x}) = \frac{p_\theta(\mathbb{x}|\mathbb{z})p_\theta(\mathbb{z})}{p_\theta(\mathbb{x})} = \frac{p_{\boldsymbol{\theta}} (\mathbf{x}, \mathbf{z})}{p_\theta(\mathbb{x})}
$$

The problem here is that we cannot exactly compute that, because we cannot compute:

$$
p_\theta(\mathbb{x}) = \int p_\theta(\mathbb{x}|\mathbb{z})p_\theta(\mathbb{z})d\mathbb{z}
$$

Since we need to integrate over the entire latent space, which we don’t have. So the problem is intractable.

What we can do is to compute an approximation:

$$
q_{\boldsymbol{\phi}}(\mathbb{z}|\mathbb{x}) \approx p_\theta(\mathbb{z}|\mathbb{x})
$$

where $q_\phi(\mathbb{z}|\mathbb{x})$ is a neural net with weights $\boldsymbol{\phi}$. In order to let the neural net learn the best parameters $\boldsymbol{\phi} ^*$ we have to enforce the fact that we want the two distributions to be as close as possible in the loss function, by minimizing the $KL$ divergence.

 

$$
\begin{align*}
\boldsymbol{\phi}^* = \text{argmin}_{\boldsymbol{\phi}, \boldsymbol{\theta}} KL(q_{\boldsymbol{\phi}}(\mathbb{z}|\mathbb{x}) || p_\theta(\mathbb{z}|\mathbb{x})) \\
\text{after some calculations} \\
=\arg \max _{\boldsymbol{\phi}, \boldsymbol{\theta}} \sum_{\mathbf{z}} q_{\boldsymbol{\phi}}(\mathbf{z} \mid \mathbf{x}) \log \frac{p_{\boldsymbol{\theta}}(\mathbf{x}, \mathbf{z})}{q_{\boldsymbol{\phi}}(\mathbf{z} \mid \mathbf{x})}-\log p_{\boldsymbol{\theta}}(\mathbf{x})
\end{align*}
$$

The $-\log p_{\boldsymbol{\theta}}(\mathbf{x})$ contains the intractable term and so there still is a problem, but this is solvable noticing that, applying at theorem, the right part of the equation is always bigger than the left part, and so the maximisation of only the left part will approximate the maximisation of the whole thing.

The right part takes the name of *Evidence variational Lower BOund* or $ELBO_{\phi, \theta}(\mathbb{x})$.

We are interested in finding:

 

$$
\begin{align*}
\max _{\boldsymbol{\phi}, \boldsymbol{\theta}}  ELBO_{\boldsymbol{\phi}, \boldsymbol{\theta}} \\
= \max _{\boldsymbol{\phi}, \boldsymbol{\theta}} \sum_{\mathbf{z}} q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x}) \log \frac{p_{\boldsymbol{\theta}}(\mathbf{x}, \mathbf{z})}{q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x})} \\
= \max _{\boldsymbol{\phi}, \boldsymbol{\theta}} \sum_{\mathbf{z}} q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x}) \log p_{\boldsymbol{\theta}}(\mathbf{x} | \mathbf{z})+\sum_{\mathbf{z}} q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x}) \log \frac{p_{\boldsymbol{\theta}}(\mathbf{z})}{q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x})} \\
= \max _{\boldsymbol{\phi}, \boldsymbol{\theta}} \underbrace{\mathbb{E}_{q_{\boldsymbol{\phi}}(\mathbf{z} \mid \mathbf{x})} \log p_{\boldsymbol{\theta}}(\mathbf{x} | \mathbf{z})}_{
\text{likelihood of observing } \mathbb{x}  \text{ given } \mathbb{z}
}
\underbrace{-K L\left(q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x}) \| p_{\boldsymbol{\theta}}(\mathbf{z})\right)}_{\text{ensures } q_\phi(\mathbb{z}|\mathbb{x})\approx p_\theta(\mathbb{z})}
\end{align*}
$$

The first part of this equation is simply the reconstruction loss, and we can also substitute it with the loss $\ell_{_\phi, \theta}$ we’ve seen before.

The second term is the $KL$ divergenge, and it’s needed in order to enforce the encoder $q_\phi$ to be the most similar to the true function $p_\theta$, this is the regularizer.

Since we want to maximise that, it’s the same as minimizing the negative, so the loss is just:

$$
\ell_{\phi, \theta} =-\underbrace{\mathbb{E}_{q_{\boldsymbol{\phi}}(\mathbf{z} \mid \mathbf{x})} \log p_{\boldsymbol{\theta}}(\mathbf{x} | \mathbf{z})}_
\text{reconstruction loss}
+\underbrace{K L\left(q_{\boldsymbol{\phi}}(\mathbf{z} | \mathbf{x}) \| p_{\boldsymbol{\theta}}(\mathbf{z})\right)}_\text{regularizer}
$$

Remember that the probability distribution is chosen a priori, so for example we choose $p(\mathbb{z}) = \mathcal N_{\mathbb{0}, \mathbb{I}}(\mathbb{z})$, and so we can forget about the parameters $\theta$, because the probability distribution has no free parameters.

The probabilistic encoder $q_\phi(\mathbb{z}|\mathbb{x})$ also generates a Gaussian distribution (if we choose the Normal distribution) with some mean $\boldsymbol{\mu}$ and a standard variation $\boldsymbol{\sigma}$, different for each data point $\mathbb{x}$ (of course the output changes also according to the neural net parameters $\phi$).

The difference of a probabilistic encoder from a simple encoder is that it outputs the mean and the standard variation, from which we can sample each time a different $\mathbb{z}$, instead of outputting directly the $\mathbb{z}$.

The Gaussian is most of the time the best choice, also because using that the $KL$ term has a closed form.

<aside>
💡 To distinguish VAE from AE, the latter are also called deterministic AE.

</aside>

## Regularizing effect

## Reparametrization trick

# Geometric Deep Learning

Image can seen as functions defined on $\mathbb{R}^2$, and so they represent flat data, since they live on an Euclidean surface. Same thing for audio signals which live on $\mathbb{R}^1$. 

Geometric deep learning applies deep learning techniques on data that lives on non-Eucildean surfaces, meaning curved surfaces. An example of that are graphs and 3D shapes.

3D shapes in particular can be embedded inside of an Euclidean space, but the shape itself is a manifold.

Non-euclidean data is made of two parts:

- Data: that is the actual data that lives on the surface
- Structure: that are the properties of the surface where the data lives.

Structure is not informative for Euclidean domains, since it’s always the same (images live all on the same surface), but can be very informative for geometric data. The structure of a graph can represent the semantic of the connectivities between nodes, which can be for example the “friend” relationship between nodes, in case of a social network graph. Structure is so informative that we can do learning also only on that.

Rarely we an have a geometric surface with only structure and without data, in this case we can extract the data from the structure itself. For example in case of a manifold, the data at a certain point can be the curvature of the manifold in that point.

The structure of the geometric surface can also change over time, and this should or shouldn’t affect our deep learning algorithm. For example we may want a pose classifier for 3D shapes of people, and in this case it should be *pose-variant*. In case of a people recognizer from 3D shapes, we want the model to be *pose-invariant*, since we want to recognize a person regarding of its pose. This is something that is never considered for regular flat data.

## Convolution on Geometric data

We can try to apply convolution on 3D shapes with 3D kernels, just like it happens for euclidean surfaces. This works well until the structure of the shape changes, in this case the result will be completely different. This is called extrinsic convolution.

In order to solve this problem, we can perform an intrinsic convolution, in which the convolutional kernel lives on the shape surface (and not in the embedding space), in order for it to change together with the structure. In this case the convolution will be invariant to that change.

![Screenshot 2023-05-12 at 11.09.41 AM.png](Screenshot_2023-05-12_at_11.09.41_AM.png)

This is a major difference, since If I want to train a classifier with extrinsic convolution, I need to train it with all the possible poses, hence it’s undoable.

<aside>
💡 To perform convolution we need also the data, and not only the structure.

</aside>

In order to have a convolution operator (i.e. any operator that is shift invariant) we have to come up with the notion of shift, that’s not so simple as for euclidean domains. This is not trivial both for surfaces and graphs. (What nodes should be inside the convolution with a certain node. For example every node at distance $k$, of the nodes that have some degree $\alpha$). This is graph learning.

ANSWER TO THIS QUESTION ON THE NOTEBOOKS

## Local ambiguity

If I have two graphs (represented with an adjacency matrix), that are the same graph but permuted, meaning the matrix has a different ordering, I have to be invariant to the permutation. This also doesn’t happen with images, since we are going to apply always the same canonical order (top left first pixel, or something else). Graph isomorphism is an NP-hard problem.

# Self-Attention and Transformers

[Transformers from scratch | peterbloem.nl](https://peterbloem.nl/blog/transformers)

Given a sequence of observations, we may want to predict the next observation in the sequence. This can be the next word in a sentence, or the next pose in a 3D shape sequence. We also may want to classify the entire sequence, for example we want to classify a sequence of a person 3D model as “running” or “standing”. We may also want to translate a sequence of words from a language to another. 

For all this cases, we may want to build a sequence-to-sequence (or seq2seq) model.

In case of text sequence, what we call a *token* can be a single character, a single word or a combination of multiple characters or multiple words.

## Sequence-to-sequence models

A seq2seq model is a model that takes in input a sequence and outputs another sequence, and that works on sequences of different lengths. A fully connected layer is not a seq2seq since it has a fixed input dimension.

A simple seq2seq is a model that applies a MLP to each token in the sequence, and each MLP outputs another token.

### Causal vs. Non-causal layers

We may want to take into account the ordering of the tokens or not. For that reason, we distinguish two different types of layers:

- Causal layer: the output of one token depends only on the tokens before, and so the model cannot look forward to generate the next token.
- Non-Causal layer: the output of one token depends not only on the previous ones, but on the whole sequence.

![Screenshot 2023-05-12 at 1.09.04 PM.png](Screenshot_2023-05-12_at_1.09.04_PM.png)

## Autoregressive modeling

Autoregressive modeling is when you construct seq2seq model that given a sequence of tokens (called *seed* or *context*) predicts the new token. In this case, by construction of the model, we can only have a causal layer, since we cannot look into the future. (This is how GPT works.)

The autoregressive model won’t output a single token, but a probability distribution over tokens, from which we can sample to obtain the final token. Each time the model produces a new larger seed that contains also the output, and produce a new distribution. This goes on until the token generation is stopped.

## Self Attention

We can build a sequence-to-sequence layer by using the concept of *self-attention*.

Let’s consider a simple linear model:

$$
y_i = \sum_jw_{ij}x_j
$$

Where $y$ is the output, $x$ the input and $w$ the weights. Let’s not make the weights $w$ trainable, but let’s compute them with a formula:

$$
w'_{i,j} = x_i^Tx_j
$$

And transform the weights such that they are strictly positive and sum to $1$ ($w_{ij} > 0 \land \sum_jw_{i,j}=1$) by using the softmax function:

$$
w_{i,j} = \frac{e^{w'_{i,j}}}{\sum_je^{w'_{i,j}}}
$$

In matrix notation, $\mathbb{X}$ is the matrix of all the token vectors stacked together.

We can compute the weight matrix by computing the inner product: $\mathbb{W}' = \mathbb{X}^T\mathbb{X}$, and compute $\mathbb{W}$ by applying the softmax to $\mathbb{W}'$ row-wise. We will have that $\mathbb{Y} = \mathbb{WX}^T$.

The matrix $\mathbb{W}$ is diagonally dominant, meaning that the elements on the main diagonal are bigger than the elements that are not on the diagonal (because the inner product is maximised when $i = j$).

Notice that in this layer we are not training the network, since there aren’t any trainable weights. We are just producing the matrix $\mathbb{Y}$. This layer can be an hidden layer in the neural network, or the final layer, and so the inputs can be the result of a trainable layer, meaning that the learning is done on the previous part of the network.

This is useful since we can capture the relationship between words and so the context of the sentence, in order to generate new tokens.

Self-attention is permutation-equivariant, meaning that if we permute the input, the output will be permuted in the same way. In other terms, let $\pi$ be the permutation operator and $\text{sa}$ the self-attention operation: $\pi(\text{sa}(\mathbb{x})) = \text{sa}(\pi(\mathbb{x}))$.

![Screenshot 2023-05-12 at 1.32.59 PM.png](Screenshot_2023-05-12_at_1.32.59_PM.png)

### Make the self-attention layer trainable

We can notice that each input vector appears in the self-attention mechanism $3$ times:

$$
w'_{i,j} = \underbrace{x_i^T}_{\text{query}}\underbrace{x_j}_{\text{key}} \quad \text{and} \quad y_i = \sum_jw_{ij}\underbrace{x_j}_\text{value}
$$

We can introduce some trainable weights $q, k, v$, such that $q = \mathbb{Q}x+b$ where $\mathbb{Q}$ and b are trainable. The same thing happens for the other set of weights $k$ and $v$.

The formulas now are:

$$
w'_{i,j} = q_i^Tk_j \quad \text{and} \quad y_i = \sum_jw_{ij}v_j
$$

### Causal self-attention

Remember that in order to insert self-attention inside an autoregressive model, we only can use causal layers, meaning that we cannot look for tokens that are ahead. We can do that by summing over tokens that are previous in the sentence.

$$
y_i = \sum_{j\le i}w_{ij}v_j
$$

In matrix notation, we want the $\mathbb{W}$ matrix to have all the elements that have $j > i$ masked out (meaning set to $0$). In order to do so, we set to $-\infty$ the elements that have $j > i$ of the $\mathbb{W}'$ matrix, in order for them to be equal to $0$ once we apply the softmax transformation.

## Position Information

Until now we were just considering the ordering of the tokens, but not their exact position. This can be very informative. Permutation equivariant in this case is not desired. In order to let the model consider this, we can use different approaches:

- Position embedding: for each position, the model learns a vector embedding and it sums it to the token embedding.
- Position encoding: passes the vector embedding to a mathematical formula that has some position information. Let $\rho$ be the function, we transform each vector by applying $\rho(\text{embedding})$. (The most used).
- Relative positions: we embed the position that a token has relative to another token instead than its absolute position (not so used).

# Transformers

A transformer is any model that primarily uses the self-attention mechanism. Transformers have many transformers blocks stacked together, each one using the self-attention mechanism.

A transformer is made of encoder-decoder blocks (not autoencoder because it doesn’t have a reconstruction loss and so doesn’t try to reconstruct the input).

The encoder produces a single embedding from the entire sequence, and it’s invariant to the sequence length. The decoder is another transformers that takes in input the embedding and outputs another sequence. Differently from auto-encoders, the decoder takes in input also the input sequence (that is in input to the encoder). The intuition is that the input sequence has precise information about the sequence, and the embedding as general global information about all the sequence. The local and global information together are very useful.

![merged.png](merged.png)

# Generative Adversarial Networks and Adversarial Attacks
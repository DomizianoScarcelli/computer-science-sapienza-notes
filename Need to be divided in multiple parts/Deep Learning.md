>[!TODO]
>This has to be divided in different pages

## The manifold hypothesis (just an intuition…)

Deep learning makes a big assumption, which is that the input data lives on an underlying non-Euclidean structured called a manifold.

In this manifold there are subspaces where the same type of objects exists. For example in a certain subspace there may be only photos of mountains.

---
## Vector lengths

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
# Classification

Classification is the task of predicting a category instead of a value.

In particular, a binary classification function is of the type:

$$
f_\Theta(\mathbb{X}) = \{0,1\}
$$

A possible solution is to use linear regression and then do some post-processing, such as thresholding, in order to convert the real value to a binary label. This is not an optimal solution since the function is optimized for the MSE loss, but once the output is converted, this is not true anymore.

The idea is to modify the loss in order to minimize the error over categorical values directly.
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

> If $\sigma$ is sigmoidal, then for any compact set $\Omega \subset \mathbb{R}^p$, the space spanned by the functions $\phi(x) =  \sigma(\mathbb{Wx} + \mathbb{b})$ is dense in $\mathcal{C}(\Omega)$ for the uniform convergence. Thus, for any continuous function $f$ and any $\epsilon > 0$, there exists $q \in \mathbb{N}$ and weights s.t.:
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

>[!Note]
The convolutional filter $g$ is also called convolutional kernel in the calculus terminology.

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
---
Exam:
  - Deep Learning
  - Fundamentals of Data Science
---
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

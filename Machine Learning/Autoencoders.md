---
Exam:
  - Deep Learning
  - Advanced Machine Learning
---
When we generalize the idea behind the PCA as generative model, we call the projection and reconstruction procedures respectively *encoding* and *decoding*.

The encoder will be a function (neural net) that takes a data point $\mathbb{x}$ in input and outputs a low-dimensional code $\mathbb{z} \in R^k$ that is the intermediate representation of $x$.

The decoder will take the code $\mathbb{z}$ and return the $\mathbb{x}$ that is the most similar to the one that generated $\mathbb{z}$.

An architecture like this, in which encoder and decoder put together generate an output $\mathbb{x}$ that is the most similar to the input. (If this doesn’t happen, then it’s just an encoder-decoder architecture).

![Screenshot 2023-04-19 at 4.52.19 PM.png](Screenshot_2023-04-19_at_4.52.19_PM.jpeg)

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

# Variational Autoencoders (VAE)

When dealing with simple autoencoders, we can have some regions of the space space in which the codes are immersed that have blanks, and so when we sample out of that blank and then decode the result, we won’t obtain an image that is natural. This because there aren’t enough points near that point.

![Screenshot 2023-04-19 at 5.28.03 PM.png](Screenshot_2023-04-19_at_5.28.03_PM.jpeg)

The idea to resolve this problem is to enforce the latent space to be packed within a smaller area, and so to be dense, in order to avoid blanks.

Variational autoencoders are a type of autoencoders that allow to do that, in particular they allow to enforce a distribution in the latent space, meaning that it will produce codes that can be seen as samples from that probability distribution. In other words, if we sample the code from the latent space, then the sampling should respect the probability distribution that we enforced. 

The distribution is chosen a priori, and most of the time it’ll be a Gaussian.

<aside>
💡 There is no proof that we are loosing information by going from autoencoders to variational autoencoders. We are just placing the embeddings in a different way.

</aside>
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
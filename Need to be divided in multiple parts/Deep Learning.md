>[!TODO]
>This has to be divided in different pages
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
---
Exam:
  - Deep Learning
  - Advanced Machine Learning
---
The overall idea behind generative models is to learn a distribution from some training samples, in order to generate new samples by sampling from that distribution.

For instance if I sample an image from the space of all possible images in $\mathbb{R}^{320 \times 240}$, most of the time I will get an image that’s only noise. The images that are natural and make sense are way less than the noisy images, and we assume they live in a portion of the entire space, and we are only interested in this subspace (this is the Manifold hypothesis).

Learning a distribution means that natural images will have more probability to be sampled with respect to noisy images that do not make sense in the real world.

![Screenshot 2023-04-19 at 4.12.55 PM.png](Screenshot_2023-04-19_at_4.12.55_PM.jpeg)
Examples of generative models are:
- [[PCA - Principal Component Analysis]]
- [[Autoencoders]]
- [[Autoencoders#Variational Autoencoders (VAE)|Variational Autoencoders]]
- [[Generative Adversarial Networks]]
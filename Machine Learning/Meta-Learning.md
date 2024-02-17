---
Exam:
  - Advanced Machine Learning
---
Meta-Learning is the branch of machine learning that focuses to learn how a model learns. It studies one-shot learning, few-shot learning, [[Hyperparameter tuning and Transfer Learning|transfer learning]] etc.

Few-shot learning, meaning learning something with very few data, is done using prior knowledge (just like human do).

The problem that meta-training solves is the following:

Let’s suppose we want to design a learning algorithm A that outputs good parameters $\theta$ of a model $M$ when we feed a small dataset $D_\text{train}$. With meta-learning (learning to learn), we mean that we can learn that algorithm A end-to-end. $A$ is called the meta-leraner, which learns the learner $M$.

We achieve this by first meta-training the model to learn the algorithm $A$, and then meta-testing it to see how the learning algorithm actually performs.

During the meta-training there are some episodes of train and test, where the model is shown some images in the training phase, and some other images in the testing phase, which are the images that it should recognize.

![Screenshot 2024-01-29 at 7.06.29 PM.png](Screenshot_2024-01-29_at_7.06.29_PM.png)

The same process is done in the meta-testing phase, where again there is a train and test phase inside, in order to test the learned algorithm $A$.

Applications of few-shot learning are something like: show an example made of few seconds of a song with some genre, and the model will be able to recognize for other songs if it's the same genre or not. Same thing with a photo, where the model may be able to learn the presence of a certain person with just few photos of them.
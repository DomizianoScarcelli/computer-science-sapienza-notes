---
Exam:
  - Advanced Machine Learning
---
When we search object and people we are searching a specific person or object. In semantic search we search for a generic concept, such as “any person with a blue hat”. You do that by giving a query image that contains the concept, and all the other images will be similar in terms of their semantic.

![Screenshot 2024-01-17 at 1.25.56 PM.png](Screenshot_2024-01-17_at_1.25.56_PM.jpeg)

>[!Note]
In a siamese network you have n times the same network with the same parameters. This is used in the deep local features, together with a ranking loss.

>[!Note]
Curriculum learning means start the training easy and increment the difficulty of the train with time. For example use more aggressive data augmentation, such as increased cut-out.
Is the semantic search task well-defined? Meaning that if we consider the query image below, what do we want as result? A person with an umbrella, or a person near the metal net?

![Screenshot 2024-01-17 at 1.28.43 PM.png](Screenshot_2024-01-17_at_1.28.43_PM.jpeg)

One may be closer to the other one depending on the interpretation, so the task is ambiguous. Experiments has been done on this, and the agreement score was about 90%, meaning that 10% of the people don’t agree, which means the task is a bit ambiguous.

During some experiments they also saw that if the image is provided with some human captions, the performance are better. By just matching the captions of the images with tf-idf produced a score of 76.3%, which is far from the 89% agreement achieved by humans, but it’s a score that cannot be reached with only the visual baseline, also by using some deep NN.

The idea is to create captions for the training set, and force two images to be close in the semantic embedding space if they have a similar caption. Then at test time you will only have images, but the embedding of an image should be closer to the ones that are semantically similar now.

![Screenshot 2024-01-17 at 1.41.51 PM.png](Screenshot_2024-01-17_at_1.41.51_PM.jpeg)

The training is done using the query, the relevant image and a non relevant image (in order to push it away in a contrastive learning fashion). The triplet loss depends on three factors, which tries to minimize the similarity between the query and the relevant image (relevant in terms of captions similarity), and maximise the similarity between the query and the non-relevant image.

In general in complex deep learning problems you should make sure that the model is able to perform some proxy tasks which means that it has understood what we think it’s important to understand in a scene. Done that, the model will be able to learn other more specific tasks to take actions and solve the specific problem.

An example is autonomous driving, if we try to directly create a model that outputs the steering and acceleration, without producing some kind of embedding of the scene which represents what the model understands in that specific moment, we won’t probably have really good results.
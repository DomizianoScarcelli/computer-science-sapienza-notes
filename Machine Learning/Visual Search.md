---
Exam:
  - Advanced Machine Learning
---
Visual Search means training a model in order for it to be able to, given a new unseen dataset of images and a new unseen query image, find other images that are relevant to the query.

![Screenshot 2024-01-11 at 9.01.11 PM.png](Screenshot_2024-01-11_at_9.01.11_PM.png)

Now let’s say we have a dataset of monuments, we can tackle this problem with a simple classification. The model will be able to learn which monuments are which, and then when provided with an unseen image of a monument will be able to classify it. 

As you can see Visual Search and Classification are two very different problems. Visual search is a one-shot understanding. Generally classification achieves better performance, but the model needs to see the class of images it will classify in the training set. Visual Search is when this class of images is not available in the training set.

An example of Visual Search are Reverse Image Search on Google, or more generally a web search engine.

Another great application is Geolocalization, where the model can output the coordinates given a certain photo. A good idea is also to use this indoor, since there is no GPS signal.

A major problem with visual search is the inherent ambiguity due to the fact that the user only inputs a single query. Two images may be very similar, but maybe they are not related at all.

In order to solve this problem we need to inject prior information, which will depend on the application.

When developing a visual search model, you should consider:

- The measure similarity
- How to represent the image or the video
- Define the search procedure
- What is the background knowledge (prior) and what can be learned.

---
Exam:
  - Advanced Machine Learning
---
Early approaches for object search was to use some global low-level features such as color histograms, texture and shape descriptors to find the same object between multiple image. Of course this method is not strong at all, since those descriptors are very rigid.

The main problem with object search is the different variations that an object can be subject to. Variations can be occlusion, different viewpoints and illumination and a different scale. All things that make the object less recognizable.

![Screenshot 2024-01-13 at 10.33.07 AM.png](Screenshot_2024-01-13_at_10.33.07_AM.png)

While global representation may be not suited for the problem, local representations have been state of the art for a long time before the advent of deep learning. The most famous local representation is the [[SIFT Descriptor]].
## Evaluating Object Search

Oxford dataset is one of the dataset on which one can evaluate object search. It contains 5K images with different monuments. The metric is the mean Average Precision (mAP). (A benchmark is defined as data + metric of evaluation).

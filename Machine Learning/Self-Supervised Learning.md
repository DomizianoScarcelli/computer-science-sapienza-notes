---
Exam:
  - Advanced Machine Learning
---
Supervised learning is the standard approach in deep learning, and it consists in leveraging information from labels which determine the ground truth data, on which the model will be able to learn.

The problem with annotated data is that it’s limited and expensive to produce. The more the progresses in the field of deep learning, the more data we need, and most of the time it’s impossible to manually label all the data that a huge model needs (see the LLMs).

Supervised learning also suffers from *supervision collapse,* which is the phenomenon that happens when a model is given some data specific for a certain tasks, which results in the model performing very well on that task, but requiring fine-tuning for any other different task. A similar phenomenon can happen also if the model is trained with a certain distribution, which causes it to perform badly on all other different distributions.

## Self-supervised Learning

Self-supervision is a technique in which it’s possible to obtain the labels without actually manually annotating them. Such a technique will unlock an almost unlimited amount of data.

The main idea of self-supervising learning is to produce automatically some labels which allow the model to learn a very generic task, called the *pretext task.* For this task a huge dataset with no labels is used. Then the knowledge is transferred to learn a more specific task, using a smaller dataset with few labels. 

The *pretext task* needs to be very simple to achieve, and designing an adeguate task is a fundamental part for the self-supervised learning. An example of task is to rotate an image and let the model reconstruct the original image, meaning it has to predict the rotation degree that modified the image. The intuition behind this particular task is that the model can recognize the correct rotation only if it has learned how the object should look without rotation. Because of that, the model is able to learn information about the content of the image, in particular it learns the rotation invariance: the semantic meaning of image doesn't change if we rotate it.

Another example of *pretext task* is to divide the image in patches with the same size, give the model just a few patches, and make it learn the patches relative positions, meaning the model has to output the position of a patch, given another patch in input.

Colorization (give RGB values from a grayscale image) and Inpainting (let the model reconstruct a missing part of the image, and use the ground truth missing part to compute the loss) are other kind of valid *pretext tasks*.

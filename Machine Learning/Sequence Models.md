---
Exam:
  - Advanced Machine Learning
  - Deep Learning
---
The *Vanilla* neural networks that we’ve seen until now work on static data. They can be classified as one-to-one models, since given that piece of static data they output another single piece of static data, such as an image (in the case of generative networks) a string or a number (in the case of classification or regression).

Sequence models are a different type of model which can get in input a sequence of data points, and output another sequence of data points. This is fundamental to solve a large class of problems, where the data is sequential, such as video, audio and text.

In particular, there are three types of sequence models:

![Screenshot 2023-12-08 at 12.04.19 PM.png](Screenshot_2023-12-08_at_12.04.19_PM.png)

- One-to-many: an example of this is a captioning model, which takes in input an image of something and outputs a text that describes the photo. Note that the sentence in output is as long as needed (it doesn’t have a size fixed a priori)
- Many-to-one: an example of this is action classification model, which takes in input a video (sequence of frames) and outputs an action class, such as running, jumping, dancing.
- Many-to-many: here we have three different kind of models.
    - **Real-time**: the output is given as soon as the input is provided. An example of this is video classification at frame level (classify the objects at each frame);
    - **Online:** the output is given with the data that is currently available, even if it’s not immediate. An example of this is machine translation, which takes a sequence of words in input and outputs another sequence of words in another language.
    - **Offline**: in order to compute the output, the model needs the whole data and a certain amount of time to give the answer. An example of this is video captioning, where from a sequence of video frames the model outputs a caption. Forecasting may be another example.

>[!Disclaimer]
Examples may be wrong, take them with a grain of salt.

Sequential processing is useful when generating sequential data, since you can generate one piece at the time.
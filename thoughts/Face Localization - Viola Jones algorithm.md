Note: you can see a better and clearer explanation in [[Q&A for Oral Exam (in Italian)]].

[Link to the official paper](https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf)

This algorithm is different from the one seen before since it doesn’t explicitly look for particular face features like eyes or mouth, but it’s more a global approach that can found a specific set of features in an image.

The algorithm needs a classifier. This is initially traines with two kind of examples:

- **Positive examples**: these are the instances of the object that has to be identified. For example if model needs to identify the mouth, the classifier is trained with a lot of images centered on the mouth or cropped over it. This examples make the classifier understand what are the elements that are required in order to identify the object.
- **Negative examples**: these are the examples that do not contain the object that has to be identified, but can cause an error. The amount of negative examples should be similar as the positive one. The idea is to stress the system with images that can provoke an error.

The training part of the classifier is essential to extract certain features from the examples, in order for the model to know which are the most relevant elements to look for into an image in order to detect a face, and which are the most discriminating ones.

In a classifier we can identify two kinds of error, that can be both decreased by retraining the model adding new examples, positive or negative:

- **Misses**: when an object is present but it's not detected;
- **False alarms**: when an object is detected but it’s not present.

This errors can be detected only if we have a ground truth. Furthermore, if the model reports to have found all the faces, we cannot be sure that it’s correct, since some detected faces could be a false alarm and some other real faces could be missed.

Viola-Jones algorithm uses the [[AdaBoost]] approach for the binary face classifier.

The classifier is based on the following ideas:

- Integral images for feature evaluation: feature evaluation mean to evaluate if a feature is present or not, for every sub-region of the image. Integral images (aka summed-area table) are used over simple images in order to improve the performances.
- Multiscale detection: we repeat the overall process with different crops of the image in different scale and position (achieved using a search sliding window), in order to be able to detect the object in all its scales.

The method is very cleaver since it follows a hierarchical order for feature evaluation, meaning that if the classifier doesn’t find the first feature in the current window, it immediately discard the window without completing the process.
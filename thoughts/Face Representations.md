In the feature extraction part of a recognizer, we should be able to obtain the less complex representation as possible, in order to perform better in terms of computation and space requirements.
## Face representations

There are many ways to create a model that can represent a face.

The most intuitive one is to represent the face as a two-dimensional image, modelled by a matrix that contains the pixels of the image.

It’s also possible to concatenate the rows in the image to represent the image as a vector of pixels.

A good way to represent an image is by associating a vector element for each feature that is extracted from the raw image. In this case we’ll obtain a multi-dimensional space that’s called Feature Space.

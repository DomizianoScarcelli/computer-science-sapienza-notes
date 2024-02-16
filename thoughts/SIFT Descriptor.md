The SIFT descriptor takes some key points of the images, like corners and angles, and describes them with a 128 dimensional vector.

Local descriptors are better than global since they are robust to illumination, and occlusion (there will be some point that is not occluded). They also are very discriminative, since two local features will be the same also in different viewpoints for the same object, but different for two different objects.

SIFT was proposed in 1988, and was state of the art since 2015 (even after CNN were introduced).

Let’s see the SIFT pipeline:

1. You extract some key-points like corners and angles from a source image;
2. You describe each key-point with SIFT;
3. You do the same processing with another image you want to compare;
4. You compare the points between images. Using geometric verification (RANSAC method) you can remove some non useful SIFT points. We do geometric verification since objects are rigid.
5. The remaining points are called *inliers*, which are those points that are consistent with an estimated translation or rotation of the object. The more *inliers* there are, the more is likely to be the same object.

This works pretty well, the only problem is that is very slow, since you have to do that for each image in the dataset.

### Global Descriptors

Global descriptors are more efficient (even if as we’ve seen before it’s difficult to find a good global descriptor that works well). Global descriptors are way faster since instead of having $N \times N$ comparison of keypoints for each image in the dataset, I just have $1$, since the global descriptor describes with a vector the whole image.

SIFT always outperforms global descriptors. The best between the global descriptors is Bag of Features. Bag of Features computes local descriptors such as SIFT and then represent an image using an histogram of occurrences of local features. They are efficient but not accurate.
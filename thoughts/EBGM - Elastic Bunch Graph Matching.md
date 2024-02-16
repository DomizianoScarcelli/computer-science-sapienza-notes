Source: [Elastic Bunch Graph Matching - Scholarpedia](http://www.scholarpedia.org/article/Elastic_Bunch_Graph_Matching)

EBGM is a method that allows to [[Face Representations |represent faces]] in a particular way in order to then compare them.

The face is represented as a labeled graph. The nodes of this graph represent the local textures based on Gabor wavelets, and the edges represent the distance between the node locations on the image.

The idea is that a graph for a face in a certain pose can match all the other faces in the same pose. The graph that models the features for any object in the class (for example the same pose for the face) is called a bunch graph.

For this reason, the EBGM model can be applied only to objects with a common structure, for example faces in a certain pose, that share a set of landmarks, or fiducial points, that can be points such as the tip of the nose, the corners of the mouth, the pupils and so on.
### Gabor jets

Since the gabor wavelet transform returns a value for each wavalet at all locations of the image, it returns about 80 (40 real + 40 imaginary) values at a single pixel location. The set of these values is called a *jet*. A jet contains information of different frequencies and orientations.

A jet can be used as a representation of a local texture. Many jets can be combined in order to represent the whole image. Jets are used as nodes in the image graph.

Two graphs $G^I$ and $G^M$ with the same structure can then be compared by using a similarity function.

### Bunch Graphs

Bunch Graphs solve the problem of finding a new graph that fits well to an image $I$ in an efficient way, instead of brute-forcing many different graphs.

Bunch graphs solve this problem by establishing a way to create a single graph that can model all the objects in a certain class, for example a face in a certain pose. Since different faces in the same pose has similar structure, it’s not hard to find the landmarks.

Bunch graphs differs from simple image graphs because the nodes are not the single jet of the image, but a set of jets representing many images with the same structure. The edges are the average distances of the set of images instead of the concrete distance from just one image.

It’s possible to compare a new image graph with the bunch graph by picking the best fitting jet at each node. This operation applied to each node returns a similarity score.

### Practical example for EBGM for face recognition

Suppose we have 1000 images of faces in the same pose. The process for recognition will be performed as following:

1. Manually build the face graph for the first image, manually detecting the face landmarks.
2. We can construct now the bunch graph. The first face graph can be seen as a bunch graph with just one image in it, we can fit it to another image but if they’re not so similar the match would be of poor quality. It’s possible to manually tweak the graph in order for the match to be better, and add that computed graph to the bunch graph. This is done for a set of images, for example the first 100 images.
3. Since we have the bunch graph for the first 100 images, it’s possible to process the remaining 900 images automatically.
4. Assuming a new probe comes in, it’s possible to construct the face graph for this image just as done for each of the other images in the point 3.
5. The probe image graph is compared with all the model graphs, resultin in 1000 similarity values. The candidate with the highest similarity above a certain threshold is considered as valid.
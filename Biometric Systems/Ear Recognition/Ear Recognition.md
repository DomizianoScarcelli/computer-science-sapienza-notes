A human ear has a well define structure. Compared to the face, the ear has some advantages:

- Less details, so it can require lower resolution;
- More uniform color distribution;
- Very low expression variations.

Being a 3D structure, it’s still sensible to illumination and pose variations.

Ear recognition for now is only used in some niche use cases like crime scenes.

It has been dimonstrated by Iannarelli that it's possible to build an extremely discriminative feature vector by just taking a certain number of landmakrs on the ear and measuring the distances. The accuracy gets higher if we’re able to capture the ear in a perfect condition.

Iannarelli also classified the ear into round, retangle, triangle and oval.

Since the ear is a small area and its colour is similar to the sorrounding skin, the localization could be hard sometimes. 

Another problem with ear is occlusion, since the ear can be covered by objects like hair most of the time.

The localization of point of interest can use Neural Networks. Since Neural Network training time is proportional to the image size, we can resize the image to a lower resolution because we’re not interesetd in details in this phase. 

## Ear localization

Ear localization is more complex than face localization, since the skin tone of the ear is the same as the sorrounding skin.

These are three possible approaches for ear localization:

- Localization of points of interest
- General object detection
- Geometric 3D methods

### Localization of points of interest

Uses a neural network approach in order to find the points of interest of an ear. The NN need a large dataset with the specified points of interest in order to be trained. The image resolution is lowered in order to improve the time for the training. 

Once we have the points of interest, it’s possible to extract the rectangle that localize the ear.

### General object detection

It’s possible to use Haar classifiers with AdaBoost to detect ears. 

### Geometric 3D models

This is the most complicated but surely the most accurate approach. 

Training is performed off-line: we start from a photo of the profile face, and the points of maximum curvature are identified, then the image is converted into a binary image and then the region corresponding to the ear is manually extracted. Those extracted regions for each ear are fused togheter in order to create a template, that will be used in the online testing phase.

In that phase, the image is converted into binary image, the poins of maximum and minimum curvature are identified, and the regions that corresponds to the template are searched.

## Ear recognition methods

In the following paragraph we will talk about the different methods to perform ear recognition.

### Iannarelli system

This approach considers the whole ear, represented by a 2D image. The recognition is performed in the following way:

1. The ROI is extracted and normalized
2. The *crus of helix* (”radice dell’elice” in Italian) is put as the origin of the measurement system
3. 12 different measurements are performed
4. The feature vector includes the gender, the ethnicity and the 12 measures

If the central point identification is incorrect, then all the measures are wrong and the method performs badly.

### Voronoi diagrams

A vonoroi diagram is a partitioning of a plane into regions, in which every region (vonoroi cell) embeds the information about the closeness to the seed points.

The problem of the exact point identification in Iannarelli system is solved in this technique, that operates in the following way:

1. Edges are detected in the ROI with the Canny edge detector
2. A voronoi diagram is built from the ROI; A Vonori diagram is just a partitioning of the surface in different Vonoroi cells, which describes how much every point in that cell is distant from a “seed” point. 
3. Since pose and illumination would lower the performances, a Voronoi neighborhood graph of the curve is built, that changes a little in case of pose and illumination variations.

### Force fields

In this method, each pixel in the image is treated as a Gaussian attractor, meaning that it acts upon all the other pixels proportional to its intensity (0-255) and inversely proportional to the square of the distance.

For each pixel the force that all the other pixels apply on it is computed, with its module, direction and orientation.

Then a series of points that make an ellipse are drawn around the ears, and from each point we draw a path that follows the force field. The lines converge into various points on the ear that are called sinks.

These sinks can be considered as unique identifiers of a particular ear, which can then be compared with the one of other ears in order to have a measure of similarity. 

### Interest points

The image is convolved with various Gabor filters, and the relative Gabor jets are extracted from the points of interest. This jets will be the nodes of the “ear graph”. 

PCA is used in order to obtain a “eigenear graph”. The matching with a probe is made extracting the ear graph from the image, projecting it into the sub-space to obtain the eigenear graph and then comparing it with the graphs in the gallery. 

## Improvements

In order to have more information about the ear, it’s possible to capture it with differents sensors, such as a thermogram or a sensor that can embed 3D information.

It’s also possible to align the ear to achieve better results during the comparison.

## Combining face and ear

Some experiments were made in order to evaluate the performances of the multibiometric approach with face and ear. It has been seen that the face alone it's always better than the ear alone, but the best process is to perform face and ear recognition in parallel and fuse the result. 

This is even better than doing first face and then ear, or vice versa, in a way that if the first one fails then the second one isn’t done.

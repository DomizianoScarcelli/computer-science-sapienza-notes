# Object Detection

While segmentation is about classifying each pixel in an image, object detection is about detecting multiple instances of multiple object in an image, giving them a category and putting a bounding box around them.

Detection is hard because the objects can be small or occluded. Before deep learning the performances of the various algorithms were always kind of bad (around 40% of Mean Average Precision), while with the advent of Deep Learning the performances spiked out to 80%.

Object detection with just a fixed number of objects in an image can be seen as a Classification + Localization problem, meaning we have to classify the objects in the image but also find the coordinates of the bounding box.

We can treat the localization problem as a regression problem, meaning we can use the L2 loss for the bounding box coordinates, and then optimize the sum of the classification (optimized using cross entropy loss) and localization loss.

![Screenshot 2024-01-30 at 1.26.55 PM.png](Screenshot_2024-01-30_at_1.26.55_PM.png)

Because it’s a multi task loss, we need to insert a scaling factor in order to give one loss more importance over the other. This scaling factor is an hyperparameter.

This works for a single object detection, but what about multiple objects in the same image?

>[!Note]
 This approach can be used also for pose estimation, where an image is input into a CNN and a set of $14$ coordinates, each for each joint, is used to compute $14$ different $L2$ losses, which weighted average is then use to backpropagate.
## Multiple Objects Detection

When we’re dealing with multiple objects in the same image we have some issues, since we are expecting a different number of outputs for each image with the same model, in particular one bounding box and one classification for each object in the image, which number is unknown before the detection, and for this reason we cannot apply the methods described above.

To solve this problem we can crop a random part of the image and apply a CNN to see if an object can be detected. We repeat this for each possible crop.

This is way too inefficient since the number of possible patches are a lot, and since we are not reusing the information we have already computed, for example if the two patches are overlapping.

## Region Proposal

A solution to this problem is to run a lightweight algorithm on the image before the detection, which purpose is to output a set of proposed regions, meaning patches which may include an object. Then we can run the CNN only on those patches.

One kind of region proposal algorithm is Selective Search, which is able to propose 2K regions in a few seconds running on a CPU.

The detection model can not only tell if there is an object in the region or not, but since we are doing regression on the bounding box coordinates it can also move the bounding box in order to better localize the object.

### Selective Search

When we’re building a region proposal algorithm, we don't care about high precision (if the model propose a region, than it’s highly probable that there is an object inside), otherwise we wouldn’t need a detection CNN at all. What we’re interested in is an high recall (there is a low probability that a non proposed region contains an object), since if an object is not contained by at least one proposed region, the detection CNN will never detect that.

Since images are intrinsically hierarchical, detection at a single scale is not enough. Because of this, selective search works in the following way:

1. The image is over-segmented
2. We compute similarity measure between all adjacent region pairs $a$ and $b$ as 
    
    $$
    S(a, b)=\alpha S_{size}(a, b)+\beta S_{\text {color }}(a, b)
    
    $$
    
    Where 
    
    $$
    S_{size}(a, b) = a - \frac{size(a) + size(b)}{size(image)}
    $$
    
    This encourages small regions to merge early. Furthermore, we have
    
    $$
    S_{color}(a,b) = \sum_{k=1}^n \min(a^ k, b^ k)
    $$
    
    where $a^ k$ and $b^ k$ are color histograms, which encourage regions with similar colour to merge.
    
3. Merge two most similar regions based on the similarity measure $S$
4. Go back to step 1 until the whole image is a single region.
5. Take the bounding boxes of all generated regions and treat them as possible object locations.
    
    ![Screenshot 2024-01-09 at 11.23.40 AM.png](Screenshot_2024-01-09_at_11.23.40_AM.png)
    
    ![Screenshot 2024-01-09 at 11.23.46 AM.png](Screenshot_2024-01-09_at_11.23.46_AM.png)
    

The number $K$ of region to propose is an hyperparameter that has to compromise efficiency with recall (and F1 score in general). I'm happy if the proposed region has an Intersection over Union of at least 0.5 with the ground truth bounding box. Recall is then computed as the proportion of objects that has $IoU \ge 0.5$.
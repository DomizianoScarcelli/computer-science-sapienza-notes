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
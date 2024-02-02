### Global methods

These methods are based on the whole appereance of the face. An example are PCA, LDA and some Neural Networks.

The advantages of these methods are that:

- They do not destroy any of the information about the iamge by concentrating only on a limited area;
- Several of these methods are been modified in order to compensate for PIE variations.

The disadvantages are:

- Most of the basic implementation of these models weight all the areas of the image the same;
- Considering the whole image may be computationally expensive.
- The training and testing set have to be highly correlated.

### Local methods

Differently from global methods, local methods only consider some significant areas of the image. An example are LBP and EBGM.

The advantages are:

- Some methods can be tolerant to PIE variations;
- The representation of the face is compact and the matching is fast;

The disadvantages are:

- The choice of which features are the most important has always to be made;
- If the features are not discriminant enough, then the method performs poorly.

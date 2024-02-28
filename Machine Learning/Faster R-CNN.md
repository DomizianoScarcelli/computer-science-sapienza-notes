---
Exam:
  - Advanced Machine Learning
---
If we analyze the time spent by the region proposal algorithm and the time spent by the [[R-CNN]], we see that in the [[Fast R-CNN]], most of the time is spent finding region to propose.

![Screenshot 2024-01-09 at 12.16.52 PM.png](Screenshot_2024-01-09_at_12.16.52_PM.jpeg)

A solution to make the region proposal phase faster is to insert a Region Proposal Network (RPN) inside of the CNN which takes in input the whole image and outputs a set of rectangular object proposals, each one with an objectness score. This is the Faster R-CNN model.

![Screenshot 2024-01-09 at 12.18.18 PM.png](Screenshot_2024-01-09_at_12.18.18_PM.jpeg)

In order to do that, for each pixel I consider an anchor box, which is a bounding box of size $n \times n$ in which the pixel is in the center. For each of these anchor boxes, I compute their objectness score, which is the likelihood of the anchor box containing an object. 

In order to capture objects at different scales and at different aspect ratio, for each pixel we use $3$ different scales and $3$ different aspect ratio ($1:1$, $2:1$, $1:2$), using in total a combination of $9$ anchor boxes.

This means that if the image is of size $W \times  H$, then there will be a total of $9 \cdot H \cdot W$ anchor boxes.

For boxes that contains the object, the model also uses regression in order to predict a box that better contains the object, using the ground truth box.

After having identifies the regions, the model sort them by objectness score and only take the top $N$ as the proposals.

The major advantage of using this method is the fact that the anchor box is modelled as a sliding window, and because of that the parameters are always shared.

We train the Faster R-CNN using a mixture of 4 losses:

- RPN Classification (Object or Not Object)
- RPN Regress box coordinates (4 points for each anchor box)
- Final classification score (Object class)
- Final box coordinates
    
    ![Screenshot 2024-01-09 at 1.12.01 PM.png](Screenshot_2024-01-09_at_1.12.01_PM.jpeg)
    
---
Exam:
  - Advanced Machine Learning
---
Mask R-CNN is a [[Faster R-CNN]] with the addition of a Mask prediction in order to perform Instance Segmentation, meaning segmenting the different instances of all the different objects in the image (3 dogs, 3 different masks). This is done adding a single small mask network that operates on each ROI and predicts a binary mask.

Since we have $C$ classes, we actually predict $C$ masks, one for each class, at each step.

![Screenshot 2024-01-09 at 2.16.00 PM.png](Screenshot_2024-01-09_at_2.16.00_PM.jpeg)

Mask R-CNN works very well at instance segmentation. Cluttered scenes, small objects and occluded are still problematic for most of the detectors.

We can also use Mask R-CNN to do pose estimation.
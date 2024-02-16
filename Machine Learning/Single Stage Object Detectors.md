---
Exam:
  - Advanced Machine Learning
---
Faster R-CNN is a Two-stage object detector, meaning that it first find region proposal and then uses those to detect the objects. 

The fist stage runs once per image and detects the region proposals. The second stage runs once per region and performs the actual detection.

One-stage detectors like YOLO or SSD just do a single pass to detect the objects.

There are also Hybrid detectors such as R-FCN.

### YOLO - You Only Look Once

YOLO modifies the Faster R-CNN Region Proposal Network in order for it to also predict the category of the object that is detected.

For each anchor box, it regress over $5$ values ($4$ values for the bounding box coordinates and $1$ value for the confidence that there is an object inside), and it also predicts a score for the $C$-way multi classification.

Since it doesn’t run the algorithm again on each region proposal, this approach is even faster than the Faster R-CNN.

While YOLO is faster, it has a worst accuracy due to imbalance that the classification at the fist stage introduces.

This is because when we deal with classification using the entire image, we will fine that a lot of bounding anchor boxes will be negative, while only a few will be positive.

On the other hand, in the second stage we perform classification only on the proposed region, which by definition are almost all positive. 

This imbalance makes YOLO make more localization errors.
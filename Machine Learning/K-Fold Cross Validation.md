---
Exam:
  - Biometric Systems
  - Deep Learning
---
In K Fold cross validation, the samples are divided into $k$ subsets all of the same size. One subset is used as the test set, and the other $k-1$ are used for training. The process is repeted $k$ times in order for all the sets to be part once in the testing set.

The error estimation is calculated with an average over all $k$ iterations to get the total effectiveness of the model, reducing bias and variance. 

Usually we choose $k=5$ or $k=10$. 
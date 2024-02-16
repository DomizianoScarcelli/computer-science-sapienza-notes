---
Exam:
  - Biometric Systems
---
When we do offline performance evaluation, meaning the application has not been deployed into the real world yet, we have a static dataset, that entails the ground truth. 

That means that all the sample (the dataset most of the time is composed by samples) are labeled with their real identities. (In the real world that’s never possible, since we don't know whether the system made a mistake in recognition or not).

During the performance evaluation, we have to make some choices in how to distribute the samples from the dataset. Below are listed the three main choices we have to make.

### First Choice: Divide the dataset between training and testing (TR vs TS)

In this scenario, the samples are divided into training and testing, and the overlap is not allowed, meaning it cannot exists a sample that’s bot in TR and TS.

The main difference between training data and testing data is that training data is the subset of the original data that is used to train the machine learning model, whereas testing data is used to check the accuracy of the model.

It’s possible to make two kinds of splits:

- By samples, meaning that all the identities are present in both the training and testing set;
- By subject, meaning that some identities are present in the testing set, but not in the training set. This assures greater generalization, since the system is able to perform well on faces it’s never seen.

N.B. The inverse case of partition by subject (ID1 in TR and not in TS) do not garantee a better generalization.

In principle, it's useful to use 70% of samples for training and 30% for testing. We should also partition the dataset in different ways, repeat the evaluation and take the average performance, in order to avoid the results specific to a certain partition, for example with methods like K-Fold cross validation.

### Second Choice: Divide the dataset in probe set and gallery set (P vs G)

Here as before, overlapping of samples between the two sets is not allowed.

According to the type of samples that we put in the gallery, the performance of the model can change. Here are suggested two main choices:

- Use the best quality samples for the gallery, since often in the enrolling phase the individual sample is captured in controlled condition, and the probe we submit in the real world would be of worse quality and conditions.
- Use very different samples from the same identity for the gallery, in order to be able to recognize the subject in multiple conditions (glasses, beard, expression etc.).

The division between probe set and gallery set is often used for testing.

### Third choice: Use open set or closed set

We talked about the differences between open and closed set, so here we just have to make the decision to what type of set our system will implement.
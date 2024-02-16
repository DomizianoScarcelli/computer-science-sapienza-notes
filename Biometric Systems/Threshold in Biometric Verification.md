---
Exam:
  - Biometric Systems
---
In verification, the subject that presents the probe and the claim is accepted only if the similarity between the probe and the template in the gallery is higher than a certain set threshold. (The opposite if we’re using distances).

In identification, the threshold separates the “good templates” from the “bad templates”.

In general, a threshold is a value between 0 and 1 that tells when a certain similarity is enough.

A good threshold can only be chosen after a good performance evaluation, in which a different value for the threshold is chosen every iteration in order to see how the system behaves.

Of course, a threshold of 0 and 1 is not useful since a similarity of 1 (or a distance of 0) is impossible in real scenarios.

Biometric identification needs some flexibility. During the choosing of the acceptance threshold, there are also some downsides, so the designer has to find a balanced compromise. Remember that the most important value to consider is the error rate.

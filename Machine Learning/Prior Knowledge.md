---
Exam:
  - Deep Learning
---
The prior knowledge is the knowledge that is known a priori, before the learning. This can make the data representation and the model construction easier.

Some forms of prior knowledge is:

- Data distribution
- Energy function
- Constraints (for example if the data is defined in a certain range)
- Invariances
- Input-output examples: this is called data prior. The data is a prior knowledge and sometimes is the only prior knowledge we have.
### Reliability of the prior and fairness

The data provided by human can be highly biased. For example the AI that’s responsible to assign a score to each resume that a certain popular company receives can be biased and assign scores that are not based on the actual potential of the person, but may be on the gender or the ethnicity. This means that the model is not *fair*.

Sometimes is the observation that is biased. For example if a certain zone of the earth is monitored for crimes more than other, it can seem like in that area more crimes are commited, when in fact it’s just monitored more and so more crimes are detected, but it doesn’t mean that they happen more frequently. In this case, the data is not reliable. 
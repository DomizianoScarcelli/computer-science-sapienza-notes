---
Exam:
  - Biometric Systems
---
The Doodington zoo is a way of describing different classes of users that may affect the reliability of a single operation of recognition.

The classes of users are defined as following:

- **Sheep**: a person who belongs in the Sheep class produces biometric samples that matches well to themselves and poorly to those of other people. This is the only good class since a Sheep will achieve more Genuine Acceptance and less False Acceptance when claiming a false identity;
- **Goats**: a person belonging to the Goats class produces biometric samples that match poorly with the other samples of themselves. Goats are used to obtain higher False Rejections since they’re not well recognized.
- **Lambs**: a person belonging to the Lambs class can be easily impersonated, meaning that samples of other people match well with a sample of a person in the Lamb class. This results in higher False Matches. An example of Lambs are children.
- **Wolves**: a person who belongs to the Wolves class is good at impersonating other people, meaning that their samples match well with other. This results in higher False Acceptance when the Wolf claims a false identity.

These classes are defined based on genuine or impostor scores’ average. If we consider both kind of errors, we can increase the number of classes. 

- **Chameleons**: people in this class always appear similar to others. They differ from Wolves since they match well with themselves but also with others. This means that Chameleons receive high scores for all verifications, resulting in very low False Rejects but also high False Acceptance.
- **Phantoms**: people in this class always have a low match with anyone, either samples from themselves or from other people. This results in high False Rejections and low False Accepts. The cause of a person being in this class may be poor biometric traits that leads to difficulties in feature extraction.
- **Doves**: people in this class have samples that match very well with themselves and very poorly with those of others. This means that Doves are almost always recognizable and hard to recognize wrong, resulting in high Genuine Acceptance and low False Rejection. The cause may be the uncommon characteristics of the person, such as a very distinctive nose.
- **Worms**: people in this class are the worst individuals for the system, since they have low matches with samples of themselves and high matches with samples of other people. This results in high False Acceptance and high False Rejections.
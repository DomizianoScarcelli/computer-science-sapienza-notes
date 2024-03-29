---
Exam:
  - Biometric Systems
---
- **Verification** (True or False): the user provides a **sample** and a **claim**. The claim is the affirmation that the user makes saying they’re who they’re trying to be identified to. The comparison between the sample and the stored template is 1 to 1, meaning that the system checks if the user is who they claim to be and validates them in case of affirmation, reject them otherwise. A claim can also be implicit, an example is a biometric authentication used in a smartphone. Since the smartphone is always used by the same user, the system assumes that the user that’s trying to be identified is the same user that enrolled.

- **Identification** (Returns the person identified): the user provides only a sample. The system tries to match the sample to the stored templates, so the comparison is 1 to N. The system returns the person identified or an error in case the person is not enrolled in the system. There could be an error where the system identifies the person (enrolled or not) with another person enrolled in the system.
	
- **Re-Identification**: It cannot identify a person. It gets in inputs many footages where a person may be, and is able to recognize that the same person appears multiple times in the footage. One of its many uses is to track an individual through many videos taken in different places, times, and angles. The person in a certain frame A is the same person in a frame B.

- **Continuous Identification** (Identification + Re-Identification): It’s the same as Re-Identification, but also identifies the person. It allows to confirm that inside all the frames where the person is, that person is always the same.
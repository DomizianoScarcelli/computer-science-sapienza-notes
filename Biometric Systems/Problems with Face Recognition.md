---
Exam:
  - Biometric Systems
---
It’s useful to know which are the main problems that occur during face recognition, in order to came up with techniques that can solve them.

The most traditional problems are those related to PIE, specifically A-PIE (Age, Pose, Illumination and Expression).

Other problems are intra-personal variations, meaning that templates of the same person can be identified as different people; and inter-personal variations, meaning two different people may be identified as the same person.

Other problems may be caused by some kind of disguises, for example make up, plastic surgery, objects that cover the face and so on. 

Some of those problems can be solved by using a 3D model of the face for recognition, instead of a 2D photo. For example variations like pose, illumination and makeup do not affect the 3D model, but this is still not tolerant to variation like expression, age and object covering the face.

Expression can be tolerated by using a morphable model, that is a 3D model of a face that can distorted in order to reproduce any kind of expression. This obviously increases the compuational complexity by a lot.
---
Exam:
  - Biometric Systems
---
Local Binary Patterns (LBP) is a simple yet very efficient texture operator that can be used in various fields such as image and video analysis, object recognition, and facial recognition. It works by comparing the intensity values of pixels in a neighborhood around a central pixel, and encoding the result as a binary pattern.

Here's how it works:

1. The LBP operator compares the intensity values of a central pixel with the intensity values of its surrounding pixels. Usually the neighborhoos has size $3 \times 3$. 
2. If the intensity value of a surrounding pixel is greater than or equal to the intensity value of the central pixel, it is assigned a value of 1. If the intensity value of a surrounding pixel is less than the intensity value of the central pixel, it is assigned a value of 0.
3. This process is repeated for all surrounding pixels, and the resulting binary values are concatenated to form a binary pattern.
4. This value of 8 bits is the converted to a decimal number, and the process is repeated for each pixel in the image.

![Screenshot 2023-01-25 at 1.08.08 PM.png](Screenshot_2023-01-25_at_1.08.08_PM.jpeg)

The good thing about this operator is that is invariant to illumination, since if a certain zone is more illuminated, all the neighbor pixels have an higher value. On the other hand, it’s sensible to pose and image rotation variations.

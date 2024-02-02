A face recognizer works by following these steps:
1. Image capture: the photo that contains the face is captured.
2. Image enhancement: the image is enhanced with some techniques like sharpening, blur elimination and contrast increase.
3. Detection and Localization: detection is used to receive a feedback wether the face is present or not in the image. Localization is instead used in order to receive the exact position of the face in the image. Localization is important in order to crop the region of interest. This has to be independent with respect to the position of the face in the image, we cannot assume the face is always in the middle.
4. ROI crop: once the image is localized, the recognizer crops the ROI (Region of Interest) in order to work with a smaller image that contains all the information needed. Sometimes this process can go on for sub-patches of the face, for example in case the illumination is not even.
5. Feature extraction and template construction: the features are extracted from the ROI and the template is constructed.

An individual can obscure their face with makeup and other objects in order to avoid face detection and localization, this is Adversarial Fashion.
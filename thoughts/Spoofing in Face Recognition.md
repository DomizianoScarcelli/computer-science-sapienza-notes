A spoofing attack is a situation in which a person imitates another person in order to fool the biometric system, and guardantee some access.

### Spoofing vs Camouflaging
- **Spoofing**: the impostor is trying to be recognized as another person that’s authorized in the system. Is trying to enter as an individual inside a white list.
- **Camouflaging**: the impostor is trying to not be recognized as themselves.

--- 

In order to successfully carry out a presentation attack, it’s needed to know which are the biometric traits used by the system in order to authenticate the user.

A biometric system can be attacked in different points, by injecting the data into one of the many sub-modules in order to force the result that we want. The attacks to the other modules, like database, comparator or feature extractor are indirect attacks.

On the other hand, a presention attack (or direct attack) is an attack to the main sensor.

Spoofing attacks are dependent on the biometric trait used by the system. In case of face recognition, there are basically two types of presentation attack:

- 2D spoofs: the attack is carried out by using a 2D surface like a photo or a pre-recorded video of another person.
- 3D spoofs: the attack is carried out by using a 3D model of another person’s face, such as a mask.

For each type of attack, there are several anti-spoofing techniques that are mostly based on lvieness detection. 

There are different types of techniques:

- Sensor-level techniques (Hardware based): This class of techniques exploits the properties of a living body, such as the reflectance of the light on the face, the involuntary signals of a living body, such as the eye movements and blinking.
- Challenge response strategy: we ask to the person that’s presenting the probe to make a certain expression or movement. If this doesn’t happen, we can conclude that’s a spoofing attack.
- Feature Extractor level (Software based): can be static of dynamic:
    - Static: we study the microtexture of the acquired image;
    - Dynamic: we study the dynamic features that a certain movement can produce when it’s natural.

We can have a score level fusion, where we carry out the anti-spoofing in advance and proceed with the recognition only if the anti-spoofing returns a genuine response.

## Photo attack

Photo or Print attack is a low effort attack since the attacker just needs to print a photo of the biometric trait of the user. This type of attack can be easily avoided by analizing the texture, the movement and some special features from the shape of the biometric trait.

The main technique to avoid this attack is called Liveness Detection, that allows to separate live faces and photographs. This can be done since a face is a 3D object represented in a 2D plane, wether a photo is just a 2D object.

In order to estimate depth information the 3D object has to move in the 2D plane. It’s possible to compute the optical flow on the video in order to obtain the information about liveness. The optical flow is a technique that tries to extract the motion vector by comparing the position of the pixels in each frame. This technique is vulnerable.

Another technique is to ask the user to say a phrase out loud and map the sound to the lip movement.

### Eyeblink detection

Another tecnique is eyeblink detection. Even though eyeblink can vary with fatigue, emotions, stress, sleep and so on, the spontaneous blink rate of a human is in average oen every 2 to 4 seconds. The avera blink lasts for about 250 milliseconds.

The eyeblink behaviour can be modeled in various ways, one of which is the Conditional Random Field.

An eyeblink activity can be represented as a sequence $S$ made of $T$ images:

$S = \{I_i, i=1,..,T\}$.

The eyes stat are opening, closing and ambiguos. The ambiguous state is when the eyes is transitioning from open to close and vice versa. We can describe the states with a set $Q = \{\alpha:\text{open}, \gamma:\text{close}, \beta:\text{ambiguous} \}$.

The blink activity can be described as a state change pattern like $\alpha \rightarrow \beta \rightarrow \gamma \rightarrow \beta \rightarrow \alpha$.

Let $Y$ be the label that has to be predictd for every image in $S$. Every element $y_i\in Y$ is a state in $Q$.

Let $G = (V,E)$ be a graph and $Y$ is indexed by the vertices of $G$, then $(Y,S)$ is called a Conditional Random Field (CRF).

This allows to predict a the next label of the sequence. Meaning we can compute the probability of finding a certain state in the next image, giving that we have already observed a certain sequence.

### Micro-texture analysis

This technique is useful in case of a photo attack, since paper has a micro-texture that isn’t visible by eyes but can be detected using some texture features.

The human face, being a 3D object, reflects lingh in different ways, whereas a 2D object doesn’t. The ink pigment also affetcs the way the light is reflecet, with respect to the natural pigments in the skin.

**Multi-scale LBP approach**

This approach uses the multi-scale local binary patterns (LBP), meaning that LBP is performed with windows of different sizes. This is a micro-texture analysis operator.

The feature vectors that are obtained from the different LBPs at different scales are concatenated, and the final feature vector ca1n be fed to a SVM classifier that determines if the face is fake or not. The SVM is previously trained with the same type of histograms.

### **Captured-Recaptured approach**

This approach exploits the fact that when the face of a person is captured by a camera, it suffers from some distortions. These distorsions happen twice if a photo of a photo is taken.

A recaptured face image has less sharpeness compared to the first capture, and so it contains less high frequency components. It's possible to find all the most constrated regions of the images by doing a Difference of Gaussian filtering.

We then compute the LBP codes and the LBP histograms in order to find the LBP variance, that is a measure of how much LBP changes along the surface. 

The LBP between the probe and the gallery images are then compared with a distance metrics like chi-square. 

### **Gaze Stability**

The idea behind this approach is that the spacial and temporal coordination of the eye, head and hand movements involved when a certain action is required by the system is different in case of spoofing attack than in a genuine presentation.

This approach is robust to mask and photograph attacks.

In particular, the collinearity features are computed by the mean square error between the expected position of the landmark points, given the stimuli, and the detected ones.

## Video attack

Video is similar to photo attack, but with a video playing on another screen. The screen inside another screen causes an overlay of two pixel patterns. This effect is called moiré pattern aliasing, and it's detectable with Multi-scale LBP and DSFIT. 

## Mask attack

A mask attack is done by making a 3D model of the original biometric trait. The techniques that exploited the difference between a 2D and 3D object are no longer useful.

The idea in order to detect a fake face is by analyzing the reflectance charateristic, since a sintetic material like plastic or silicon reflects differenly with respect to natural skin.

This technique has a downside. In order to detect a fake face, the material has to be studied in advance in order to get the reflextive characteristics. This means that if a new material comes in, there is the risk of not detecting it as a fake material.

Another technique is to apply the micro-texture analysis separately on color images and depth maps.

Another approach is the photoplethysmogram, that is a measurement that can capture the micro volumetric changes of the skin produced by the blood flow. This technique obviously needs advance video capture equipment and advanced processing. 

---

In general, spoofing can be avoided by just asking the user to interact with the system, by for example making a movement in a random time, in order to avoid pre-recorded movements.

## Anti-spoofing for moving faces

The most robust spoofing detection systems are the ones that perform recognition of the face in 3D, and require an interaction with the user.

Since the 3D face recognition requires ad-hoc sensors, a lot of computational power and very sophisticated techniques, it’s possible to get the 3D information of a 2D face that moves during time. Since we’re dealing with 2D images, the computational power needed is less.

Different from the eye-blink detection, where the user has to remain still and look in the camera, with this technique the user can move the head freely. The idea is to take some points of the face as reference points, and exploit the 3D information as the points moves in the 3D space.
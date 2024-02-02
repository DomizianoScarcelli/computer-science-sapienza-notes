The iris consists in a flat layer of muscle fibers that surround the pupil, and reculates how much the pupil dilatates, thereby regulating the amount of light that enters the eyes.

Is a higly randotypic trait, meaning that is not affected by genuine inheritance, such as fingerprints. 

### Iris advantages

The **advantages** of iris recognition are that the iris is an area where it’s difficult to create damage, and is less prone to occlusion.

The factor that provide a very high level of discrimination are:

- Iris colour
- Iris texture
- Irregular patterns

The level of discrimination are comparable to fingerprints. The right iris is different from the left one, and even two identical twins have different irises.

The iris is also time invariant, after the 2 years of age.

### Iris problems

Iris recognition also has some disadvantages:

- The area is very small, and so an high resolution sensor is needed in order to capture an useful sample;
- The reflection that the light has on the iris may alter the capture. The reflection could also be caused by the presence of contact-lenses or glasses;
- The texture of a very dark iris could not be visible at the requested distance, if a simple camera (and not infrared) is used.
- The person should be looking in the same direction otherwise the iris would be different, in order to solve this problem we can use some tricks like the “off-axis-problem”.

## Iris capture

Since the surface is very small, we need an high resolution capture device at a distance usually less than one meter.

The two main capture modalities are the one in **visible** light and the one in **infrared** light.

- Visible light
- Infrared light

## Processing phases

[Source](https://arxiv.org/pdf/1111.5135.pdf)

The first part is acquisition or capture, then we have:

- **Segmentation**: in this phase we want to get rid of reflection and isolate the actual iris region from the other parts of the eye such as the pupil and eyelashes. This is done using an edge detector like canny edge. Techniques like hough trasnform are used in order to detect the eyelids.
- **Normalization**: in this phase a geometric normalization scheme is applied in order to transform the segmented iris image from cartesian coordinates to polar coordinates. This is also called iris unwrapping.
This process has thre advantages:
    - It accounts for variation of pupil size due to external illumination that might have influenced iris size;
    - It ensures that different irises are mapped onto a common image, despite of the pupul size;
- **Encoding**: in this phase, we use some feature extraction technique like LBP only on the iris part, since we don’t want to encode the other useless parts.
- **Matching**: the difference is computed between two iris econding and the user is accepted or rejected based on that distance.

## Segmentation

Iris segmentation for identification systems requires four main steps, that are:

1. Preprocessing
2. Pupil localization
3. Linearization
4. Limbus localization

If the quality of the capture is bad these phases are not trivial. The details of the scelare vessels, the skin pores and the eyelashes also can interfere with the segmentation process.

### Preprocessing

Posterization can be useful as a preprocessing operation in order to find edges more accurately and it consists in replacing all the pixels in a certain areas with the pixel with the most occurrences. This is done for every subcell in the image.

### Pupil localization

Edge detection is performed with the canny edge detection with different thresholds. Here different elliptic shapes are found, and we need to find the one that best fits the real position of the pupil.

Sometimes the pupil is the darker region of the image. When the conditions are less controlled, the pupil can have some light reflections that can alter its appereance. The dark boundary can also be difficult to find for very dark irises.

The circle that fits the pupil the most is gotten by assigning a score to each circle, according to homogeneity and separability and getting the one with the highest score.

### Linearization

The current image is transofmed from cartesian coordiantes to polar coordinates, where the center is the center of the pupil. This is done in order to better find the boudnary line between the iris and the sclera.

### Limbus localization

The limbus is the part on the border of the iris. Once found that, it’s possible to get the iris section, and remove from it the pupil section.

This can be found exploiting the fact that the pupil occupies the lowest part of the image, and then the limbus ir present before entering the iris and sclera zones.

## Daugman algorithm

Daugman algorithm is the first and most famous algorithm for iris recognition.

The iris image has to be aquired with an infrared sensor in strictly controlled conditions.

The algorithm uses a kind of circular edge detector in order to locate the pupil and the iris.

It also carries out eyelids localization, that is used on the iris and pupil part in order to remove the not necessary eyelids parts. It uses an operator that looks for arches.

### Rubber Sheet Model

The rubber sheet model it’s a kind of normalization procedure that solves the problem of the pupil that is not centered within the iris and has different dilation. This is a problem in the normalization phase.

The idea is to take a fixed number of points on each radius that is contained beween the pupil boundary and the iris boundary. When we have a larger region, the sampling will be less dense, otherwise it will be more dense in case of a narrower region.

Doing this, all the iris will be unwrapped as the pupil was perfectly centered within the pupil, and so the different irises can be compared between each other.

The difference from the Linearization process seen before is that the rubber sheet model applies the transformation only on the iris part. (I think this is true but I'm not sure)

### Feature Extraction

The features are then extracted by applying Gabor filters to the normalized image. The extracted features are called “iris code”. 

### Iris Comparison

We can compare two iris codes we can use the Hamming distance defined as:

$$
HD = \frac{1}{N}\sum_{j=1}^NA_j \oplus B_j
$$

Where $N$ is the toal number of values in the rectangle and $\oplus$ is the XOR.

In this way we’re assuming that every point we're comparing belongs to the iris in both images. This isn’t true in case we have different masks, in that case we define the Hamming Distance as:

$$
HD = \frac{||(\text{codeA} \oplus \text{codeB})\cap \text{maskA} \cap \text{maskB}||}{||\text{maskA} \cap \text{maskB}||}
$$

## Other methods for iris matching

### LBP - Local Binary Patterns

It’s possible to use LBP to extract features from the normalized iris. It’s better to divide the image in horizontal bands than in vertical bands. It’s also possible to divide it in blocks.

Once we have the histograms and the similarity function $\delta$, we can compute the similarities between the codes:

$$
\frac{1}{n}\sum^n_{i=1}\delta(H_i, K_i)(1-\frac{\text{noise}_i}{\text{totpixel}})
$$

Where $n$ is the total number of bands, and $H$ and $K$ are repectively the bands of the template and the probe.

### Blobs

Another possibility for iris feature extraction and matching is by looking at blobs, that are particular regions of the iris. It’s possible to use the laplacian of the gaussian normalized image at different scales, and then fuse the different scales into a single image with a segmentation mask. The matching happens with the hamming distance. 

A variation includes not to fuse the different scales but to chain them, and then match them by getting the average of the hamming distance between the probe and the template.

### LBP-BLOB

LBP-Blob is a technique in which the two different methods are fused, and it’s been proven to work generally better than the single methods alone.

The codings are chains, and the matching is given by the average of the results output by the matchings.

## Noisy Iris Challenge Evaluation - NICE

In order to know which were the best methods for iris preprocessing and recognition, a challenge was raised, called NICE, that consisted in two phases:

- Phase 1: evaluate iris segmentation and noise detection techniques;
- Phase 2: evaluatie iris encoding and matching strategies

### About the dataset

For the challenge the UBIRIS database was used, that contained highly degraded iris samples captured with a visible light sensor.

 The captured were made in two different sessions, each lasting two weeks and separated by an interval of one week. From one session to another the distance from the camera, the acquisition device and the light source were changed. 60% of the volunteers partecipated in both sessions, while the rest only in one of them.

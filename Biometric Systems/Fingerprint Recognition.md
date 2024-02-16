---
Exam:
  - Biometric Systems
---
In 1893 the Home Ministry Office of the UK recognized that no pair of exactly equal fingerprints exists, so that could be a part of the body that could identify an individual.

### Macro-singularities - First Level Features

Sir Francis Galton was an English polymath and anthropologist who was the first to define the three basic fingerprint types. He classified them depending on the number of deltas:

- Whorls (2 deltas)
- Loop (1 delta)
- Arches (no delta)

These are called macro-singularities or “first-level features” and they’re used to compare fingerprints.

An importan point for the fingerprint is the core, that is the central point of the fingerprint. It’s easily individuable in case the fingerprint has a whorl or a loop. In case of an arch it may be not so trivial.

### *Minutiae: Micro-singularities* - Second Level Features

He also introduces the concept of minutia, which consented to creating the first system of classification of fingerprints. 

The *minutiae* in the fingerprints are where the fingerprints line stops or forks.

These features are called micro-singularities or also “second-level features”.

The number of minutiae found in a pair of fingerprints it’s compared and used as a distance measure.

### Third level features

With a robust and high-resolution sensor, it’s possible to study the pores along the ridges. These are called third-level features.

---

Every level of features is useful to divide a set of fingerprints into more specific categories, to ignore as soon as possible the most different couples of fingerprints from the comparison.

In the case of identical twins, the minutiae details are different, but the general attributes are similar, like the number of minutiae, width, separation, and depth of the ridges.

The maximum difference between fingerprints is among different races, even if it’s impossible to determine the race starting from the fingerprint.

We can write a ranking that goes from most different to most similar:

1. People of different races
2. People of the same race but without any kinship
3. Father/Mother and son/daughter
4. Siblings
5. Twins

## Fingerprint Acquisition

There are two basic models of fingerprint capturing:

- **Offline**: the finger is passed on an ink pad and the print is left on a piece of white paper. The digitalization of the print is done afterward through an optical scanner or a high-resolution camera.
This is not an optimal solution since both the ink and the paper can alter the fingerprint and add some noise.
- **Live scan**: the digital image of the fingerprint is acquired directly by holding the fingertip onto a special sensor. Usually the used sensor are pressure-based.
Even in this case we still have some noise, but in a lower quantity.

### Latent fingeprints

Latent fingerprints are those left on some material like glass, most of the time without the subject being aware. They're are used in crime scenes and other similar scenarios where the person is not collaborative.

The acquisition is done with special powders and special techniques that allow to transfer the fingerprint from the surface onto a special paper, in order for them to be digitalized afterward.

### Comparison between different acquisition sensors

- **Optical scanner**:
    
    They use a camera to capture the fingeprint.
    
    - **Pros**: inexpensive and can tolerate some degree of temperature fluctuations;
    - **Cons**: the plate must be big enough for the finger, and can leave some noise caused from the surface residuals of the previous scans. The coating can also wear with age, reducing accuracy.
- **Capacitive scanner**:
    
    They use a capacitive scanner that measures the electical capacity of the finger in order to capture the fingerprint.
    
    - **Pros**: it has a smaller size, so it's cheaper than optical scanner, and can be integrated into devices like smartphones.
    - **Cons**: silicon’s durability has yet to be proven and it’s not certain to be better than optical’s. Since the sensor is smaller, the enrolment and verification have to be done carefully.
- **Thermal scanner**:
    
    They capture the fingerprint by measuring the change in temperature between the fingertip and the sensor.
    
    - **Pros**: it’s tolerant to any temperature and impossible to spoof with an artificial fingeprint.
    - **Cons**: the image disappears quickly, because of reaching the thermal equilibrium between the sensor and the fingertip.

## Matching techniques

There are different approaches when we want to match two fingerprints, those approaches can be classified in three main classes:

- **Correlation based**: in case we’re working with fingerprint images, we can overlap the two images and then compute the correlation between the pixels. There is a problem with allignment, which have to be changed at every iteration to find the optimal one. This is not the best solution since it’s also very sensitive to non-linear transformations, for example when the finger is shifted during the capture, and the algorithm has an high complexity also because of the allignment;
- **Ridge features based:** since it's not always possible to extract information about minutiae from images unless they're very high quality, this method relies on features such as ridges orientation, shape, texture and local frequency. They're easier to extract but less discriminative.
- **Minutiae based**: the minutiae are extracted from the two fingerprints that need to be compared and stored as points in a two dimensional space. Then we search the allignment that maximise the numbers of corresponding pairs of minutiae. It’s also possible to measure the relationship between the minutiae, in order to see similar patters.
- **Hybrid approach**: other methods uses both ridge, minutiae and other information about the fingerprint in order to extract the features. An example is tessellating the fingerprint and then extracting features with a bank of gabor filters.

### Main problems in fingerprint matching

The main problems are in finger matching are:

- The fingerprint may be not centered on the sensor and so it could be captured only in part. In this case the matching has to be made between the common parts;
- Bad skin condition can result in a poor quality capture;
- Different pression on the sensor between different fingers can affect the template;
- Distorsion because of the skin or movement;

## Feature extraction

The steps for fingerprint feature extraction are the followings:

1. Acquire fingerprint image
2. Segmentation
3. Compute directional map
4. Determine fingerprint shape
5. Compute density map
6. Compute singularities, ridge patterns and minutiae

### Segmentation

Segmentation in this case indicates the separation between the foreground fingerprint, meaning the striped pattern, from the rest of the finger. The fingerprint pattern is anisotropic, meaning that its properties changes with orientation.

### Directional map

A directional map is a matrix, in which each element $(i,j)$ denotes the average orientation of the tangent to the ridge points in the neighborhood of the point.

### Density map

A density map is a matrix in which each element denotes the density of the ridge lines in each region of the fingertip.

### Frequency map

The frequency of a local ridge line $f_{xy}$ at the point $(x,y)$ is defined as the number of ridges per unit length along a segment centered at $(x,y)$ and orthogonal to the orientation of the local ridge.

It’s possible to compute a frequency map by computing this value for each discrete region (group of pixels) in the image.

### Poincaré index (singularity detection)

We can then find the singularities based on the directional map using the Poincaré index.

The fingerprint can be modelled by a curve that’s immersed in the directional map, that is a vector field. For each point $p$, we can define the poincaré index as the sum of the orientation of the points in the neighborhood of $p$.

For closed curves, is show that the Poincaré index assumes only one of the discrete vaues 0, ±180, ±360 degrees. It’s possible then to classify the curve:

$$
P(i,j) = 
\begin{cases}
0^\circ && \text{if (i,j) does not belong to any singular region} \\
360^\circ && \text{if (i,j) belongs to a whorl type singular region} \\
180^\circ && \text{if (i,j) belongs to a loop type singular region} \\
-180^\circ && \text{if (i,j) belongs to a delta type singular region} \\
\end{cases}
$$

### Minutiae Extraction

In general the minutiae extraction phase starts with the binarization procedure, meaning the gray scale image is converted into a binary image; and then there is a thinning procedure, where every ridge that’s thicker than 1 pixel is thinned into 1 pixel.

<aside>
💡 Note that some authors proposed methods that work directly on the gray scale image, because a significant amount of information could be lost during binarization, and both binarization and thinning are time consuming. Furthermore the thinning procedure may introduce a number of fake minutiae. Both the procedure also perform poorly on low-quality images.

</aside>

The location phase of the minutiae is based on the analysis of the crossing number $cn(p)$, that is the number of changes in color that happen in the neighborhood of a certian pixel that’s taken into account in a certain moment. This value is calculated for each pixel in order to tell if it represents a minutiae or not.

A pixel with value $val(p)=1$ is:

- An **internal point** of a ridge line if $cn(p)=2$. It's not an interesting point;
- A **termination** if $cn(p)$ = 1, because we only have a single change in direction;
- A **bifurcation** if $cn(p) = 3$;
- A more complex minutiae if $cn(p) >3$.

### Ridge count

Ridge count consist in counting the numbers of ridges between two points $a$ and $b$ inside of a fingerprint. This is useful as an abrasct measure of distance between the two points. It's computed simply counting the ridges that intersect the segment $\overline{ab}$. Usually $a$ and $b$ are chosen between relevant points, such as *core* (the innermost arc in a sequence of arcs) or *delta*.

### Hybrid approach

An hybrid approach fuses the comparison between minutiea and texture into a single result. We first extract the minutiae from the fingerprints and then we use Gabor filters with different orientation and frequencies. 

---

### Image Alignment problem

As all the other methods of matching for other biometric traits, also here there is the problem of alignment, meaning that before matching the fingerprints in any way, we have to make sure that they're aligned, otherwise the comparison wouldn’t be reliable.

Given two fingerprint images, the alignment procedure is the following:

1. The minutiae are extracted from each of the fingerprints;
2. One minutiae is chosen as a reference for each of the fingerprints;
3. The minutiae are overlapped and it’s determined the number of matching minutiae pairs using the remaining set of points;
4. The reference pair of minutiae that produces the maximum number of matching pairs is chosen as reference for the best alignment.

### Masking problem

Since not all the regions may be present in both fingerprints, it’s necessary to only take account for the one that are, and which are the best to consider.

### Tessellation and matching with Gabor filters

After that, the image is divided in non-overlapping cells of the same size, and for each cell the light intensity of the pixels is normalized referencing a costant mean and variance.

A bank of 8 Gabor filters is then used on each cell, all with the same frequency but different orientation. This produces 8 sorted images for each cell.

A cell characteristic value is defined as the mean absolute deviation of the intensity of the pixels in the cell. Those characteristic values are concatenated into a characteristic vector. The characteristic values in the vector that belong to a masked region are not used for the comparison and are marked as missing values.

Finally the matching can be computed by computing the sum of squared difference between two characteristic vectors. This score is combined with the one obtained from the comparison of minutiae. The matching is successful if the distance is below a certain threshold.

## Security improvements

### Identify fake fingerprints

Making fake fingerprints is not that hard. It’s possible to build them with various materials, like gelatin, silicon and latex. The problem is that these materials have different properties from an optical and electrical point of view. So in every case, both for optical and capacitive sensor, it’s possible to recognize a fake fingerprint.

### Liveness Detection

Liveness detection on fingerprints has the same principles of live detection on faces.

There is one assumption: if the finger is alive, then the print is of the person to whom it belongs.

The authenticity of the finger can be detected by:

- The characteristics of the pores, that are very difficult to imitate in an artificial fingerprint;
- The color of the skin when it's pressed on the sensor surface;
- The bloodstream, temperature and pulsation, which can be measured by transmitting light through the finger;
- The resistance that the skin have to alternating current
- The sweat

FTIR is a technology that acquire different captures of the ridges of the fingerprints, in this way it can be more robust to attacks by artificial fingerprints.
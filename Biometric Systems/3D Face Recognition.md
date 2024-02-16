---
Exam: Biometric Systems
---
## How to get a 3D model of a face
There are many procedures in order to perform face recognition with a 3D model of a face.

We will talk about three devices that are useful to get a 3D model from a face:

- **Stereoscopic cameras:** the face is captured by one or more streoscopic cameras by multiple point of view. The accuracy is a medium level, the overall procedure is low cost but it's difficult to reproduce the model in real time.
- **Structured light scanner:** a source of light beams hit the object and map the point onto the 3D model. The 2.5D image scan is obtained for each point of view by computing the depth information obtained by the distortion of the light beams. The process has to be repeated with different point of views in order to obtain a full 3D model. The accuracy is medium-high, the overall procedure cost is medium-high and it’s medium-high robust to illumination.
- **Laser scanner:** this is the most accurate result. The procedure is similar to the previous one, instead of many light beams we have a single laser beam that projects its light onto an oscillating mirror and a photocell captures the reflected light. The beam is deformed by the 3D structure and this allows to create a 3D model. The procedure has to be repeated in different points of view. This method is used for object since we have a medium-high cost, high accuracy but the light is dangerous for the eyes.

### Errors in 3D scans

Noise produced by pollution in the air or other materials can create spikes in the 3D model, in order to solve this problems we can apply some filters or try to solve the problem manually.

Another problem is the presence of holes, meaning some areas that are not mapped. This can happen in case some points are not captured by the sensor. A way to solve this problem is by applying some smoothing. 

Smoothing can also be applied in case we have some inaccuracy in the capture in order to smooth the surface.

Another error is the wrong alignment, since when we have different captures, these has to be perfect alignes in order to produce the full model without distorsions. We can solve the alignment problem with the Iterative Closest Point algorithm. 
### More about 3D models

As we said, a 3D model is built by using polygons.

A poolygon is a sequence of coplanar points connected by segments.

In order to determine teh orientation of a surface in the 3D space, we use the normals:

- The normal to a polygos in the vector that’s perpendicular to the plane where the pollygon lies. We can compute the orientation of a polygon in the space by computing the cross product (prodotto vettoriale) of two vectors in the plane.
- The normal to a vertex is the normalized sum of the length of the normals of the adjacent polygons. It identifies the orientation of the vertex in the space.
### From 2D image to 3D model

The method that allows to obtain a 3D model from a set of images is called “shape from shading”. Of course we need a set of images since we cannot recover the shape from a single image. This isn’t true in the case of the Kemelmacher-Shlizerman and Basri approach, where it’s possible to use a single input image to mold a single reference model in order to build a 3D model. 

### 3D features

It’s possible to extract inforamtion about the shape of a 3D face:

- Crest Lines: we select the area with the createst curvature. These areas represent the lines where we can find a sharper variation in orientation;
- Local Curvature: we can represent local curvatures with color. Ligther the color, higher the degreee of the curvature.
- Local Features: we can segment the face into regions of interest and extract features vectors from those regions.
### Normal Maps

A normal map is a projection of a 3D model into a 2D image. The intensity of the RGB pixels map the length of the vector component.

When we want to compare two models, we calculate the difference map, that is the difference image between two normal maps. Each pixel represent the angular distance between the two normal maps in that particular point.

### Morphable Models and Iso-geodesic stripes

As we said before, we can use morphable models in order to represent a face with a 3D model that can morph to simulate facial expression.

To compare two 3D models, we can use iso-geodesic stripes, meaning we can identify stripes that has the same geodesic distance (shortest path between two points in a curved space).

This procedure is obviously more computational expensive than normal maps.

Every face is partitioned into a fixed number of iso-geodesic stripes of equal width, pseudo-concentric and centered on the nose tip of the face. The mutual displacement on each pair of stripes is measured by computing the 3DWWs (3D Weighted Walkthrough) between all possible pair of points of the two stripes.

The benefit of iso-geodesic stripes is that they're robust unde expression changes. 
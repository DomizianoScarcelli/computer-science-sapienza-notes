A particular case of Visual Search is Person Search.

The model will be able to find a queried person, which has never been seen in the train dataset, from a gallery of images. For example a video stream of a surveillance camera can be considered as the gallery of images.

The model learns trough images of other person what are the features that determine the identity of a person (the color of the hair, the shape of the face, the length of the limbs etc.)

Person Search does person detection, re-identification. Detection is the first goal of the model, which first detects all the people. Re-identification means that the model is able to identify a person without ever having seen them. 

If you want to learn both the tasks end-to-end you would need a combination of two losses. Since this is an example of a cascade model, it’s better to first build a model for detecting people, and then a model for identifying the detected people.

>[!Note]
In general, a multi-task neural network learns in a good way if the two tasks help each other. Doing two tasks jointly has sense if those two tasks are related.

Since detection and re-identification are not related (detection just wants to find people, throwing away anything that has to do with identity), the end-to-end approach is not a good idea. This is because the parameters are shared, so you would need to achieve two very different tasks with the same set of parameters.

If you need to follow a person trough multiple cameras, you need identification, since you need to re-identify the person across the different streams. If you only have a single camera and the person never goes out of sight, you can just follow the bounding box and ignore the identity.

>[!Note]
Another way of doing long term tracking if the person goes out of sight is path forecasting. Let’s say the person passes behind an house, you can forecast the path in order to then know that the person that appears is the same person.

## Person Search Architecture

In person search, you first find the bounding box of the people with a Faster R-CNN and then you pass the cropped image to the Re-ID network, which compares it with the images in the gallery. This of course is just an example of an approach.

This approach has been state of the art for a while. It uses Faster R-CNN detection network with ROI Align.

The identification network outputs an unique ID for each identity, so the same person should yield the same, or very close ID. The id is some vector. The match is the person that has the closest match with the query, using something like cosine distance between those id vectors.

The main feature of this network is that during training they found a way for efficiently storing those ID (with a lookup table), and then force the same person to have the same ID, in order for the network to learn.

Another interesting idea is to not crop the query, but use the entire image, in order to also give some importance to the context. In this way the model can contextualise the image and learn the color changes due to the time of the day, and other similar stuff. This is the idea behind the QEEPS paper.
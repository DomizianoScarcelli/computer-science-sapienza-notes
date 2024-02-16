Fourier transforms is an algorithm that allows to break a signal into multiple signals of a single frequency. It’s extremely useful because it allows to check how much of a every frequency is present in a certain signal. With FT you loose information about time.

On the other hand, Wavelet Transforms is able to get the information about both the frequencies that make up a signal, and when those frequencies appear in the signal. 

### Gabor filters

The Gabor filters are a kind of wavelet that is exploit with images and it’s mainly used for edge detection.

The filter only captures only frequencies in a certain interval, cutting the ones above and below thus interval. The Gabor filter is denoted as $\psi_{f, \theta}(x,y)$, and can be represented as a complex sinusoidal signal modulated by a Gaussian kernel function.

A feature vector is obtained by convolving the image with a Gabor filter bank, that is a set of Gabor filters with different orientations and different scales. The set of images resulting the convolution operations enhance different edge contours, such as eye, mouth, nose, scars and so on.

The computational power needed is a lot, since for each image we have to perform as many convolutions as the cardinality of the filter bank. 

> [!Note]
> Incomplete
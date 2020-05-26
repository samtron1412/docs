# Overview

It is a multi-layer neural network designed to analyze visual inputs.


# Some Popular Architectures

- https://towardsdatascience.com/illustrated-10-cnn-architectures-95d78ace614d
- LeNet-5 (1998)
- AlexNet (2012)
- VGG-16 (2014)
- Inception-v1 (2014)
- Inception-v3 (2015)
- ResNet-50 (2015)
- Xception (2016)
- Inception-v4 (2016)
- Inception-ResNets (2016)
- ResNeXt-50 (2017)

# Architecture

There are two main parts:
1. A convolution tool splits the various features of the images
2. A fully connected layer that uses the output of the convolution layer
   to predict the best description for the image.

There are several kinds of layers:
1. **Fully connected input layer**: flattens the outputs of the previous
   layer to turn them into a single vector that can be used as an input
   for the next layer.
2. **Convolutional layer**: creates a feature map to predict the class
   possibilities for each feature by applying a filter that scan the
   whole image, few pixels at a time.
3. **Pooling layer (downsampling)**: scales down the amount of
   information the convolutional layer generated for each feature and
   maintains the most essential information (the process of the
   convolutional and pooling layers usually repeats several times).
4. **Fully connected layer**: applies weights over the input generated
   by the feature analysis to predict an accurate label.
5. **Fully connected output layer**: generates the final probabilities
   to determine a class for the image.

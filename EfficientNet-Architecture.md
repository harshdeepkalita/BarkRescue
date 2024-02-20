# EfficientNet Architecture

## Overview

The courses referenced offered a high-level overview of the EfficientNet model, I found myself seeking more in-depth understanding. It was a YouTube video that sparked my curiosity, leading me to create my own hand-drawn diagram, meticulously capturing the intricate details.

### The 2 main blocks:
### 1) Squeeze-and-Excitation Block:

**High-Level Overview**: The input tensor goes through a Global Average Pooling (GAP) layer to produce a channel-wise vector. This vector is then processed by two fully connected (FC) layers, resulting in a set of weights between 0 and 1. These weights are used to rescale the original input tensor's channels, **allowing the network to emphasize more on the informative channels and pay less attention to the others**.

![EfficientNet-B0 Squeeze-and-Excitation Block](https://github.com/harshdeepkalita/BarkRescue/assets/96279045/278e2b16-2ac9-4e99-9cb0-54e26644e530)


### 2) MBConv Block: 
**High-Level Overview**:


### References:

1. EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks: [https://arxiv.org/pdf/1905.11946.pdf](https://arxiv.org/pdf/1905.11946.pdf)
2. Aladdin Persson YouTube Video: [https://youtu.be/fR_0o25kigM?si=YltCKQ_ijYY4da5I](https://youtu.be/fR_0o25kigM?si=YltCKQ_ijYY4da5I)
3. Udacity Deep Learning Nanodegree: [https://www.udacity.com/course/deep-learning-nanodegree--nd101](https://www.udacity.com/course/deep-learning-nanodegree--nd101)
4. Coursera Deep Learning Specialization: [https://www.coursera.org/specializations/deep-learning](https://www.coursera.org/specializations/deep-learning)

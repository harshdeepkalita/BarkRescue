# Understanding the EfficientNet Model before implementing it on my Project

## Overview

The courses mentioned at the references section offered a high-level overview of the EfficientNet model. I found myself seeking more in-depth understanding. It was a YouTube video that sparked my curiosity, leading me to create my own hand-drawn diagram, meticulously capturing the intricate details.
I'll try to cover the concepts in brief, if you are a beginner and have just started learning about CNNs (and have some knowledge about Attention mechanism and MobileNet-v2), you could refer to this document for learning about EfficientNet model and architecture :)

---

### The Building Blocks of the EfficientNet Model:
### 1) Squeeze-and-Excitation Block:

- **High-Level Overview**: The input tensor goes through a Global Average Pooling (GAP) layer to produce a channel-wise vector. This vector is then processed by two fully connected (FC) layers, resulting in a set of weights between 0 and 1. These weights are used to rescale the original input tensor's channels, **allowing the network to emphasize more on the informative channels and pay less attention to the others**.

![EfficientNet-B0 Squeeze-and-Excitation Block](https://github.com/harshdeepkalita/BarkRescue/assets/96279045/278e2b16-2ac9-4e99-9cb0-54e26644e530)

### 2) MBConv Block: 
- **High-Level Overview**: The input tensor is expanded to increase channel depth to a calculated `hidden_dim`, *enhancing its feature representation capacity*. This expansion is followed by depthwise convolution, which efficiently *extracts spatial features across the expanded channels* with minimal computational overhead. Subsequently, the Squeeze-and-Excitation (SE) block dynamically rescales each channel's importance based on a channel-wise vector obtained from Global Average Pooling (GAP) and processed through two fully connected (FC) layers, yielding weights that *adjust channel intensity to prioritize key features*. The process culminates with a pointwise convolution that aggregates the rescaled features into the final output channel size, **strategically directing the network's focus towards more informative channels and diminishing less relevant ones**.

- **Note for the diagram:** 
  - Conditions :
    - Expansion : if hidden dimensions is not equal to the input channels then we can expand
    - For applying residual connection : input channels must be eqaul to output channels and stride = 1
 
  - To calculate the hidden dimension for the expansion part = expand_ratio * in_channels
  -  We have considered:
    - in_channels = 3
    - expansion ratio = 4
    - stride = 1
    - out_channels = 16

![0](https://github.com/harshdeepkalita/BarkRescue/assets/96279045/f766dfae-a128-4470-967a-7e739775313e)

---

### I am displaying the table from the referenced research paper, this will give you an intuition about the sequence of blocks used to build the EfficientNet-B0 model:

<p align="center">
  <img width="500" alt="image" src="https://github.com/harshdeepkalita/BarkRescue/assets/96279045/1d205aeb-a338-4d02-b8a6-10e6ffe8b9f6">
</p>

---

### The Game Changer Part: Compound Model Scaling used to enhance the model's performance efficiently: 

<img width="1000" alt="image" src="https://github.com/harshdeepkalita/BarkRescue/assets/96279045/2b2305dc-e482-4248-86fb-280038300573">

- **Depth**:
  - refers to the **number of layers** in a neural network.
  - Depth scaling involves adding more layers to the network.
  - EfficientNet scales depth by increasing the number of convolutional blocks, allowing the network to capture more complex patterns.
    
- **Width**:
  - refers to the **number of channels or units** in layers.
  - Width scaling increases the number of channels in each convolutional layer, expanding the network's capacity to process and represent more features simultaneously.
    
- **Resolution**:
  - refers to the **size of the input image** processed by the network.
  - Resolution scaling involves increasing the size of the input images.
  - This allows the network to work with more detailed information but also increases the computational load on the network.

<p align="center"><img width="500" alt="image" src="https://github.com/harshdeepkalita/BarkRescue/assets/96279045/f384b6c0-f886-4cc3-ab2c-e63616e8502a"></p>

This approach is the use of three constants—**α for depth, β for width, and γ for resolution** - which guide how resources are allocated across these dimensions. The unique aspect of this scaling method is its consideration of how changes in each dimension affect the model's computational cost, measured in FLOPS (Floating Point Operations Per Second). 

### As I am going to utilize EfficientNetB0 :
- The values of ϕ (Phi), resolution, and drop connect rate are preset as part of the model's architecture definition. These parameters are specifically optimized for the B0 variant and are intended to provide a balanced starting point for various applications without the need for initial manual tuning.
- ϕ (phi value) is set to 0
- Resolution is fixed at a specific size (typically 224x224 pixels)
- Drop Connect Rate: 0.2
---

### References:

1. EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks: [https://arxiv.org/pdf/1905.11946.pdf](https://arxiv.org/pdf/1905.11946.pdf)
2. Aladdin Persson YouTube Video: [https://youtu.be/fR_0o25kigM?si=YltCKQ_ijYY4da5I](https://youtu.be/fR_0o25kigM?si=YltCKQ_ijYY4da5I)
3. Udacity Deep Learning Nanodegree: [https://www.udacity.com/course/deep-learning-nanodegree--nd101](https://www.udacity.com/course/deep-learning-nanodegree--nd101)
4. Coursera Deep Learning Specialization: [https://www.coursera.org/specializations/deep-learning](https://www.coursera.org/specializations/deep-learning)

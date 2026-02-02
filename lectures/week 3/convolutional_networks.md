# Convolutional Neural Networks


## Learning Goals

Understand how Convolutional Neural Networks (CNNs) work
- What problem CNNs are designed to solve
- Why they outperform fully connected networks on structured data like images

Know when to apply CNNs
- Recognize data that lies in Euclidean doamins (images, audio, time series)
- Understand why convolutions exploit structure that other models ignore

Computer the number of trainable parameters
- Compare parameter counts between fully connected layers and convolutional layers
- Reason about model efficiency and overfitting risk


## Data in Euclidean Domains

What does it mean when data lives in Euclidean Space?
- Fixed dimensional structure
- Meaningful spatial or temporal relationship

Examples
- Images: 2D grid of pixels
- Audio: 1D time signals
- Text after embedding: sequences with local correlations

The key idea is that nearby values are more related to distant ones
- It's this correlation that CNNs are designed to exploit

## So why Convolutions?

Mathematical process that:
- Applies the same local filter across the entire  input
- Extracts local patterns efficiently
- Computed fast on modern hardware like GPUs

Ideal for:
- Edge detection
- Texture recognition
- Detect objects from object parts

## Why not use Fully Connected Neural Networks?

FCNNs treat the input as a flat vector and ignore spatial structure.

For example:

Input image: 256 X 256 = 65,536 pixels
Output layer: 10 neurons

The parameters would be:
- Weight: 256 X 256 X 10 = 655,360
- Biases: 10
- Total: 655,370 parameters

This is very memory intensive
High chance of overfitting
No sense of locality or translation

Dense only architectures scale poorly for images


## Where does CNN solve these issues?


1. Weight sharing
- Same filter is applied at every spatial location
- Share weights across inputs (connection sparsity)
- Reduces parameters

2. Sparse Connectivity
- Each neuron sees only a small local region (receptive field)
- Encourages learning local features

3. Locality
- Nearby pixels are processed together
- Leverage local correlations
- Preserves spatial structure


## Counting Parameters in CNNs

Kernel size → W×H

Input channels → C

Weights per filter → W×H×C

Number of filters → F

Total weights → W×H×C×F

Biases → F

Number of Parameters = (WxH) * C * F + B


Kernel:
- A kernel refers to the 2D spatial weights
(e.g., a 3×3 matrix)
- There is one kernel per input channel

Filter:
- A filter is the stack of kernels across all input channels
- It produces one output feature map

With:
- Input signal length: L
- Kernel Size: 3
- Number of filters: 10

Parameters:
- Weight: 3 X 10 = 30
- Biases:10
- Total: 40 parameters

![CNN Weight Sharing](/diagrams/cnn-weight-sharing.png)


## Convolution Operation (Single Channel Input)

### What is a convolution is simple terms?
- A way for the network to scan an input like an image using a small window called a filter (or kernel)
- Filter is like a pattern detector

So what happens?

1. Filter slides across the input
- Filter is much smaller than the input, ex. 3x3
- Moves left to right, top to bottom
- Looks at a local patch of the input

2. Calculate Dot product at each position
- Values in filter multiplied with the values underneath it
- Products are then added together
- Results in one number for that position

3. Bias is added
- Bias is added after convolution
- Gives flexibility in activation

4. Output is a feature map
- Repeating this process for the whole input image gives us a 2D grid of numbers called feature map
- Here each value shows how strongly the filter detected its patterns at that location


### So what kind of patterns are learned?

Since the filters are local, they learn simple visual structures:
- Edges
- Corners
- Intensity or frequency changes

A single convolution layer does not recognize objects, just patterns


## Padding in Convolution

### What is padding?
- Adding extra pixels (usually zeros) around the border of the image before applying convolution

### Why is padding needed?

1. Preserve spatial dimensions
- Output gets smaller and smaller after each convolution without padding
- Padding helps keep input and output sizes aligned

2. User border information
- Pixels near the edges are used less without padding
- Padding ensures that edge pixels matter as much as center pixels

3. Control output size
- Padding lets us design networks where shapes shrink ONLY when we want them to


### Common padding types

1. Valid padding
- No padding at all.
- Filter only slides where it fully fits.
- Output size shrinks.

2. Same padding
- Padding is added so output size equals input size.
- Most common choice in modern CNNs.

* Padding gives us control over how spatial dimensions evolve through the network


## Multi Channel Inputs (e.g., RGB images)

An RGB image has 3 channels:
- Red
- Green
- Blue

Each pixel is a vector of 3 values

So a filter of W X W is actually W X W X number of input channels

Ex. A 3X3 filter becomes 3X3X3

### What does this mean in practice?

Each filter:
- Looks at all the channels at once
- It combines the colour information spatially

- One filter produces one feature map
- Multiple filters produce multiple feature maps that are stacked depth-wise


### Why this matters?

It means the early layers of the CNN can learn:
- Colour edges
- Texture patterns
- Simple shapes across channels


## Max Pooling

A non linear downsampling operation

Instead of learning weights it:
- Takes a small window (2X2)
- Outputs the maximum value in that window


### Why is it used?

1. Reduces spatial size
- Increases computation speed

2. Keeps the strongest signals
- Most activated features survive

3. Adds translation invariance
- Small shifts in the image doesnt change the output much

4. Helps control overfitting
- Since there is less detail, there is less of memorizing noise


After pooling we decrease height and width, but number of filters increase

* We trade fine spatial detail for more abstract meaningful features


## Flattening

### Why flatten?

Convolution layers output feature maps 3D

Fully connected layers expect vectors

So we take all the values, and lay them into a vector

The convolutions answer what patterns are present and where?
The fully connected layers answer what does this combination of patterns mean?


## Hierarchy of Concepts in CNNs

Learn representation layer by layer

1. Early layers
- Edges
- Gradients
- Simple contrasts

2. Middle layers
- Textures
- Repeated shapes
- Motifs

3. Deeper layers
- Object parts (wheel, eyes, handles)

4. Final layers
- Full objects or classes

* The hierarchy is not programmed, it comes automatically during training


## VGG-16 as an Example

Shows that we dont need complex filters

Just  many small convolutions, stacked deeply with gradual pooling

Architectural ideas it popularized
- Small kernels → fewer parameters
- Depth → expressive power
- Increasing channel count → richer representations

Big lesson from VGG-16
- Depth + simple operations = powerful feature learning

This idea directly influenced modern architectures like ResNet and EfficientNet.

![VGG-16](/diagrams/vgg-16.png)



## Summary

CNNs share weights and use sparse connections

They exploit local correlations in Euclidean data

Convolutions and pooling are the fundamental operations

They drastically reduce parameters compared to dense networks

CNNs naturally learn a hierarchy of concepts

Parameter counting is essential for understanding scalability and generalization
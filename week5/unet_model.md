# U-Net Model


## Learning Goals

1. Understand the U-net architecture and its building blocks
2. Discuss potentail applications of the U-net model

## U-net model

- Fully convolutional neural network
- Initially proposed for biomedical image segmentation problems
- It maps an input of size N into an output also of size N


## Architecture

3 key parts:
- Contracting Path (Encoder)
- Bottleneck
- Expansive Path (Decoder)


### Contracting Path (Encoder)

Just like a normal CNN each block:
- Uses a small filter to scan the image and find features Conv(3x3)
- Uses ReLU to add non linearity to help the model learn better
- Uses Max Pooling (2x2) to shrink the image while retaining the most important information (edges, textures, etc.)


### Bottleneck

- Lowest point of the model
- Small in size but rich in semantic info
- Links both the encoder and decoder


### Expansive Path (Decoder)

Each block here:
- Upsampling -> which increases spatial size
- Concatenate skip connection from the encoder -> Take the feature maps from the encoder to accurately upsample image with details that might have been lost when shrinking.
- Conv (3x3) to clean up and refine the output
- ReLU to add non linearity to help the model learn better (complex shapes, boundaries, edges, irregular shapes, etc.)
- Conv (3×3)
- ReLU


### Final Layer

- The final layer of the U net model involves a 1x1 Convulation Layer
- Looks at one pixel at a time across all channels
- Essentially looks at each pixel and tries to describe what it is based on prediction required

Output:
- Binary Segmentation -> 1 value (probability of class 1) ------ Sigmoid
- Multi class segmentation -> [value, value, value, value] (Each class gets a score) ------ Softmax


* U-Net can also do regression style outputs (continuous values)
- Used for heatmaps, depth estimation and continous values
- Output per pixel would be a real number (not a class) 



## Metrics


1. For regression:
- Mean squared error
- Mean absolute error

2. For segmentation:
- Dice coefficient
- Jaccard coefficient

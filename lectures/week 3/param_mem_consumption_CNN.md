# Parameters and Memory Consumptions of CNNs


## Learning Goals

1. Be able to compute number of parameters of a CNN
2. Estimate GPU memory consumption during training/testing



## Calculating the number of model parameters in a 3D CNN architecture


1. Method A: Formula for per-filter view. Look at a single filter first. "One filter has weights plus bias". Then multiply that unit by the total number of filters.

* Parameters=(Kernel Size×Input Channels+Bias)×Output Channels

In a 3D Convolutional Neural Network, the kernel is volumetric (3X3X3) which results in 27 spatial weights per kernel.

Layer1 = (27 X 1 + 1) X 30 = 840 parameters


2. Method B: Formula for weight/bias seperation. Calculate the massive weights first, then add the total number of biases.

* Parameters=(Kernel Size×Input Channels×Output Channels)+Total Biases

Layer1 = (27 X 1 X 30) + 30 = 840 parameters


Summary
- Method A is useful for understanding the structure of a signle feature map. Every map comes from a specific set of weights plus a bias term.
- Method B is useful for programming and memory estimation. PyTorch or TensorFlow usually store weights as one large tensor and Biases as seperate vector.


Total Model Parameters
- Calculate parameters for each layer, and then sum them up.


## Estimating GPU memory consumption


To estimate GPU memory consumption, you need to calculate the memory required for:
- Feature maps (activations)
- Parameters
- Gradients


### Calculate Feature Map Memory

Need to calculate the memory size for the output for every layer. This is the data volumen flowing through the network


The formula for a single layer's feature map is
* Width X Height X Depth X Channels X Bytes

Layer2 = 191 * 227 * 191 * 30 channels * 4 bytes = 993.74 MB

You repeat this for every layer in the network


### Calculate Parameter and Gradient Memory

You also need to think about the space to store the model's weights (parameters) as well as the calculated updates for those weights (gradients)

- Parameters: Take the total number of parameters and multiply by byte size

Ex. 3,301,651 params * 4 bytes = 13.21 MB

- Gradients: Typically equals the memory size of the parameters

Ex. 3,301,651 grads * 4 bytes = 13.21 MB


### Total Batch Memory Formula

Finally you apply the formula to find the total memory required for a specific Batch Size (bs)

![Total Batch Memory Formula](/diagrams/formula-batch.png)


- Params + Grads: Fixed memory cost, does not increase with batch size
- bs (Batch Size): Multiplier for data dependedent parts. Larger batches require more memory
- I1 = The memory for the input image
- 2 X Ii: Memory for the intermediate feature maps. Multiplies the sum of intermediate layers (I2 to I10) by 2, likely to account for storing both the forward pass activations and the backward pass error signals required for training.


## Summary

These estimates are important because:
1. It allows you to make sure the GPU (VRAM) is sufficient to train the model before you begin.
2. It helps in identifying which layers have the most amount of parameters (consuming the most amount of memory) so you can alter them if you run into bottlenecks or overfitting.

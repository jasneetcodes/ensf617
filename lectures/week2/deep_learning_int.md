# Introduction to Deep Learning

## Learning Goals

Get an intuitive feel for how the majority of deep learning methods work

Get familiar with different activation functions used in deep learning

## Deep Learning intuition

Neural network is built by alternating linear and non linear operations to learn increasingly complex mappings from inputs and outputs

Non linear operations that come after linear operations are called "activations"

The activation at the end of the neural network determins if the model is a classification or regression network

You can have 2 consecutive non linear operations

Having 2 consecutive linear operations is redundant
- Multiple linear layers stacked together are equivalent to a single linear layer
- Stacking them does not increase model expressiveness


The three core ingredients of deep learning training
1. Data
2. Model
3. Cost function or loss or objective

The goal:
- Fit the model to the data by minimizing your cost function

cost function measures how wrong the model's predictions are
- Tells the model how to change, with no loss function there is no learning signal


## Optimization by gradient descent

Algorithm that adjusts the model parameters (weights) to minimize the loss function

The gradient tells which directions to adjust the parameters to decrease the loss

Linear and non-linear operations need to be differentiable, meaning they have a well-defined derivative (slope) that tells how changes in inputs affect the loss.


* So you take the batch THEN predict the outcomes THEN compute the loss THEN compute the gradient THEN update the model weights
- Move to the next batch
- Repeat
- After all batches, you are done 1 epoch

Core loop of deep learning training:
* Batch → Predict → Loss → Gradients → Update
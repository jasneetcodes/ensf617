# Fully Connected Neural Networks


## Learning Goals

Introduce fully connected neural networks

Learn how to compute the number of parameters of your model

## FCNN


A network where every neuron in one layer connects to every neuron in the next layer
- Each output depends on ALL input features


### FCNN Diagram explained

On the left of the diagram, input ball is a feature

Every line connecting two balls is a weight

A neuron in a hidden or output layer  has:
- 1 incoming line per input
- One bias

zi​=wi1​x1​+wi2​x2​+wi3​x3​+bi

A bias is not drawn but is:
- An extra input that is always + 1
- With it's own weight

A layer of neurons is:
- output vector=σ(W⋅input vector+B)
- All lines together = weight matrix W
- All biases = bias vector B

On the most right, the balls are the output

Depending on the tasks:
- Regression: Each output ball is a predicted value, often no activation at the end
- Classification: Each output ball is a class score, softmax activation turns them into probabilities


Balls are neurons, lines are weights, each neuron sums its incoming weighted lines, adds a bias, applies an activation, and passes the result forward.


### Single layer FCNN

No hidden layers just input and outputs

S=σ(WXiT​+B)


Where:

𝑋= one sample

𝑊= weights

𝐵= bias

𝜎= activation


### Multi layer FCNN

Input -> Hidden layer -> Output

Each layer has its own weights, bias, and activation

Each Layer:
1. S(1)=σ1​(W(1)XiT​+B(1))
2. S(2)=σ2​(W(2)S(1)+B(2))

* Function Composite -> Output of one layer becomes the input to the next

### Parameter Counting

(M + 1) x C = P

(Inputs + Bias) * Outputs = Parameters

Parameters tell you:

- Model capacity

- Risk of overfitting

- Memory requirements

- Computational cost


More parameters:

- More expressive

- More data needed

- Higher overfitting risk



### Summary


FCNNs alternate linear operations and non-linear activations

Each neuron computes a weighted sum + bias, then applies an activation

Softmax converts outputs into probabilities for classification

Parameter count per layer is:

(inputs+1)×outputs

Multi-layer networks are built by stacking these layers
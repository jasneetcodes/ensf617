# Fundamental of machine learning

Concepts and context that led to the success of deep learning


## Learning Goals

Explain the difference between AI, ML, and DL

Explain the historical context that led to the success of DL

Introduce basic ML concepts


## AI, ML, DL

AI is the broad disciplein of creating intelligent machines

ML are systems that can learn from experience

DL are systems that can learn from experience using large data sets

Neural Networks (NN) are models of human neural networks that are designed to help computers learn


## What is machine Learning?

Algorithms that parse data, learn from it, and make either predictions or determinations about something.

There are 3 aspects:

1. Data -> engineer or learn features? how to set the experiment?
2. Model -> which model is best
3. Cost function minimization -> setting parameters

The usual concerns are interpretability, explainability, generalizability 

## Traditional ML vs Deep Learning

Traditional machine learning consists of feature engineering, and simpler models where there are less parameters to be learned
- X= N samples with M features.  Y = Labels

Deep learning is a data driven modeling approach where the model 'learns the features'
- More complex model with (b)millions of parameters that need to be turned

Deep learning models tend to be much better in handling complex problems
- Ex. ImageNet Challenge




## Supervised and Unsupervised Learning

Supervised: the data present associated outputs (labels/classes)
Unsupervised: no labels are given to the algorithm
- Goal is to discover groups within the data (clustering), determine distribution of data within input space(density estimation)


## Semi-Supervised Learning

Combines a small amount of labeled data with large amount of unlabeled data during training


## Classification and Regression

Classification referes to decision among a discrete and small set of categories (cancer or not)
Regression refers to estimating a continous output variable (predict sales with x amount of advertising budget)


## Binary and Multi-class and Multi Label Classification

Binary: 2 possible classes
Multi class: More than 2 classes, each sample belongs to exactly one.
Multi Label: A sample can belong to more than one class


## Domain Shift

When the source data distribution is different but related to the target data distribution
Ex. Training data uses high quality images, deployement data uses blurry, weird angle images


## Summary 

The success of Deep Learning came from the development in hardware (GPU/TPU), software and availablity of data

Deep Learning models can learn the features from the data

Deep Learning models performance scales better with the amount of data available

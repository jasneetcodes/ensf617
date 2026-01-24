# Experimental Setup, Model Selection, Overfitting, Regularization

Explaining concepts with a polynomial fitting example



## Learning Goals

Explain how to design your experiment

Introduce the concepts of overfitting, underfitting and model generalization

Introduce the concept of regularization for reducing model over fitting


## Experiment Design: Train, Validation and Test

Dataset is divided into three sets

- Training Set: To learn the paramenters of the models
- Validation Set: To select the best model
- Test Set: To verify generalizability to unseen data


## K-fold cross validation

Performs k iterations on data

Maintains the same proportions of each class into folds (unbalance data)



## Under and overfitting

Under-fitting: too inflexible, captures no pattern
- model is too simple

Over-fitting: too flexible, captures noise in the data
- model is too complex


## Techniques to avoid over-fitting

- More data

- Reduce model complexity (number of trainable parameters)

- Regularization 
1. Dropout
2. L1 and L2 regularization

- Data augmentation


## Dropout

Used in neural networks, where random nodes in a neural network are disabled during the training stage.
This forces more even distribution of information across the neural paths, more subset of neural paths learn the information and to solve the task
Reduces over reliance on one specific node or neural path. Model better generalizes on unseen data.


## Data augmentation

A technique used in supervised learning, where the data is slightly changed (compressed, rotated, cropped) to increase SIZE and DIVERITY of the dataset.
This way the model learns to identify the real patterns, instead of pixel level details and work with more real world variability.

For segmentation tasks, it is important to transform the mask as well as the image IDENTICALLY. They need to be aligned or it will break the label.

Good for small datasets, vision tasks, real world noisy data, high capacity models (CNN, deep nets)


## L1 and L2 Regularization

Idea of regularization is to penalize the model by decreasing its complexity

L1 regularization (Lasso)
- Can be seen as feature selection
- Zero some of the weights to tell what features are not important

L2 regularization (Weight Decay)
- Shrink the weight according to the regularize factor, Not necessarily zero


## Metrics - Classification

### Confusion matrix
Table that shows the classifiers predictions compared to the true labels

TP: Correctly predicted positive

TN: Correctly predicted negative

FP: Predicted positive, but actually negative (false alarm)

FN: Predicted negative, but actually positive (miss)


From these we can compute:
Accuracy = (TP + TN) / Total  -- How many did we accurately classify?

Precision = TP / (TP + FP)  -- Of the positives we classified, how many were actually positive?

Recall (Sensitivity) = TP / (TP + FN)  -- Of the positives in the dataset, how many did we correctly classify as positives?

Specificity = TN / (TN + FP)  -- Of the negatives in the dataset, how many did we correctly classify as negatives?

F1-score = harmonic mean of precision & recall


Multiclass confusion matrix

For C classes:

Matrix is C × C

Rows = true labels

Columns = predicted labels

Diagonal entries = correct predictions
Off-diagonal entries = specific confusions (e.g., 3 mistaken for 5)

### Receiver operating characteristic curve  (ROC)

Evaluates a classifier across all possible decision thresholds
- How does performance change as I move the threshold?



1. X-axis: False Positive Rate (FPR)

FPR= FP / FP+TN 
	​

2. Y-axis: True Positive Rate (TPR / Recall)

TPR= TP / TP+FN 

Each point on the curve corresponds to a different threshold.


Low threshold → predict positive easily
- High TPR
- High FPR

High threshold → predict positive cautiously
- Low FPR
- Low TPR

ROC shows this trade-off.


An AUC of 1.0 is a perfect classifier
An AUC of 0.5 means its randomly guessing
A higher AUC means there is better seperability

AUC measures how well the model ranks positives above negatives, independent of the threshold


## Metrics - Regression

### Structural Similarity (SSIM)

Measures how similiar two images look to a human, not just how different their pixel values are.

Looks at:
- Target image
- Predicted image

The 3 components of SSIM are:
1. Luminance - Are brightness levels similiar?
2. Contrast - Are the intensity variations similiar?
3. Structure - Do edges, texture, and spatial patterns align?


SSIM score
- Range: -1 to 1
- 1.0 is a perfect structural match, where as 0 means there is no similarity


Use Cases:
- When perceptual similarity matters
- Image denoising
- Image compression
- Super resolution
- Medical imaging


### Normalized Root Mean Squared Error (NRMSE)


Measures the average magnitude of error normalized for fair comparison.

RMSE measures the square root of the average squared error
- Depends on the data range

Dataset with 0-1 range and 0-244 but with the same RMSE mean very different things.

NRMSE = RMSE / normalization factor

This way it is scale free, and comparable across datasets



### Peak Signal to Noise Ratio (PSNR)

Measures image quality by comparing the maximum signal value to the noise between the predicted and target images

Uses Mean Squared Error (MSE)
- MSE = On average, how much squared error is there per pixel?


Signal value
- the orignal, correct ground truth image


PSNR scores:
- Higher PSNR = better quality
- Ranges: < 20 -> poor, 30-40 -> good, > 40 -> excellent



### Definitions 

MSE measures average squared error (in squared units)
RMSE takes the square root to express the same error magnitude in the original units of the data, making it easier to interpret.
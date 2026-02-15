# Transfer Learning

## Learning Goals

1. Understand the motivation behind transfer learning approaches
2. Understand the general transfer learning procedure



## What is transfer learning?

* It is the process of taking a representation that a model learned while solving one specific problem and then adapting that representation to solve a different, but related problem.


The primary motivation for using transfer learning is DATA SCARCITY. 
- For situations where you simply do not have enough data in your own dataset to train a complex, full scale model from scratch
- By using a pre trained model, you bypass the need for massive amounts of annotated data



![Lasagna or Endocarditis](/diagrams/lasagna_or.png)


For example, by observing the visual similiarity of Lasagna and Endocarditis.
- We can take the visual patterns (texture, edges, shapes) learned from general images (like lasagna) and be useful for recognizing features in a completely different domain (medical imaging)




## Procedure for implementing transfer learning using a CNN

1. Select a Pre-trained model
2. Freeze the feature learning layers: Prevents the weights from being updated during the initial training
3. Replace and Retrain the Classifer: Remove the old classifier and replace it with a new one that matches your classes. Train ONLY this new classifier on your new data.
4. Unfreeze feature learning layers: Retrain the entire network (features + classifier) using a small learning rate to fine tune the representations.


## Summary

- Powerful technique when dataset is too small to train a full scale model from scratch

- Relies on the assumption that the representation that you learned from one problem will be useful for a seperate but related problem
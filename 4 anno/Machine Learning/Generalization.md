---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning]]"
tags:
  - ML
Creation: 2025-01-09
---
## Generalization

Generalize mean give the right result with a model over new data.
We can't generalize if we haven't a bias.

We can see if our model is able to generalize using the ***test set***. (See the [[Statistical Learning Theory - Vapnik]])


## Overfitting
Overfitting is a phenomenon where a model learns to perform well on training data abut it's not capable to generalize on unseen data.
We can recognize overfitting when we have a high accuracy in training but a low one in test, when our model is too complex with a lot parameters relative to the number of data and when it's sensitive to small variation to the training data.

If a model is yo complex, in number coefficients (weights), it's possible that it could learn to complex pattern in the training set that are not useful to generalize.


> [!NOTE] Definition : OVERFITTING
> A learner overfit data if it outputs a hypothesis $h \in H$ having true/generalization error (risk) $R$ and empirical (training) error $E$, but there's an another $h' \in H$ having $E'>E$ and $R'<R$
> 
> So $h'$ is better then $h$ despite a worst fitting



Technique which are used to control overfitting are:
- [[Regularization]]
- [[K-fold - cross validation|Cross Validation]]


### Complexity 

A model that is too simple cannot representing  the target function and it's possible to make underfitting. If a model is too complex it's possible to do overfitting.
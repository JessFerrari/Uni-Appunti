---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
Creation: 2025-01-09
---
In addiction at the **training**, using the training set, it's important to do : 
- **Model selection** (on Validation set): estimating the performance (generalization error) of different learning models in order to choose the best one; that include hyper-parameters of the model. -> ==returns a model==
- **Model assessment** (on Test set): having chosen a final model estimating/evaluating its prediction error/risk (generalization error) on new test data; measures the performance of the ultimately chosen model -> ==returns an estimation==



For the model selection we can use techniques to create sets to use for training and validation starting from the initial dataset.
- [[Hold Out - cross validation]]
- [[K-fold - cross validation]]

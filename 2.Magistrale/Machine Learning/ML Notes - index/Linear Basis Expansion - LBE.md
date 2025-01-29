---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Linear models]]"
tags:
  - ML
Creation: 2025-01-11
---
***Linear Basis Expansion*** (LBE) is a technique use to extend the capabilities of a [[Linear models|linear model]] by transforming the original features into a new feature space. It's useful for capturing complex relationship in the data that a a simple linear model can't handle directly.

$$h_{\mathbf{w}}(\mathbf{x})=\sum_{k=0}^K w_{k}\phi_{k}(\mathbf{x})$$
Augment the input vector with additional variables which are transformation of $\mathbf{x}$ according to a function $\phi:\mathbb{R}^n\to \mathbb{R}$
$\phi$ could be anything:
- polynomial representation
- non liner transformation of single inputs
- non linear transformation of multiple input 
- ...

With large basis of function we  easily risk overfitting, hence we require methods to control the complexity, for example with the [[Regularization]].

-> Consequences : 
1. [[Curse of dimensionality]]
2. $\phi$ is fixed before observing training data
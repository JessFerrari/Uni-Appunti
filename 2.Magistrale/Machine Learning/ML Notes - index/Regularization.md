---
Subject: "[[Indice - Machine Learning|ML]]"
tags: 
Creation:
---
Regularization is a technique used to control the [[Machine learning#Overfitting|overfitting]] phenomena. 
There are many approaches.

## L2 - Tikhonov regularization+

This works by adding a ***penalty term*** $\lambda$ to the [[Error Function]] in order to discourage the coefficients from reaching large values. That's connected to [[model complexity]].

The simplest penalty term takes the form of a sum of squares of all the coefficients.

This is the modified error function.
$$E(\mathbf{w})=\frac{1}{2}\sum_{n=1}^N\{y(x_{n},\mathbf{w})-t_{n}\}^2+\frac{\lambda}{2}||\mathbf{w||^2}$$


Often the coefficient $w_{0}$ is omitted from the regularizer because its inclusion causes the result to depend on the original choice for the target variable.

The quadratic case is known by the name of **ridge regression**, and in the [[Neural Networks|neural networks]] context such as **weight decay**. 
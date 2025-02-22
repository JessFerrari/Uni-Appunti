---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
Creation: 2025-01-09
---
Recap:
- [[Machine learning#Task|Supervised learning]]
- [[Machine learning#Regression task|Regression task]]
- [[Machine learning#Classification task|Classification task]]
# Linear models
A *linear model* is a model which assume linearity in the system.
The simplest is the one which is linear in the number of input.

- [[Linear models - regression]]
- [[Linear models - classification]]
## Inductive bias

In linear models we can distinguish:
- *Language bias* : as the $H$ set of linear function
- _Search bias_ : ordered search guided by Least Square minimization goal
## Limitation 
Not all the classification problem can b resolved with a linear model.
Given 3 points they are simply separable by a line with $2^3$ cases. 
If we have 4 points we cant.

-> We can extend the linear model with non-linear models using [[Linear Basis Expansion - LBE|Linear Basis Expansion]].
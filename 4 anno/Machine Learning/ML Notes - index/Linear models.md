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
Thy simplest is the one which is linear in the number of input.


- [[Linear models - regression]]
- [[Linear models - classification]]

## Univariate Linear Regression
The univariate linear regression is the simplest case. It's made of 1 input variable $x$ and 1 output variable $y$.
We assume a model $h_{\mathbf{w}}(x) = w_{1}x+w_{0}$, where $\mathbf{w}$ are real-valued coefficients/free parameters (weights).

With this model we can only fit data in a straight line. 

We have an infinite hypothesis space, for the continuous values of $\mathbf{w}$ but it's possible to learn.

##### Training:
For the training we have to find $\mathbf{w}$ such that minimize the empirical loss (the best data fitting on the training set with $l$ data)

- *Given* a set of $l$ training examples $(\mathbf{x}_{p}, y_{p})$,  $p:1\dots l$ 
- *Find* $h_{\mathbf{w}}(x)$ in the form $w_{1}x+w_{0}$ that minimize the expected loss on the training data

For the loss we can use the LMS -> $\text{argmin}_{\mathbf{w}} \text{ Loss}(h_{\mathbf{w}})$
$$\text{Loss}(h_{\mathbf{w}})=E(\mathbf{w})=\sum^l_{p=1}(y_{p}-h_{\mathbf{w}}(x_{p}))^2=\sum_{p=1}^l(y_{p}-(w_{1}x+w_{0}))^2$$
	-> to have the mean divide by $l$: $\frac{1}{l}\sum_{p=1}^l(y_{p}-(w_{1}x+w_{0}))^2$

Because of the local minimum is where the gradient is equal to 0, to solve we can just put equal to 0 each of the partial derivable of the error:
- $\frac{\partial E(\mathbf{w})}{\partial w_{0}}=0$
- $\frac{\partial E(\mathbf{w})}{\partial w_{1}}=0$

And so we have:
	$\frac{\partial E(\mathbf{w})}{\partial w_{i}}=\frac{\partial (y-h_{\mathbf{w}(x)})^2}{\partial w_{i}}=2(y-h_{\mathbf{w}}(x))\frac{\partial (y-h_{\mathbf{w}(x)})}{\partial w_{i}}=2(y-h_{\mathbf{w}}(x))\frac{\partial (y-(w_{1}x+w_{0}))}{\partial w_{i}}$

For $w_{0}$:
$2(y-h_{\mathbf{w}}(x))\frac{\partial (y-(w_{1}x+w_{0}))}{\partial w_{0}}=-2(y-h_{\mathbf{w}}(x))$

for $w_{1}$:
$2(y-h_{\mathbf{w}}(x))\frac{\partial (y-(w_{1}x+w_{0}))}{\partial w_{1}}=-2x(y-h_{\mathbf{w}}(x))$

### Multidimensional input

For multidimensional input we have:
	$\mathbf{w}^T\mathbf{x}+w_{0}=w_{0}+w_{1}x_{1}+w_{2}x_{2}+\dots+w_{n}x_{n}=w_{0}+\sum^n_{i=1}w_{i}x_{i}$

## Inductive bias 

In linear models we can distinguish:
- *Language bias* : as the $H$ set of linear function
- _Search bias_ : ordered search guided by Least Square minimization goal
## Limitation 
Not all the classification problem can b resolved with a linear model.
Given 3 points they are simply separable by a line with $2^3$ cases. 
If we have 4 points we cant.

-> We can extend the linear model with non-linear models using [[Linear Basis Expansion - LBE|Linear Basis Expansion]].
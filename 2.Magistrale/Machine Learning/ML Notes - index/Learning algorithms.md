---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Linear models]]"
tags:
  - ML
Creation: 2025-01-10
---
We can distinguish two central algorithm, each valid for regression and classification using linear models.

1. A direct approach based on *normal equation* solution
2. An iterative approach based on *gradient descent*

## Learning problem 

- *Given* a set of $l$ examples $(\mathbf{x}_{p},y_{p})$ and a loss function measure $L$
- *Find* the weight vector $\mathbf{w}$ that minimizes the expected loss on the training data$$R_{\text{emp}}=\frac{1}{l}\sum_{p=1}^lL(h(\mathbf{x}_{p}),y_{p})$$
-> using a piecewise constant for classification, over the function $\text{sign}(\mathbf{w}^T\mathbf{x})$, can be a difficult problem. So we assume we use the [[Machine learning#Loss for Regression|MSE]] (it's smooth and differentiable)

### Last squeare

- *Find* $\mathbf{w}$ to minimize the residual sum of squares:$$E(\mathbf{w})=\sum_{p=1}^l(y_{p}-\mathbf{x}^T_{p}\mathbf{w})^2=||\mathbf{y}-\mathbf{Xw}||^2$$
We could obtain the min error if when $y_{p}=1$ and $\mathbf{x}_{p}^T\mathbf{w}$ go toward 1 and when $y_{p}=-1$ and $\mathbf{x}_{p}^T\mathbf{w}$ go toward -1.


This is a quadratic function that means the *minimum always exists* but may be not unique.
$\mathbf{X}$ is a matrix $\mathbf{1}\text{ x }\mathbf{n}$ with a row for each input vector $\mathbf{x}_{p}$.


# Normal equation


If we differentiate $E(\mathbf{w})$ with respect to $\mathbf{w}$ we obtain:
$$\frac{\partial E(\mathbf{w})}{\partial w_{j}}=\frac{\partial \left( \sum_{p=1}^l(y_{p}-\mathbf{x}^T_{p}\mathbf{w}) ^2\right)}{\partial w_{j}}=-2\sum_{p=1}^l(y_{p}-\mathbf{x}_{p}^T\mathbf{w})x_{p,j}$$
we can call $\delta$ the term $(y_{p}-\mathbf{x}^T_{p}\mathbf{w})$ and we get : $-2\sum_{p=1}^l \delta_{p}x_{p,j}$

- Point the gradient of $E$ w.r.t. $\mathbf{w}$ equal to 0, we can get the normal equation:
$$(\mathbf{X}^T\mathbf{X})\mathbf{w}=\mathbf{X}^T\mathbf{y}$$
- If $\mathbf{X}^T\mathbf{X}$ is not [[Singular Matrix|singular]], the unique solution is given by: (where $\mathbf{X}^+$ is the [[Moore-Penrose pseudoinverse matrix]])
$$\mathbf{w}=(\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}=\mathbf{X}^+\mathbf{y}$$

The [[Singular Value Decomposition]] (SVD) can be used for computing the pseudoinverse of a matrix ($\mathbf{X}^+$)
$$\mathbf{X}=\mathbf{U\Sigma V}^T\to \mathbf{X}^+=\mathbf{V\Sigma^+ U}^T$$
- Where $\Sigma$ is the diagonal, and we obtain $\mathbf{X}^+$ by replacing every non zero entry by its reciprocal 

Moreover we can apply directly SVD to compute $\mathbf{w}=\mathbf{X}^+\mathbf{y}$ obtaining the minimal norm on $\mathbf{w}$ solution of the last square problem.

# Gradient descent
It's an iterative technique that:
- has more efficient solutions
- reduce the complexity of the model by [[Regularization]]
- make a better approximation with noisy data by stopping searching before the minimum : [[Early stopping]]

The [[Gradiente|gradient]] shows the direction where the function grows, since we want the minimum of the function we want to follow the direction in which he function decreases : the *negative of the gradient* $\Delta \mathbf{w}=-\nabla E(\mathbf{w})$.

It's a local search which modify iteratively the $\Delta \mathbf{w}$ to decrease up to minimize the error function.

## Learning rule : delta rule

We update the vector of weights $\mathbf{w}$ adding the $\Delta \mathbf{w}$:
$$\mathbf{w}_{\text{new}}=\mathbf{w}+\eta \Delta \mathbf{w}$$
where $\eta$ is the ***Learning rate***, the step size parameter ruling the speed of our gradient descending.

## Algorithm

1. Start with a weight vector $\mathbf{w_{\text{initial}}}$ (small) and fix $0<\eta<1$
2. Repeat until convergence or $E(\mathbf{w})$ is sufficiently small
	1. Compute $\Delta \mathbf{w}=-\nabla E(\mathbf{w})=-\frac{\partial E(\mathbf{w})}{\partial\mathbf{w}}$ for each $w_{i}$
	2. Compute the update $\mathbf{w}_{\text{new}}=\mathbf{w}+\eta \Delta \mathbf{w}$ for each $w_{i}$


- LMS : standard case dividing by $l$ -> $\frac{\Delta \mathbf{w}}{l}$
- Batch version -> compute $\Delta \mathbf{w}$ after each epoch of $l$ training patterns
- $\eta$ can gradually decrease to zero


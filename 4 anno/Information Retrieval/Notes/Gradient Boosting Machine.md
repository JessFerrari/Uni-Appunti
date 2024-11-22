---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Efficient training and inference of ensemble of decision trees forest]]"
tags:
  - IR
  - ML
Creation: 2024-11-20
---
In the *Gradient bosting* we ave multiple *weak leaners* that their result is a part for the final result.

The final result is compute as:

$F(x)=\sum_{i=0}^MF_{i(x)}$ 

The gradient boosting is used for [[Classification]], [[Regression]] and [[Learning to rank]] problems.


We have some **input data** in the form $\{(x_{i},y_{i})\}_{i=1}^n$ , where $x_{i}$ is a multi dimensional  [[vector of feature]], a dimension for each feature, and $y_{i}$ is a [[Machine learning|target value]]. We also have a [[Funzione differenziabile|differentiable]] [[loss function]] $L(y_{i}, F(x_{i}))$.

We want to evaluate how far is our prediction to the target value.
So we have an [[Optimization|optimization problem]].
If we learn to much from the data we will go to the [[overfitting]].

The **initial prediction** $F_{0}$ is the average of the target values because is the one that minimize the initial [[MSE]]. We don't know anything about the data points.
$$F_{0}(\mathbf{x}_{i})=\frac{1}{n}\sum_{i=1}^n y_{i}$$ Than we want the **pseudo residuals** for the others $m$ weak learners. (Recall: $m\in[1,M]$)

The pseudo residuals for the [[Gradiente|gradient]] are the [[derivate parziali|partial derivatives]] of the loss function. The residual is the mistake made by the previous model on the $i$ data point
$$r_{i,m}=-\left[ \frac{\partial L(y,i,F(x_{i})) }{\partial F(x_{i})} \right]_{F(\mathbf{x})=F_{m-1}(\mathbf{x})} \ \ \ \ \ \ \text{for } i=1,\dots,n$$
For the [[MSE]] the $r_{i,m}$ is compute as : $$r_{i,m}=y_{i}-F_{i}(x_{m})$$
![[Pasted image 20241121170302.png]]
The loss function is fixed and for each data point we compute the prediction (real value) and for every prediction we compute the loss function.
With the partial derivate of the loss for the $F_{m}$ we obtain a direction in which i want to go with the next model.

Then we want to fit a new regression tree on the pseudo residual and create $k_{m}$ leaves (terminal regions).
For each region $j$ we assign a value. From a datapoint $x_{i}$ in the region $j$ we compute the value $\gamma$ using the previous prediction and the correction that we made:
$$\gamma_{j,m}=argmin_{\gamma} \sum_{x_{i}}L(y_{i},F_{m-1}(x_{i})+\gamma)$$
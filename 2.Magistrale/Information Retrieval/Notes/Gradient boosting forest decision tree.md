---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Learning to rank]]"
tags:
  - IR
  - PEA
  - ML
Creation: 2024-11-21
---
## Motivations
___
With [[Learning to rank]] it's possible to create a [[4 anno/Machine Learning/Machine Learning]] model which ranks documents using a [[Ranking models|ranking method]], i.e. [[BM25 (Best Matching 25)|BM25]], to sort them, trying to maximize a [[Ranking metrics]], such as the [[NDCG]].

Starting from a dataset, which is composed by queries, documents and features, te objective is **training** the model (off-line process) and **ranking** the documents (inference, online process).

We use **gradient boosting forest decision tree** for the learning to rank model.

At the end of training time we produce a forest and at the end of each inference time we go thought the whole forest.

We use [[Ensemble]], in particular the **Gradient Boosting Machine** with [[Decision trees]]  forest. The score of a document is made by the sum of the partial score of each tree. Each tree is a weak learner.

The gradient boosting is used for [[4 anno/Machine Learning/Machine Learning#Classification task|classification]], [[4 anno/Machine Learning/Machine Learning#Regression task|regression]] and [[Learning to rank]] problems.

## Dataset, loss function and details on trees 
We have some **input data** in the form $\{(x_{i},y_{i})\}_{i=1}^n$ , where $x_{i}$ is a multi dimensional  [[vector of feature]], a dimension for each feature, and $y_{i}$ is a [[4 anno/Machine Learning/Machine Learning#^af8e9d|target value]]. We also have a [[Funzione differenziabile|differentiable]] [[4 anno/Machine Learning/Machine Learning#Loss|loss function]] $L(y_{i}, F(x_{i}))$, such as a MSE.


The number of decision trees is thousand up to 20 thousands, and each tree is a small model that have from 16 to 512 leaves.
The number of features involved depends on the ask but usually is about 100 up to 2000.
![[Pasted image 20241121155135.png]]

Here the [[Decision trees]] are small trees in which each node has a threshold and a feature. A document is associated a score of a feature and from the root we arrive at leaves.
Potentially every node have much than a feature, it depends on the training phase.
![[Pasted image 20241121162108.png]]
We stop when we arrive at one leaf and we have a score for a document.

If the feature score is greater than the threshold we go to the right if is less than it we go to left. 

## How it works

In the *Gradient bosting* we ave multiple *weak leaners* that their result is a part for the final result.

The final result is compute as:

$F(x)=\sum_{i=0}^MF_{i(x)}$ 
The **initial prediction** $F_{0}$ is the average of the target values because is the one that minimize the initial [[4 anno/Machine Learning/Machine Learning#Loss|MSE]]. We don't know anything about the data points.
$$F_{0}(\mathbf{x}_{i})=\frac{1}{n}\sum_{i=1}^n y_{i}$$ Than we want the **pseudo residuals** for the others $m$ weak learners. (Recall: $m\in[1,M]$)

The pseudo residuals for the [[Gradiente|gradient]] are the [[Derivate parziali|partial derivatives]] of the loss function. The residual is the mistake made by the previous model on the $i$ data point
$$r_{i,m}=-\left[ \frac{\partial L(y,i,F(x_{i})) }{\partial F(x_{i})} \right]_{F(\mathbf{x})=F_{m-1}(\mathbf{x})} \ \ \ \ \ \ \text{for } i=1,\dots,n$$
For the MSE the $r_{i,m}$ is compute as : $$r_{i,m}=y_{i}-F_{i}(x_{m})$$
![[Pasted image 20241121170302.png]]
The loss function is fixed and for each data point we compute the prediction (real value) and for every prediction we compute the loss function.
With the partial derivate of the loss for the $F_{m}$ we obtain a direction in which i want to go with the next model.

Then we want to fit a new regression tree on the pseudo residual and create $k_{m}$ leaves (terminal regions).
For each region $j$ we assign a value. To do that, from a datapoint $x_{i}$ in the region $j$ we compute the value $\gamma$ using the previous prediction and the correction that we made:
$$\gamma_{j,m}=argmin_{\gamma} \sum_{x_{i}}L(y_{i},F_{m-1}(x_{i})+\gamma)$$
We simply choose the value $\gamma$ which minimize the summatory.
Then we update the model $F_{m}(\mathbf{x})$ adding to the previous model the correction $\gamma$ weighted by the learning rate $\alpha$ (in machine learning we call it $\eta$).
$$F_{m}(x)=F_{m-1}+\alpha \gamma_{j,m}$$



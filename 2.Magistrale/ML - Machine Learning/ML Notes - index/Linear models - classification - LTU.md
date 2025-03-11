---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Linear models]]"
tags:
  - ML
Creation: 2025-01-09
---
# Classification by hyperplanes

The problem is dived points from an unknown distribution into classes, and in particular we want to predict the class of future datapoints.

We use the same model used for the [[Linear models - regression|regression]], but in this case $\mathbf{w}^T \mathbf{x}$ is the hyperplane that separate classes. 

Data have categorical targets (0/1 or -1/+1), and we can say that a point belong to a specific class by the zone of the hyperplane in which it is.

The objective is set $\mathbf{w}$ by learning such that we get a good classification accuracy.

For two variables, the hyperplane will be:

$$\mathbf{w}^T \mathbf{x}=\mathbf{x}^T \mathbf{w}=w_{0}+w_{1}x_{1}+w_{2}x_{2}=0$$
and our hypothesis :
	if the output range is $[0,1]$
$$h(\mathbf{x})=\begin{cases}
1 \ \text{ if } \mathbf{w}^T\mathbf{x}+w_{0}\geq 0 \\ \\
0 \ \text{ otherwise}
\end{cases}$$
	or in the case it's $[-1, 1]$
	$$h(\mathbf{x})=sign(\mathbf{w}^T\mathbf{x}+w_{0})$$

The bias $w_{0}$ has the role of threshold because saying that $h(\mathbf{x})=\mathbf{w}^T\mathbf{x}+w_{0}\geq0$ is equivalent to say $h(\mathbf{x})=\mathbf{w}^T\mathbf{x}\geq -w_{0}$.

## Properties
- if $w_{0}=0$ the line goes through the origin of the coordinate system
- if $n>2$ the hyperplane generalizes to higher dimensions as a decision boundary
- *scaling freedom* : multiplying $\mathbf{w}$ by a scalar $K$ results in the same decision boundary
- *orthogonality* : $\mathbf{w}$ is a vector orthogonal to the hyperplane :
	Given $\mathbf{x}_{a}, \mathbf{x}_{b}$ belonging to the separation hyperplane.
	We have $\mathbf{w}^T\mathbf{x}_{a}+w_{0}=0$ and $\mathbf{w}^T\mathbf{x}_{b}+w_{0}=0$
	If we take the different : $\mathbf{w}^T (\mathbf{x}_{a}-\mathbf{x}_{b})=0$ that means that $\mathbf{w}$ is orthogonal to $\mathbf{x}_{a}-\mathbf{x}_{b}$
- *separability* : if a separating hyperplane exists, there ca be many such hyperplane with multiple possible solutions


# LTU
---

L'**LTU** (Linear Threshold Unit) consente di definire un **iperpiano** che suddivide lo spazio dei dati in due regioni, ciascuna corrispondente a una classe. 

Gli **LTU** sono efficaci in molti contesti, ma hanno limitazioni nel separare dati non linearmente separabili.

Questo concetto è strettamente legato al [[Statistical Learning Theory - Vapnik]].

L'iperpiano separa le due classi generando un insieme di **dicotomie**, che corrispondono al numero di possibili ipotesi $h$ nello **spazio delle ipotesi** $H$.

Più formalmente, il numero di dicotomie rappresenta la capacità del modello di separare il dataset in differenti modi, e questa capacità è direttamente legata alla **[[VC-Dimension]]** (Vapnik-Chervonenkis Dimension), una misura fondamentale della complessità di un modello di apprendimento.
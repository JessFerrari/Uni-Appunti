---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[SVM]]"
tags:
  - "#ML"
Creation: 2025-02-13
---
*A complex pattern-classification problem, cast in high-dimensional space nonlinearly, is more likely to be linearly separable than in a low-dimensional space, provided that the space is not densely populated.*



Let $\mathbf{X}$ denote a set of $N$ patterns (vectors) $\mathbf{x}_{1},\dots,\mathbf{x}_{N}$, each of which is assigned to a a class between $X_{1}, X_{2}$.
The binary partition of the points is said to be linearly separable respect to a family of surface, if in the family exists a surface that divides the points into the to classes.

For each pattern $\mathbf{x} \in \mathbf{X}$ define a vector of real-valued function: $$\mathbf{\phi}(\mathbf{x})=[\phi_{1}(\mathbf{x}),\dots,\phi_{m_{1}}(\mathbf{x})]^T$$
This vector maps $\mathbf{x}$ from a space $m_{0}$-dimensionality to a new one $m_{1}$-dimensionality. 
Every function $\phi_{i}$ of the vector is called *hidden function* cause il plays a role similar to a hidden unit of a [[Neural Networks]], and the new space $\{\phi_{i}(\mathbf{x})\}_{i=1}^{m_{1}}$ is called *Feature space*.

# Theorem (Cover, 1965)
A dichotomy $\{\mathbf{X}_{1},\mathbf{X}_{2}\}$ of $\mathbf{X}$ is said to be $\phi$ separable if there exists an $m_{1}$-dimensional vector $\mathbf{w}$ such that:
$$\begin{cases}
\mathbf{w}^T\mathbf{\phi}(\mathbf{x})>0, \quad \mathbf{x}\in X_{1} \\
\mathbf{w}^T\mathbf{\phi}(\mathbf{x})<0, \quad \mathbf{x}\in X_{2}
\end{cases}$$


The hyperplane that describe the separating surface in the $\phi$-space is define by : $\mathbf{w}^T\mathbf{\phi}(\mathbf{x})=0$.

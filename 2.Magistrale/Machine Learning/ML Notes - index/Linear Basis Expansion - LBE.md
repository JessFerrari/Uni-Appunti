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

# NN as LBE
Le reti neurali possono essere viste come un metodo per fare [[Linear Basis Expansion - LBE|espansione di base LBE]]. 
Infatti, ricordiamo che per la LBE si otteneva:
- classificazione : $h(\mathbf{x})=f\left( \sum_{j}w_{j}\phi_{j}(\mathbf{x}) \right)$ 
- regressione : $h(\mathbf{x})=\sum_{j}w_{j}\phi_{j}(\mathbf{x})$

Data una rete neurale della forma : $h(\mathbf{x})=f_{k}\left( \sum_{j} w_{jk}f_{j}\left( \sum_{i}w_{ij}x_{i} \right)\right)$
Se si pone $\phi_{j}(\mathbf{x,w})=f_{j}\left( \sum_{i} w_{ji}x_{i}\right)$
Si ottiene una rete della forma : $h(\mathbf{x})=f_{k}\left( \sum_{j}w_{j}\phi_{j(\mathbf{x,w})} \right)$

In questo caso $\phi$ non dipende solo dai dati ma anche dai pesi.

## SVM as LBE
Per i problemi non linearmente separabili si portano i dati in uno spazio con dimensionalità più alta con una funzione $\phi:\mathbb{R}^{m_0}\to \mathbb{R}^{m_{1}}$
Computazionalmente è difficili e si usano quindi i [[SVM - Kernel]].

## differenze:
- LBE è un'espansione di base fissa e selezionata in precedenza
- le NN sono adattive e quindi flessibili. Dato che $\phi$ dipende anche dai pesi e questi sono in evoluzione nel processo di training allora anche $\phi$ cambierà nel metre
	- Ogni hidden unit si può vedere come una LBE indipendente che impara una feature non lineare in modo adattivo.
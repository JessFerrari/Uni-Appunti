---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Perceptron]]"
tags:
  - "#teorema"
  - ML
Creation: 2025-02-05
---
Garantisce la convergenza del [[Perceptron|percettrone]] in un numero finito di step se il problema è linearmente separabile. 
Ciò indipendentemente dal punto di partenza .

Se il problema non è linearmente separabile può risultare instabile e presentare cicli nelle scelte dei pesi non ottimali.

Assunzioni:
- $(\mathbf{x}_{i}, d)$ è un pattern del TR set con $d_{i}=\pm_{1},  i=1\dots l$
- un problema si dice linearmente separabile se esiste una soluzione $\mathbf{w}^*$ tale che $d_{i}(\mathbf{w^*}^T\mathbf{x}_{i})\geq \alpha$, dove $\alpha =min_{i}(d_{i}(\mathbf{w^*}^T\mathbf{x}_{i}))>0$. 
	Quindi $\mathbf{w^*}^T(d_{i}\mathbf{x}_{i}\geq \alpha)$
- Definendo $\mathbf{x'}_{i}=(d_{i}\mathbf{x}_{i})$ allora $\mathbf{w^*}$ è soluzione se e solo se $\mathbf{w^*}$ è soluzione di $(\mathbf{x'}_{i}, +1)$
-
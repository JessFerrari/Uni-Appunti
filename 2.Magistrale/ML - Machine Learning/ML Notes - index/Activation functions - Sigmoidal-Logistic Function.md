---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Activation functions]]"
tags:
  - ML
  - Functions
Creation: 2025-03-04
---
# Sigmoidal-Logistic Function
---
La funzione di attivazione Sigmoidale (o Logistica) definita come:
$$f_{\sigma}(\mathbf{x})=\frac{1}{1+e^{-ax}}$$
è una funzione adatta ai problemi di classificazione binaria.

Questa funzione è differenziabile, smooth e rappresenta un threshold

Il parametro $a$ è detto *parametro slope* della funzione sigmoidale.
- Semilinearità vicino a 0 e a 1
- Se $a=0$ diventa lineare
- se $a\to \infty$ diventa LTU

Se il risultato della funzione è maggiore del threshold allora si classifica come classe positiva, altrimenti come 0 o classe negativa.

La funzione Sigmoidale è sensibile al problema del [[Vanishing gradient]]

![[Logistic function.png]]

Al posto di questa si può usare la [[Activation functions - TanH|TanH]].

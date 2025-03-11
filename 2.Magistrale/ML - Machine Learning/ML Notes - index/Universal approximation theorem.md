---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks]]"
tags:
  - ML
  - NN
Creation: 2025-02-05
---
Una rete con un singolo hidden layer può approssimare, arbitrariamente bene, qualsiasi funzione continua, o sull'ipercubo, avendo a disposizione di abbastanza hidden units.
Quindi una MLP può approssimare arbitrariamente bene ogni mapping input-output avendo a disposizione abbastanza hidden units negli hidden layer.

## Teorema:
Dato $\epsilon, \exists h(\mathbf{x})$ tale che $|f(\mathbf{x})-h(\mathbf x)|< \epsilon \ \forall \mathbf{x}$ nell'ipercubo

Questo è teorema di esistenza e non fornisce ne un algoritmo ne un numero di unità da utilizzare.
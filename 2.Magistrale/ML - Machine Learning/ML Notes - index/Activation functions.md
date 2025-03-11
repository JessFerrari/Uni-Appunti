---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks]]"
tags:
  - ML
Creation: 2025-02-05
---
Le funzioni di attivazione sono [[Funzioni|funzioni]] che servono a introdurre non linearità nel modello, permettendo alla rete di apprendere e rappresentare relazioni complesse tra input e output.

Senza di esse, una rete neurale composta da più livelli sarebbe equivalente a un [[Linear models|modello lineare]]. 


# Perceptron unit
---
Il [[Perceptron|Percettrone]] usa la funzione di attivazione Threshold, come il LTU (Linear Threshold Unit).



# Sigmoidal-Logistic Function
---
$$f_{\sigma}(\mathbf{x})=\frac{1}{1+e^{-ax}}$$
- è una funzione differenziabile, smooth e rappresenta un threshold
- $a$ è il parametro di slope della funzione sigmoidale.
- Semilinearità vicino a 0 e a 1
- Se $a=0$ diventa lineare
- se $a\to \infty$ diventa LTU
![[Logistic function.png]]


Al posto di questa si può usare la ***Tanh***, che passa per 0 ed è simmetrica:
$$f_{\text{symm}}=2f_{\sigma}(\mathbf{x})-1=TanH\left( \frac{ax}{2} \right)$$

Se il risultato della funzione è maggiore del threshold ( sia nella logistica che in Tanh) allora si classifica come classe positiva, altrimenti come 0 o classe negativa.

# Radial basis Functions
---
$$f(\mathbf{x})=e^{(-ax)^2}$$
Come $\mathbf{x}$ si usa la norma tra i pesi e gli input : $||\mathbf{W}-\mathbf{X}_{input}||$
![[Gaussian function.png]]

Queste funzioni sono: 
- ***SoftMax***: per la classificazione multi classe
- ***Stochastic neurons with probability***

# RELU
---
è la funzione di default per il deep learning.

$$f(x)=\begin{cases}
0, for x<0 \\
x for x\geq 0
\end{cases}$$
che si può anche vedere come $f(x)=max(0,x)$

# SoftPlus
---
Che approssima in modo più smooth la Relu:
$$f(x)=\ln(1+e^x)$$
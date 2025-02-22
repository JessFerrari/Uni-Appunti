---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks]]"
tags:
  - ML
  - "#NN"
Creation: 2025-02-05
---
Un percettrone è un singolo neurone molto semplice ed è la base delle reti neurali.

Una rete che si compone di più percettroni a più layer si chiama ***Multi Layer Perceptron (MLP)***.

Un neurone $i$ diventa attivo quando la somma della connessioni $W_{ij}$ più il bias è, in valore assoluto, maggiore di zero.

## Perceptron learning algorithm

Questo algoritmo ha lo scopo di minimizzare il numero di patterns mal classificati.
L'idea è : trovare $\mathbf{w}$ tale che $\text{sign}(\mathbf{W}^T\mathbf{x})=d$

è un algoritmo on-line ed ogni suo step può essere effettuato singolarmente per ogni pattern.

1. Inizializzare i pesi e scegliere un learning rate $\eta$
2. while le stop condition non sono soddisfatte:
	1. calcolare $\text{out}=\text{sign}(\mathbf{W}^T\mathbf{x})$
	2. se $\text{out}=d$ non cambiare i pesi
	3. se $\text{out}\neq d$ -> $\mathbf{w}_{new}=\mathbf{w}+\eta d \mathbf{x}$


# Delta rule
---
Se per l'algoritmo di learning vogliamo correggere l'errore di classificazione dobbiamo calcolare la differenza tra il nostro output e il valore desiderato. Quindi la regola di update diventa:

$$\mathbf{W}_{new}=\mathbf{W}+\eta(d-out)\mathbf{x}=\mathbf{W}+\eta \delta \mathbf{x}$$
Ciò comporta che se $d-out=0\to d= out$ e non si applica nessuna correzione. Altrimenti la correzione è pari alla distanza tra i due.




Il percettrone è sempre in grado di imparare quel che può rappresentare [[Perceptron convergence Theorem]].


## Differenze con LMS
- LMS si deriva con il gradiente senza usare la [[Activation functions#Perceptron unit|Threshold activation function]]. Usa direttamente $\mathbf{w}^T\mathbf{x}$ mentre il percettrone usa il segno.
- Cambia il delta
	- LMS : $\delta=(d-\mathbf{w}^T\mathbf{x})$
	- perceptron : $\delta=(d-\text{sign}(\mathbf{w}^T\mathbf{x}))$

La LMS si può usare per la classificazione se le si applica il segno (LTU)
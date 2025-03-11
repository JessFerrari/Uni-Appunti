---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning - Task]]"
tags:
  - ML
Creation: 2025-03-04
---
Un ___problema di classificazione___  ha l'obiettivo di assegnare una classe, etichetta discreta, a ciascun dato di ingresso.
Un problema di classificazione può essere visto come **l'assegnazione di un input alla regione di decisione corretta** nello spazio delle caratteristiche (feature space).

Formalmente, si tratta di una funzione che restituisce un valore discreto:
$$f(\mathbf{x})\to \text{classe di } \mathbf{x}$$


A seconda del numero di classi presenti nel problema, possiamo distinguere due scenari principali:

- **Classificazione binaria (Binary Classification)**: se il numero di classi è **2**, la funzione $f(\mathbf{x})$ è una funzione booleana e il problema rientra nella categoria del _concept learning_. 
- **Classificazione multiclasse (Multiclass Classification)**: se il numero di classi è maggiore di **2**, il problema diventa **multiclasse**.



Le ipotesi che definiscono il modello di classificazione si basano su funzioni decisionali che separano il feature space in regioni associate a ciascuna classe. 

Un esempio comune di funzione ipotesi è:
$$h(\mathbf{x})=\begin{cases}
1 \text{  if  } \mathbf{w}^T\mathbf{x}+w_{0} \geq {0} \\
0 \text{        otherwise}
\end{cases}$$
o in forma più compatta:
$$h(\mathbf{x})=\text{sign}(\mathbf{w}^T\mathbf{x}+w_{0})$$


Queste funzioni rappresentano **funzioni indicatrici** del **[[Linear models - classification - LTU|LTU]] (Linear Threshold Units)**, ovvero modelli di classificazione lineari.
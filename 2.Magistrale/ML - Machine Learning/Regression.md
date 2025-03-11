---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning - Task]]"
tags:
  - ML
Creation: 2025-03-04
---

L'obiettivo di un problema di **regressione** è approssimare una funzione continua che mappa un insieme di input $\mathbf{x}$ a un valore numerico reale. 
Formalmente, un problema di regressione può essere espresso come:

$$f(\mathbf{x}) \to \mathbb{R}$$

Nella regressione il modello cerca di prevedere un valore numerico per ogni input

Un problema di regressione può essere visto come la **determinazione della funzione che meglio approssima la relazione tra input e output** minimizzando l'errore tra le predizioni del modello e i valori reali.


Le ipotesi di base nei problemi di regressione si basano su funzioni continue che stimano il valore di uscita con una certa precisione. 

Un esempio comune è la [[Linear models - regression|regressione lineare]], definita dalla funzione:

$$h(\mathbf{x}) = \mathbf{w}^T\mathbf{x} + w_0$$​

dove il vettore $\mathbf{w}$ rappresenta i coefficienti del modello e $w_0$​ è il termine di bias.

Questo modello definisce un **iperpiano** che cerca di adattarsi ai dati minimizzando un'opportuna funzione di perdita, come l'**errore quadratico medio** ([[MSE]]):

$$\mathcal{L} = \frac{1}{N} \sum_{i=1}^{N} (h(\mathbf{x_i}) - y_i)^2$$
dove $y_i$ è il valore reale associato al dato $\mathbf{x_i}$​ e $N$ è il numero di campioni nel dataset.
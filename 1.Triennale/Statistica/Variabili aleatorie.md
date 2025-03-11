---
Subject: "[[Indice - Statistica|STAT]]"
tags:
  - STAT
Creation: 2024-11-20
Esercizi: "[[Esercizio Variabili Aleatorie]]"
---
Una variabile aleatoria è uno strumento utile per studiare i modelli. 
Risulta semplice lavorarci perché, in quanto funzioni, hanno ampia libertà di calcolo.


## Variabile aleatoria



Una VARIABILE ALEATORIA è una funzione $$ X : (\Omega, \ Algebra, P) \to \mathbb{R} \text{ tale che }\forall \ A\subset \mathbb{R} $$misurabile vale che :
$$X^{-1}(A)=\{\omega \in \Omega / X(\omega)\in A \} \in \text{Algebra}$$

### Legge di probabilità
Data una variabile aleatoria $X:(\Omega, Algebra, P)\to \mathbb{R}$ si chiama *LEGGE DI PROBABILITÀ* di X la funzione : $P_x :\{\text{ insieme  misurabile di } \mathbb{R}\} \to [0, 1]\\text{ definita da } P_x(A)=P(X\in A)=P(X^{-1}(A))​$

> [!NOTE] Osservazione
> Non è necessariamente importante sapere chi sia $\Omega$ e la variabile aleatoria ma è importante conoscere la legge di probabilità.

La legge di probabilità è una probabilità su $\mathbb{R}$.

## Variabili aleatorie equidistribuite

Due variabili aleatorie $\mathbf{X}$ e $\mathbf{Y}$ a valori reali si dicono *EQUIDISTRIBUITE* se hanno la stessa legge di [[Probabilità]] , ossia che $P_{\mathbf{X}}=P_{\mathbf{Y}}$

## Variabili aleatorie discrete

Una variabile aleatoria X a valori reali si dice *DISCRETA* se la sua legge di probabilità $P_\mathbf{X}$ è una probabilità su $\mathbb{R}$ discreta, ossia se esiste una [[funzione di massa]]. Esiste quindi una funzione di massa definita su un insieme finito e numerabile $\{x_1 , x_2, ..., x_n \}$ in $\mathbb{R}$ e $x_i \to p_i =P_\mathbf{X}(x_i)$, con $p_i\in [0,1]$ e $\sum_{x_i}{P_\mathbf{X}(x_i)}=1 ]$ .

## Variabili aleatorie con densità

Una variabile aleatoria $\mathbf{X}$ a valori reali si dice con *DENSITÀ* se la sua legge di probabilità $P_{\mathbf{X}}$ è una probabilità su $\mathbb{R}$ con [[Probabilità con densità|densità]]. Esiste quindi $f:\mathbb{R}\to[0,+\infty]$ , integrabile e tale che $\int_{-\infty}^{+\infty}{f(x) dx} = 1$, per cui per ogni $A \subset \mathbb{R}$ vale che $P_\mathbf{X}(A)=P(\mathbf{X}\in A)=\int_{A}{f(x) dx} ]$ .
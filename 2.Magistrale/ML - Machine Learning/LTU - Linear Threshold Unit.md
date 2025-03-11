---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Linear models - classification - LTU]]"
tags:
  - ML
Creation: 2025-03-04
---
L'**LTU** (Linear Threshold Unit) consente di definire un **iperpiano** che suddivide lo spazio dei dati in due regioni, ciascuna corrispondente a una classe. 

Gli **LTU** sono efficaci in molti contesti, ma hanno limitazioni nel separare dati non linearmente separabili.

Questo concetto è strettamente legato al [[Statistical Learning Theory - Vapnik]].

L'iperpiano separa le due classi generando un insieme di **dicotomie**, che corrispondono al numero di possibili ipotesi $h$ nello **spazio delle ipotesi** $H$.

Più formalmente, il numero di dicotomie rappresenta la capacità del modello di separare il dataset in differenti modi, e questa capacità è direttamente legata alla **[[VC-Dimension]]** (Vapnik-Chervonenkis Dimension), una misura fondamentale della complessità di un modello di apprendimento.
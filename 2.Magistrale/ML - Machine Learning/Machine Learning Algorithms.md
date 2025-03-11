---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning]]"
tags: 
Creation:
---

Gli **algoritmi di learning** definiscono il campo del _[[Machine learning]]_. 
Questi algoritmi consentono a una macchina di estrarre conoscenza dai dati, ovvero di apprendere informazioni basandosi sui dati a cui ha accesso.

The learning algorithm is based on *data*, **task** and **model**.

The heuristic is search through the hypothesis space $H$ of the best hypothesis.
![[hypothesis space.png]]

Gli __algoritmi di learning__ possono essere suddivisi in varie categorie come :

1. [[Supervised Learning]]
2. [[Unsupervised Learning]]
3. [[Semi-supervised Learning]]
4. [[Reinforcement Learning]]

Indipendentemente dalla categoria i passi sono solitamente
1. __Fase di apprendimento__ (training o fitting):  in cui si ricerca un ipotesi partendo dai dati conosciuti, insieme dei quali è chiamato __training set__.

2. __Fase di inferenza__ (o stima): in cui viene utilizzata l'ipotesi generata dal modello per predire nuovi dati. 

I dati predetti si possono confrontare con un altro set di dati che si assumono corretti, solitamente detto __test set__, per avere informazioni sull'ipotesi predittiva scelta e quindi sulle capacità di ___[[Generalization|generalizzazione]]___, ossia la capacita di ottenere buone prestazioni su dati non presenti nel training set.
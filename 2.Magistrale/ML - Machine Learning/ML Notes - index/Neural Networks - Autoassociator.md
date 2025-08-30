---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks|NN]]"
tags:
  - ML
  - "#NN"
Creation: 2025-03-08
---
Gli ***auto-associatori*** sono [[Neural Networks|reti neurali]] ad [[Unsupervised Learning|apprendimento non supervisionato]] che imparano a riprodurre come output il proprio input. 
Sono specializzati nei pattern associativi, rendendoli robusti a rumore e dispersione, e funzionano anche se l'input è corrotto, parziale o rumoroso.

Gli auto associatori sono definiti da una funzione di associazione $f$ con cui un determinato input $x$ viene mappato in un output $r$, cercando di minimizzare la distanza tra i pattern memorizzati e quelli ricostruiti.

Esempi di autoassociatori sono:
- **Reti di Hopfield**: sono reti completamenti connesse con pesi simmetrici, in grado di memorizzare un numero finito di pattern stabili.
- **Memorie associative di Kanerva**: utilizza una [[Machine learning - Data and concept representation#Concept representation|rappresentazione distribuita]] per memorizzare e rappresentare le associazioni
- **[[Neural Networks - Autoencoder|Autoencoder]]** : Reti neurali usate nell'ambito deep con una struttura encode-decoder
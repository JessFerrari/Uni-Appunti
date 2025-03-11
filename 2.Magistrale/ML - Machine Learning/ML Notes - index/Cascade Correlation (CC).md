---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Issues in training]]"
tags:
  - ML
  - NN
Creation: 2025-02-06
---
Questo è un algoritmo incrementale che partendo da una rete piccola minimale aggiunge unità durante il training fino a quando non raggiunge un errore piccolo.

Impara sia i pesi della rete che la topologia della rete stessa.

Si può dire che determina in modo automatico la topologia della rete e permette quindi di trattare con uno spazio delle ipotesi flessibile nella dimensione.

Allena una singola unità ad ogni step.

Ogni unità aggiunta serve per ridurre l'errore residuo dell'output e per risolvere un "sotto problema". Quindi un'unità diventa un "feature-detector" permanente.

- Per evitare i massimi locali si usa il ***Pooling***: vengono allenate diverse hidden units e poi tra queste viene scelta la migliore.

- si può considerare un algoritmo greedy in quanto arriva a convergenza con un numero minimi di unità ma può portare ad overfitting e si deve quindi [[Regularization|regolarizzare]].


# Algoritmo
---
Si parte con una rete minimale $N_{0}$ senza hidden units.

 1. Training di $N_{0}$
 2. Calcolare l'errore di $N_{0}$ 
 3. Se $N_{0}$ non risolve il problema aggiunge un hidden unit e si va alla rete $N_{1}$
 4. i pesi i questa unità si calcolano massimando la correlazione tra l'output dell'unità aggiunta e l'errore residuo di $N_{0}$ 
 5. Dopo l'allenamento il peso viene congelato e negli step successivi non viene mai cambiato
 6. Si fa lo stesso su $N_{1}$ e sulle future unità fino a quando non si trova il numero adeguato che risolva il problema

![[CC.png]]

L'algoritmo lavora sia minimizzando l'errore totale con LMS sia massimizzando la correlazione del nuovo candidato con l'errore residuo.

$S=\sum_{k}|\sum_{p}(o_{p}-\text{mean}_{p}(o_{p}))(E_{p,k}-\text{mean}_{p}(E_{p,k}))|$

Dove:
- $E_{p,k}=(o_{p,k}-d_{p,k})$ : errore residuo nell'output layer con il pattern p
- $o_{p}$ : il nuovo candidato aggiunto alla rete
---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine Learning Model]]"
tags:
  - ML
Creation: 2025-03-09
---
I __[[Machine Learning Model|modelli]] parametrici__ di [[Machine Learning|macchine learning]] sono generati da un [[Machine Learning Algorithms|algoritmo di learning]]. 

Sono caratterizzati da un numero fisso di __parametri__ che vengono imparati durante la fase di training.

Questo approccio elimina la necessità di mantenere in memoria l'intero dataset durante l'inferenza in quanto il modello è rappresentato da un ipotesi analitica esplicita. 

Gli algoritmi che costruiscono questi tipi di modelli sono detti anche "__eager__".

Vantaggi:  
- __Efficienza__: L'uso di un numero limitato di parametri rende questi algoritmi generalmente più rapidi sia durante l'addestramento che nell'inferenza.  
- __Semplicità__: Il modello è spesso più semplice da interpretare e implementare rispetto ad altre metodologie.  

Svantaggi:  
- __Rigidità__: Non sempre riescono a catturare relazioni complesse o pattern non lineari nei dati.  
- __Possibile sottoparametrizzazione__: Se il modello è troppo semplice rispetto alla complessità dei dati, le prestazioni potrebbero risentirne.  

Tra gli esempi più comuni di algoritmi parametrici troviamo:  
- __[[Linear models - regression|Regressione lineare]]__  
- __Regressione logistica__  
- __Modelli lineari generalizzati__  
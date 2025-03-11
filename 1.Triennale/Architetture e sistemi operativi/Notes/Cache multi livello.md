---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Argomento 1]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
## Cache multi livello

Per mitigare il problema in caso di miss nel primo livello della cache si possono aggiungere ulteriori livelli, in questo modo la miss penalty per la cache L1 non sarà altro che l'access time nella cache L2 che sarà estremamente inferiore rispetto al tempo di accesso alla RAM.

Con un sistema di cache multi livello i cicli di stallo a causa della memoria possono essere ridefiniti come i cicli di stallo provocati da tutti i livelli di cache :

$CPI_{stall}=MissRate_{L1}*MissPenalty_{L1}+GlobalMiss_{L2}*MissPenalty_{L2}+...$

Si può pensare al global miss rate come alla probabilità che si arrivi ad avere un miss in tutti i livelli antecedenti a quello preso in considerazione , per esempio si suppone di avere un livello $L_N$ con N > 1 :

$GlobalMiss_{LN}=MissRate_{L1}*MissRate_{L2}*...*MissRate_{LN}$

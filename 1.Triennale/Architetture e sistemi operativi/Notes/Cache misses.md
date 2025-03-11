---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Cache]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
## Tipi di cache misses

Si possono categorizzare i miss in diversi modi :

- Miss obbligatori : causati da un primo accesso ad un blocco non ancora presente in cache
- Miss di capacità : avvengono quando la cache non può contenere tutti i blocchi di cui si ha bisogno , perciò alcuni vengono svuotati e riutilizzati
- Miss di conflitto : avvengono solo nella direct mapped e nella parzialmente associativa

Una cache miss stalla l'intero  processore mentre esso aspetta di ricevere i dati che necessita.  Quando avviene una cache miss viene detto al livello successivo di memoria di leggere il dato mancante, si aspetta per il risultato, si aggiorna il blocco di cache con i dati ricevuti e si riesegue l'istruzione.

Ci sono degli algoritmi che possono avere impatto sulla potenzialità della cache per avere miss rate più basso e avere prestazioni migliori
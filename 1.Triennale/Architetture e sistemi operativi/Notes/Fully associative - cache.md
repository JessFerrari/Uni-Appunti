---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Cache]]"
tags:
  - AESO
Creation: 2025-02-24
---
### Fully associative

Una cache completamente associativa è costituita da un unico blocco set a B blocchi e vie e quindi un indirizzo di memoria può essere mappato in una qualsiasi di queste vie.

![[fullyassociative.png]]


La figura mostra una cache associativa con 4 blocchi e 2 parole per blocco. Alla richiesta di un dato, devono essere effettuati 4 confronti di tag con i confrontatori che poi verranno messi in and con il bit di integrità e nel mentre il block offset seleziona quale delle due parole del blocco prende grazie ad un altro mux. Quello che usciva in and dal tag viene mandato in un encoder che ne determina la posizione e fa da controllo per il multiplex che seleziona la parola necessaria e fa uscire il dato.

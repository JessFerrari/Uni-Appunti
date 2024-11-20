---
Subject: "[[Indice - Basi di dati]]"
tags:
  - BD
Creation: 2024-02-08
---
>Una [[Indice - Basi di dati|BASE DI DATI]] è un insieme organizzato di dati per il supporto allo svolgimento di attività (si un ente, azienda, ufficio, persona).
>Una [[Base di dati|base di dati]] è una tecnologia per la gestione delle attività quotidiane e la loro organizzazione.

Per utilizzare una base di dati si devono raccogliere  informazioni e legarle.

Raccogliendo dati si possono analizzare i dati e prendere decisioni in quanto posso vedere i vari comportamenti nel periodo DataWarehouse. Queste servono per prendere decisioni e fare previsioni, lavorano su molti dati anche non aggiornati.

Nelle basi di dati i dati devono essere aggiornati in modo immediato e le operazioni devono avvenire in maniera atomica per garantire consistenza.

Va inoltre gestita la [[Concorrenza|concorrenza]].

Ci sono 3 persone coinvolte nella costruzione di una base di dati:
- il committente, che può essere un dirigente o un operatore, 
- il fornitore,
- l’amministratore del [[DBMS|DBMS]].

Per la rappresentazione delle basi di dati si usano __tabelle__. 
Una tabella è un insieme di dati strutturati e omogenei e collegati tra loro.

Le proprietà vanno stabilite all’inizio in modo da progettare correttamente la tabella.

Non avere duplicati in una tabella vuol dire che non posso avere due righe uguali.

![[01_tabelle.png]]

Il [[Modello relazionale]] è il più diffuso fra i DBMS commerciali come schema di organizzazione dei dati.
Il meccanismo di astrazione fondamentale è la relazione (tabella), sostanzialmente un insieme di record con campi elementari.

Lo schema di una relazione ne definisce il nome e descrive la struttura dei possibili elementi della relazione (insieme di attributi con il loro tipo).

CARATTERISTICHE :
- Atomicità delle operazioni
- Consistenza dei dati
- Aggiornamento immediato
- Dati pochi ma aggiornati
- Dati protetti in accesso


[[Esempi database relazionale]]

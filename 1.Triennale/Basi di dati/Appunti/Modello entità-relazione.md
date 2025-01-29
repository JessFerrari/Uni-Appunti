---
Subject: "[[Indice - Basi di dati]]"
tags:
  - BD
Creation: 2024-02-14
---
Il modello entità-relazione è un [[Modelli dei dati|modello per la modellazione di dati]] che a differenza del [[Modello ad oggetti|modello ad oggetti]] non tratta di metodi, gerarchie, collezioni e tipi.

___Definisce un meccanismo per modellare direttamente le associazioni, in particolare quelle non binarie e con proprietà___ 

Prevede 2 meccanismi di astrazione: 
- uno per le entità e le loro proprietà
- uno per le loro associazioni, chiamate relazioni

Le collezioni sono chiamate _tipi di entità_ e gli attributi possono assumere solo valori primitivi.

Il formalismo grafico sono _diagrammi ER_ in cui:
- i rettangoli rappresentano tipi di entità
- gli archi con un rombo in mezzo le relazioni. Nel rombo c'è scritta l'etichetta della relazione e nella parte tra il rombo e il tipo di entità è presente il (min:max), che rappresenta quante entità di quel tipo possono partecipare alla relazione.
	![[Pasted image 20240215031220.png]]
	Esempio di un diagramma ER

Il rettangolo doppio rappresenta un tipo di entità debole, i cui elementi dipendono da quelli di tipo di entità con cui sono in relazione.

Le relazioni possono essere anche non binarie e avere proprietà

Questo è l'[[Esempio biblioteca universitaria|esempio della biblioteca]] con lo scema entità relazione
![[Pasted image 20240215031529.png]]
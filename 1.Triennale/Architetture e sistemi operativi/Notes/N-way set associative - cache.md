---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Cache]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
Si verifica trashing quando si hanno sempre miss e alla fine la lettura diventa lunga come quella in memoria

PRO :

- È semplice da realizzare
- Nel caso di cache hit è molto veloce

CONTRO :

- È molto rigido
- Possono essere presenti molti conflitti

### N-way set associative

Una cache parzialmente associativa ad N vie riduce i conflitti prevedendo N blocchi in ciascun set dove il dato mappato in tale set può trovarsi : ogni indirizzo di memoria viene mappato in uno specifico set ma può essere copiato in uno degni N blocchi di tale set. Si potrebbe quindi anche dire che una cache a mappatura diretta equivale ad una cache parzialmente associativa ad una sola via.![[nwayassociative.png]]

In figura ogni set contiene due vie, ognuna delle quali contiene da un blocco con bit di validità, tag e due parole. La cache legge i blocchi da entrambe le vie del set selezionato e controlla i tag e i bit di validità. Se si ottiene una hit in una delle due vie un mux seleziona quale delle parole scegliere grazie al block offset. La cache parzialmente associativa ha solitamente dei tassi di miss inferiori rispetto a quella a mappatura diretta ma sono tuttavia più lente e costose a causa dei mux e comparatori.


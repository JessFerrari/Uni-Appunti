---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Sistemi di IO]]"
tags:
  - AESO
Creation: 2025-02-24
---
### CANALE DI COMUNICAZIONE BUS

È una collezione di linee, trattate come un solo filo, a cui sono connesse entità e le prestazioni dipendo dalla lunghezza e quanti device posso attaccarci.

Tra vari bus si ha il system bus quello che aggancia i dispositivi con la memoria, i fili sono divi per i vari compiti.

La MMU ha a che fare con gli indirizzi di memoria e fa comunicare la memoria con il sistema di i/o mentre la DMA fa comunicare il dispositivo con la memoria.

I bus si suddividono in indirizzi, dati e controllo.Sono classificabili come:
- i/o bus
- Backplane bus
- System bus (veloce e ogni architettura ha il suo)


Per disegnare un bus per un determinato sistema è importante ottimizzare le prestazioni e implementare la standardizzazione.

Gli altri due sono meno veloci e standardizzati, basso cosso e prodotti in serie, hanno il vantaggio che si possono attaccare più dispositivi.

Per progettare un bus servono un'insieme di domande:
- Ha un clock? (bus sincroni o asincroni)
- Quanto è ampio? (quanti fili deve avere, quanto spazio deve occupare? Il system bus ha un'ampiezza che può caricare tanti blocchi cache,quindi è probabili che l'ampiezza sia almeno per 4/8 parole di memoria)
- Come vengono eseguite le operazioni di acquisizione e rilascio?
	- Atomic-transactions : chi lo acquisisce inizia la transazione e non lo lascia fino a quando non l'ha finita. Ci possono essere tempi morti e non viene utilizzato al pieno.
	- Split-transaction
- Chi decide chi acquisisce il bus?

## Classificazione dei BUS

![[Pasted image 20250224112513.png]]![[Pasted image 20250224112527.png]]

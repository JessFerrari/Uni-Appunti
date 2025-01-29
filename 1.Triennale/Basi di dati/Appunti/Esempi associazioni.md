---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Conoscenza concreta]]"
tags:
  - esempio
  - BD
Creation: 2024-02-12
---
# Associazione tra studenti ed esami


![[10-1_esempio.png]]
Ogni esame riguarda uno ed un solo studente:

- Univocità (freccia singola) e totalità (assenza del taglio).

Si ha invece per lo studente:

- Vincolo di parzialità (taglio) e assenza di univocità sugli esami (freccia doppia) superati da uno studente.

![[10-2_esempio.png]]

Uno studente può sostenere zero o più esami. Un esame riguarda esclusivamente uno studente.

Cosa succede se al posto di rappresentare materia come “fatto”, quindi come proprietà creiamo la sua propria classe?
![[10-3_esempio.png]]

In questo caso possiamo anche ampliare l’esempio:
![[10-4_esempio.png]]
Per dare informazione sulla cardinalità in questo caso ci serviranno 4 valori: minimo e massimo per ciascuna delle due direzioni.



## [[Modello ad oggetti|Modello a oggetti: le associazioni]]

Le associazioni si modellano con un costrutto apposito (la freccia).
![[10-5_esempio.png]]

Le associazioni possono anche avere delle proprietà.
![[10-6_esempio.png]]

Possono inoltre essere ricorsive
![[10-7_esempio.png]]

Esempio: reificazione delle associazioni molti a molti (come si gestisce in maniera pratica una associazione molti a molti), si crea una nuova classe.
![[10-8_esempio.png]]

Si può fare una reificazione anche delle associazioni con proprietà indipendentemente da quella che è la molteplicità, nel caso in cui l’associazione abbia proprietà si trasforma in una classe con le proprietà.
![[10-9_esempio.png]]

### Associazione non binaria

Per semplicità non diamo una notazione per le associazioni non binarie. Trasformeremo le associazioni ternarie in binarie.

Per farlo usiamo una nuova classe con una associazione tra tutte che sarà multivalore ma con i vincoli.
![[10-10_esempio.png]]
	Trasformazione di associazione ternaria in binarie (associazione fra Voli, Passeggeri e Posti). L’associazione è multivalore rispetto ad ogni collezione, poiché ogni singolo volo, passeggero, e posto, partecipa in generale a diverse istanze di associazione, ma con i vincoli che, in un singolo volo, ogni posto è associato al più ad un passeggero ed ogni passeggero può occupare al più un posto



Le ___associazioni ricorsive___ sono relazioni binarie fra gli elementi di una stessa collezione. 
Occorre etichettare la linea non solo con il nome dell’associazione, ma anche con dei nomi per specificare il ruolo che hanno le due componenti in un’istanza di associazione.


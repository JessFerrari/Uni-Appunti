---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBS - Ordinamento]]"
tags:
  - BD
Creation: 2024-03-04
---
Per fare il join posso effettuare 2 for annidati.
![[Pasted image 20240304235131.png]]
Prendo tutti i record della prima relazione e poi  quella della seconda li confronto e se sono uguali li aggiungi.

Il costo di esecuzione dipende dallo spazio a disposizione in memoria centrale.

Nel caso base in cui vi sia 1 buffer per R e 1 buffer per S, bisogna leggere 1 volta $R$ e $Nrec(R)$ volte $S$, ovvero tante volte quante sono le tuple della relazione esterna, per un totale di $Npag(R) + Nrec(R) * Npag(S) I/O$

Se è possibile allocare $Npag(S)$ buffer per la relazione interna il costo si riduce a $Npag(R) + Npag(S)$

Questo algoritmo è efficiente se si hanno un numero di buffer a disposizione che copre il numero di pagine di S 

Bisogna saper scegliere quale tabella mettere per esterna e quale per interna.
Per ridurre il costo bisogna mettere quella più piccola come esterna (A destra)

Se dopo la join c'è il group by si usa in quanto non si ha bisogna che siano ordinate ma solo consecutive

# PageNestedLoop
Non è il miglior algoritmo perché analizza tutti i record di ogni pagina, si potrebbe migliorare facendolo sul numero di pagine e non sui record

# IndexNestedLoop
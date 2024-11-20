---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS - Indici]]"
tags:
  - BD
Creation: 2024-02-29
---
Un albero binario di ricerca è un albero binario etichettato, in cui per ogni nodo, il sottoalbero sinistro contiene solo etichette minori di quella del nodo.
Il sottoalbero destro etichette maggiori.

Il tempo di ricerca (e inserimento), pari alla profondità: 
- logaritmico nel caso “medio” (assumendo un ordine di inserimento casuale)
![[Pasted image 20240229210908.png]]


Ogni nodo ha (fino a) $P$ figli e (fino a) $P-1$ etichette, ordinate.
Un albero di ricerca di ordine $p$ è un albero i cui nodi contengono al più $p-1$ *search value* e $p$ *puntatori* nel seguente ordine: 
	$<P_1, K_1, P_2, K_2, .., P_{q-1}, K_{q-1}, P_q>$ con $q ≤ p$.
Ogni $P_i$ è un puntatore ad un nodo figlio (o un puntatore nullo) e ogni $K_i$ è un search value appartenente ad un insieme totalmente ordinato.

![[Pasted image 20240229213046.png]]

###### Vincoli fondamentale albero di ricerca
Ogni albero di ricerca deve soddisfare due vincoli fondamentali:
- in ogni nodo $K_1 < K_2 < ..... < K_{q-1}$; 
- per tutti i valori di $X$ presenti nel sottoalbero puntato da $P_i$, vale la seguente relazione:
	$K_{i-1} < X < K_i$ , per $1 < i < q$ 
	$X < K_i$ per $i = 1$
	$K_{i-1} < X$ per $i = q$

Un albero di ricerca può essere utilizzato per cercare record memorizzati su disco.

Ogni ricerca/modifica comporta la visita di un cammino radice foglia.

I valori di ricerca (search value) possono essere i valori di uno dei campi del file (search field).

 Ad ogni valore di ricerca è associato un puntatore al record avente quel valore (oppure al blocco contenente quel record) nel file di dati. 
 
 L'albero stesso può essere memorizzato su disco, assegnando ad ogni nodo dell'albero una pagina. 
 
 Quando un nuovo record deve essere inserito, l’albero di ricerca deve essere aggiornato includendo il valore del campo di ricerca del nuovo record, col relativo puntatore al record (o alla pagina che lo contiene), nell’albero di ricerca.

Per inserire e cancellare valori di ricerca nell’ (dall’) albero di ricerca sono necessari specifici algoritmi che garantiscano il rispetto dei due vincoli fondamentali. 

In generale, tali algoritmi non garantiscono che un albero di ricerca risulti sempre bilanciato ossia che i nodi foglia siano tutti allo stesso livello. 

Per rendere vera quest'ultima si usano i $B$-alberi e i $B^+$-alberi.
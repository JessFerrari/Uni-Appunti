---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS - Indici]]"
tags:
  - BD
Creation: 2024-02-29
---
# B-albero

Un $B$-tree di ordine $p$, se usato come struttura di accesso su un campo chiave per la ricerca di record in un file di dati, deve soddisfare le seguenti condizioni: 

- ogni nodo interno del $B$-albero ha la forma: $<P_1, <K_1, Pr_1>, P_2, <K_2, Pr_2>, ..., <K_{q-1}, Pr_{q-1}>, P_q>$ con $q ≤ p$. 

1. $P_i$ è un **tree pointer** (puntatore ad un altro nodo del $B$-albero), 
2. $K_i$ è la chiave di ricerca 
3. $Pr_i$ è un **data pointer** (puntatore ad un record il cui campo chiave di ricerca è uguale a $K_i$ o alla pagina che contiene tale record);
	- Per ogni nodo, si ha che: $K_1 < K_2 < .... < K_{q-1}$ 
	- ogni nodo ha al più p tree pointer;

Per tutti i valori $X$ della chiave di ricerca appartenenti al sottoalbero puntato da $P_i$, si ha che: 
	- $K_{i-1} < X < K_i$ per $1 < i < q$; 
	- $X < K_i$ per $i = 1$; 
	- $K_i-1 < X$ per $i = q$; 

La radice ha almeno due tree pointer, a meno che non sia l'unico nodo dell'albero.
Ogni nodo, esclusa la radice, ha almeno $⎡p/2⎤$ tree pointer.
Un nodo con $q$ tree pointer, $q ≤ p$, ha $q-1$ campi chiave di ricerca (e $q-1$ data pointer).
Tutti i nodi foglia sono posti allo stesso livello (i nodi foglia hanno la stessa struttura dei nodi interni, ad eccezione del fatto che tutti i loro tree pointer $P_i$ sono nulli)

Svantaggio: ricerca per valori complicata perché non si ha modo di saltare da un dato ad un altro.

![[Pasted image 20240229215647.png]]
# B+ -albero

Un $B^+$-tree è un $B$-albero in cui _i data pointer sono memorizzati solo nei nodi foglia dell’albero_ e le foglie sono in relazione tra loro.

La struttura dei nodi foglia differisce dal B-tree quindi da quella dei nodi interni.

_Se il campo di ricerca è un campo chiave_, i nodi foglia hanno per ogni valore del campo di ricerca una entry ed un puntatore ad un record.

_Se un campo di ricerca non è un campo chiave_, i puntatori indirizzano un blocco che contiene i puntatori ai record del file di dati, rendendo così necessario un passo aggiuntivo per l’accesso ai dati.

_I nodi foglia di un $B^+$-tree sono generalmente messi fra loro in relazione_ (cioè viene sfruttato nel caso di range query). 
Essi corrispondono al primo livello di un indice. 
I nodi interni corrispondono agli altri livelli di un indice.

Alcuni valori del campo di ricerca presenti nei nodi foglia sono ripetuti nei nodi interni per guidare la ricerca.![[Pasted image 20240229071501.png]]

La struttura dei _nodi interni_ (di ordine $p$) di un B+-tree è la seguente:

1. Ogni nodo interno del B+-tree ha la forma: $<P_1, K_1, P_2, K_2, ..., P_{q-1}, K_{q-1}, P_q>$ con q≤p
2. Per ogni nodo interno si ha che: $K_1<K_2<...<K_{q-1}$
3. Ogni nodo interno ha al più $p$ tree pointer
4. Per tutti i valori $X$ della search key nel sottoalbero puntato da $P_i$ si ha che
    - $X \leq K_i$ per i=1
    - $K_{i-1} < X \leq K_i$ per 1<i<q $K_{i-1} \leq X$ per i=q
5. Ogni nodo interno esclusa la radice ha almeno $\lceil p/2 \rceil$ tree pointer. La radice ha almeno 2 tree pointer se è un nodo interno.
6. Un nodo interno con $q$ tree pointer, con q≤p, ha q-1 campi di ricerca.

La struttura dei _nodi foglia_ (di ordine $p_{leaf}$) di un B+-albero è la seguente:

1. Ogni nodo foglia è della forma: $<<K_1, Pr_1>, <K_2, Pr_2>, ..., <K_q, Pr_q> P_{next}>$ dove $q \leq p_{leaf}$ e per ogni nodo si ha $K_1<K_2<...<K_q$
    - $P_{next}$ è un tree pointer che punta al successivo nodo foglia del $B^+$-tree
    - $Pr_i$ è un data pointer che punta al record con valore del campo di ricerca uguale a $K_i$ o ad un blocco contenente tale record (o ad un blocco di puntatori ai record con valore del campo di ricerca uguale a $K_i$ se il campo di ricerca non è una chiave.
2. Ogni nodo foglia ha almeno $\lceil p_{leaf}/2 \rceil$ valori
3. Tutti i nodi foglia sono dello stesso livello.
![[Pasted image 20240229071600.png]]![[Pasted image 20240229071645.png]]

A simple  B+ tree example linking the keys 1–7 to data values d1-d7. The linked list (red) allows rapid in-order traversal. This particular tree's branching factor is b=4. Both keys in leaf and internal nodes are colored gray here.



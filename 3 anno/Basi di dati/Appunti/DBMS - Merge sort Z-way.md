---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBS - Ordinamento]]"
tags:
  - BD
Creation: 2024-03-04
---
## Z-way Sort-Merge

Questo è l’algoritmo di sorting più utilizzato dai DBMS ed ha un costo di $N*log(N)$

Supponiamo di dover ordinare un input che consiste in un file di NP pagine e di avere a disposizione solo NB < NP buffer in memoria centrale.


 L’algoritmo opera in 2 fasi: 
 -  Sort interno: si leggono una alla volta le pagine del file e i record di ogni pagina vengono ordinati facendo uso di un algoritmo di sort interno (es. Quicksort). Ogni pagina così ordinata, detta anche “run”, viene scritta su disco in un file temporaneo 
 - Merge: operando uno o più passi di fusione, le run vengono fuse, fino a produrre un'unica run

Per semplicità consideriamo il caso base a Z = 2 vie, e supponiamo di avere a disposizione solo NB = 3 buffer in memoria centrale

![[Pasted image 20240304232154.png]]

## Complessità

$O(2NP(⎡ log2NP ⎤)+1)$

 Consideriamo per semplicità solo il numero di operazioni di I/O.
 
 Nel caso base Z = 2 (e NB = 3) si può osservare che: 
- Nella fase di sort interno si leggono e si riscrivono NP pagine 
- Ad ogni passo di merge si leggono e si riscrivono NP pagine (2 * NP) 
- Il numero di passi fusione è pari a ⎡log2 NP ⎤, in quanto ad ogni passo il numero di run si dimezza
- Il costo complessivo è pertanto pari a 2 * NP * ( ⎡ log2NP ⎤ + 1)


Esempio: 
	per ordinare NP = 8000 pagine sono necessarie circa 224.000 (2*8000*( ⎡ log28000⎤ + 1)) operazioni di I/O; 
	se ogni I/O richiede 20 msec, il sort richiede 4.480 secondi, ovvero circa 1h 15 minuti! 
	In realtà se NP non è una potenza di 2 il numero effettivo di I/O è leggermente minore di quello calcolato, in quanto in uno o più passi di fusione può capitare che una run non venga fusa con un’altra


## Osservazioni ed utilità

Una prima osservazione è che nel passo di sort interno, avendo a disposizione NB buffer, si possono ordinare NP pagine alla volta (anziché una sola), il che porta a un costo di 2 * NP * ( ⎡ log2 (NP/NB) ⎤ + 1) 

Esempio: 
	con NP = 8000 pagine e NB = 3 si hanno ora 208.000 I/O 
	Miglioramenti sostanziali si possono ottenere se, avendo NB > 3 buffer a disposizione, si fondono NB – 1 run alla volta (1 buffer è per l’output) 
	In questo caso il numero di passi di fusione è logaritmico in NB – 1, ovvero è pari a 2 * NP * ( ⎡ logNB-1 (NP/NB) ⎤ + 1) 
	Esempio: con NP = 8000 pagine e NB = 11 si hanno 64000 I/O, per un tempo stimato pari a 1280 sec

Utilità:

Oltre che per ordinare le tuple, il Sort può essere utilizzato per:
- Query in cui compare l’opzione DISTINCT, ovvero per eliminare i duplicati 
	Un'approccio banale è quella di utilizzare l'ordinamento in quanto dopo aver ordinato la tabella in base all'attributo interessato si eliminano i duplicati, stampando solo il primo di ogni valore uguale
- Query che contengono la clausola GROUP BY
	

# Sort Merge Join
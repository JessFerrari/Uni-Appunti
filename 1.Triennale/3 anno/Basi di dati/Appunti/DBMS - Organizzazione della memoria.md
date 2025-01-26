---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS]]"
tags:
  - BD
Creation: 2024-02-29
---
Tipi di organizzazioni:
- Seriali o Sequenziali 
- Per chiave 
- Per attributi non chiave 

Parametri che caratterizzano un’organizzazione: 
- Occupazione di memoria 
- Costo delle operazioni di: 
	- Ricerca per valore o intervallo
		- Le tabelle hash ottime per valore ma non per valore 
	- Modifica 
	- Inserzione 
	- Cancellazione


# Organizzazione seriale

***Organizzazione seriale (heap file)***: i dati sono memorizzati in modo disordinato uno dopo l'altro. 

Semplice e a basso costo di memoria ma poco efficiente, devo scorrerlo tutto.
Va bene per pochi dati.
Se devo sempre leggere tutta la tabella è vantaggiosa.

Questa è l'organizzazione standard di ogni DBMS.
![[Pasted image 20240229070527.png]]

# Organizzazione sequenziale

***Organizzazione sequenziale***: i dati sono ordinati sul valore di uno o più attributi.

Posso usare quindi la ricerca binaria. se faccio poche inserzioni e molte ricerche è vantaggiosa.

Le ricerche sono più veloci rispetto all'organizzazione seriale.
Nuove inserzioni fanno perdere l'ordinamento.

Costo di ricerca
	Ricerca binaria su file di dati ordinato richiede $\log_2(b)$ accessi a blocco/pagina.
	Se il file contiene $b_i$ blocchi, la localizzazione di un record richiede la ricerca binaria nel file e l'accesso al blocco che contiene il record, quindi richiede $\log_2 (b_i) + 1$ accessi a blocco/pagina.

La ricerca binaria si fa direttamente sui i file e quindi dipende dal numero di pagine.

![[Pasted image 20240229070544.png]]
##### Esempio:
File ordinato con r = 30.000 record.
Dimensioni dei blocchi/pagine su disco B = 1024 byte 
I record hanno dimensione fissa e sono indivisibili, lunghezza R = 100 byte
Il fattore di blocco/pagine è $$bfr = ⌊ (B/R) ⌋ = ⌊ (1024/100) ⌋ ={10\ record\ per\  blocco}/{ pagine}$$
Numero blocchi necessari $$ b = ⌈(r/bfr) ⌉ = ⌈(30000/10) ⌉ = 3000\ blocchi$$
Una ricerca binaria su file dati richiede circa $$⌈ log2b ⌉ = ⌈log23000 ⌉ = 12\ accessi\ ai\ blocchi/pagine$$

Inserzione efficiente di un nuovo record in una pagina : 
	Si lascio dello spazio vuoto nelle pagine e nel momento in cui devo inserire un nuovo record cerco la pagina che ha i record più simili, inserisco quello nuovo e poi riordino solo quella li. 
	Se si riempie devo ridistribuire i record. 

# Organizzazioni per chiavi 

Noto il valore di una chiave, si vuole trovare il record di una tabella con qualche accesso al disco (l'ideale sarebbe 1 accesso). 
Utile per migliorare il meccanismo di ricerca.

L'hash va usata sulle pagine 

Alternative: 
- Metodo procedurale ([[DBMS - Hash file|hash]]) o tabellare ([[DBMS - Indici|indice]]) 
- Organizzazione statica o dinamica.
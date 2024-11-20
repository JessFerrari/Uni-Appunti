---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS - Organizzazione della memoria]]"
tags:
  - BD
Creation: 2024-02-29
---
# Indice
Un **indice** è un _insieme ordinato_ di coppie $(k, r(k))$ dove:
- $k$ è un valore della chiave
- $r(k)$ è un riferimento al record con chiave $k$

L'indice può essere utilizzato con un [[albero binario di ricerca]]. Il problema è che questo può essere sbilanciato.

Per non avere sbilanciamento si possono usare i B

L’indice è di solito gestito con un’opportuna struttura ad albero detta **[[DBMS - B-tree|B+ -albero]]**, la struttura più usata dai DBMS.

Gli indici possono essere multi-attributi.

L’indice è una struttura che contiene informazioni sulla posizione di memorizzazione delle tuple sulla base del valore del campo _chiave_.

La _realizzazione di indici_ avviene tipicamente attraverso l’utilizzo di strutture ad albero multi-livello, in particolare [[DBMS - B-tree#B+ -albero|B+ alberi]].

Un indice può essere definito 

In una base di dati possono essere definiti più indici, sia primari che secondari. Averne tanti però vuol dire avere alti costi di aggiornamento
# Indice statico 
La struttura ad albero viene creata sulla base dei dati presenti nel DB e non più modificata, o comunque modificata periodicamente
# Indice dinamico
La struttura ad albero viene aggiornata ad ogni operazione sulla base di dati di inserimento o di cancellazione, preservando le prestazioni senza bisogno di riorganizzazioni

# Indice primario

Un _indice primario_ è un file ordinato i cui record sono di lunghezza fissa e sono costituiti da due campi:

- Il primo campo è lo stesso del _campo chiave di ordinamento_ (chiave primaria)  
- Il secondo campo è un puntatore a un blocco del disco

LA CHIAVE DI ORDINAMENTO DEL FILE SEQUENZIALE COINCIDE CON L ACHIAVE DI RICERCA DELL'INDICE , OSSIA CON LA CHIAVE PRIMARIA

Esiste un record nel file dell’indice per ogni blocco nel file di dati.
L'indice è la coppia chiave RID, il RID è mutevole, contiene la pagina e il suo slot
![[Pasted image 20240229071721.png]]


# Indice secondario

Un _indice secondario_ può essere definito su un _campo non chiave_ che è una [[Schema relazionale - Ricerca delle chiavi#Chiave candidata e attributo primo|chiave candidata]] ed ha valori univoci, o su un campo _non chiave_ con valori duplicati.

Il primo campo è dello stesso tipo del campo che non viene usato per ordinare il file ed è chiamato _campo di indicizzazione_.

Il secondo campo è un _puntatore_ a blocco oppure un puntatore a record (RID).

![[Pasted image 20240229071742.png]]


# Indici su chiavi esterne
Potrebbe essere utile l'utilizzo di indici su chiavi esterne per le query con il CASCADE, ossia per le cancellazioni a cascata.


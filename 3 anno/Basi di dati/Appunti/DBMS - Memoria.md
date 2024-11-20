---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Realizzazione DBMS]]"
tags:
  - BD
Creation: 2024-02-29
---
# Gerarchia delle memorie
La memoria di un sistema di calcolo è organizzata in una gerarchia. 
Al livello più alto memorie di piccola dimensione, molto veloci, e costose.
Scendendo lungo la gerarchia la dimensione aumenta, diminuiscono la velocità e il costo. 

**Prestazioni di una memoria**: dato un indirizzo di memoria, le prestazioni si misurano in termini di tempo di accesso, determinato dalla somma della latenza, ossia il tempo necessario per accedere al primo byte, e del tempo di trasferimento, ovvero il tempo necessario per muovere i dati.
$$Tempo di accesso = latenza + \frac{dimensione\ dati\ da \ trasferire}{velocità\ di\ trasferimento}$$
![[Pasted image 20240229053836.png]]

## Implicazioni per i DBMS

Un DB, a causa della sua dimensione, risiede normalmente su dischi, ed eventualmente anche su altri tipi di dispositivi.
I dati devono essere trasferiti in memoria centrale per essere elaborati dal DBMS.
Il trasferimento non avviene in termini di singole tuple, bensì di blocchi (o pagine, termine comunemente usato quando i dati sono in memoria).
Poiché spesso le operazioni di I/O costituiscono il bottleneck del sistema, si rende necessario ottimizzare l’implementazione fisica del DB, attraverso:
- Organizzazione efficiente delle tuple su disco • Strutture di accesso efficienti
- Gestione efficiente dei buffer in memoria 
- Strategie di esecuzione efficienti per le query


# Hard disk 

Un hard disk (HD) è un dispositivo elettro-meccanico per la conservazione di informazioni sotto forma magnetica, su supporto rotante a forma di piatto su cui agiscono delle testine di lettura/scrittura
![[Pasted image 20240229054037.png]]Include organi di registrazione, di posizionamento e di rotazione. 
Un’unità a dischi contiene una pila di dischi metallici che ruota a velocità costante ed alcune testine di lettura che si muovono radialmente al disco.
![[Pasted image 20240229054110.png]]Una traccia è organizzata in settori di dimensione fissa.
I settori sono raggruppati logicamente in blocchi, che sono l’unità di trasferimento. 
Trasferire un blocco richiede:
- un tempo di posizionamento delle testine
- un tempo di latenza rotazionale 
- tempo per il trasferimento (trascurabile)
	Esempi:
	- IBM 3380 (1980) : 2Gb, 16 ms, 8.3 ms, 0.8 ms/2.4Kb 
	- IBM Ultrastar 36Z15 (2001): 36GB, 4.2 ms, 2 ms, 0.02 ms/Kb


# Pagine 
Un blocco (o pagina) è una sequenza contigua di settori su una traccia, e costituisce l’unità di I/O per il trasferimento di dati da/per la memoria principale.

La dimensione tipica di una pagina è di qualche KB (4-64 KB).
Pagine piccole comportano un maggior numero di operazioni di I/O, pagine grandi tendono ad aumentare la frammentazione interna (pagine parzialmente riempite) e richiedono più spazio in memoria per essere caricate.
Il tempo di trasferimento di una pagina (Tt) da disco a memoria centrale dipende dalla dimensione della pagina (P) e dal transfer rate (Tr).

Esempio: con un transfer rate di 21.56 MB/sec e P = 4 KB si ha Tt= 0.18 ms, con P= 64 KB si ha Tt= 2.9 ms


Con il PID si trova la pagina 
# Località 
Per leggere un file da un MB servono (IBM Ultrastar 36Z15 ):
- 0,027 secondi se memorizzato in settori consecutivi (località spaziale) 
- 0,8 secondi se memorizzato in blocchi da 16 settori ciascuno (8KB) distribuiti a caso (128*(4,2+2+0,16)) 
- 12,7 secondi se memorizzato in blocchi da 1 settore ciascuno, distribuiti a caso (2048*(4,2+2+0,01))


# Gestore memoria permanente

![[Pasted image 20240229054609.png]]

Il gestore di memoria permanente fornisce della memoria permanente in termini di insiemi di file logici di pagine fisiche di registrazioni (blocchi), nascondendo le caratteristiche dei dischi e del sistema operativo.

#### Gestore del buffer
Il gestore del buffer si preoccupa del trasferimento delle pagine tra la memoria temporanea e la memoria permanente, offrendo agli altri livelli una visione della memoria permanente come un insieme di pagine utilizzabili in memoria temporanea, astraendo da quando esse vengano trasferite dalla memoria permanente al buffer e viceversa
	Area dell pagine :![[Pasted image 20240229054940.png]]
Si usa tabella associativa che collega l'id della pagina con la cella del buffer. di tale pagina si ha bisogno di sapere se è stata modificata. 
Se lo è va trasferita nel disco per garantire affidabilità sostituendola a quella vecchia. Per saperlo si usa il bit dirty/non dirty.
Il Pin count è quanto una pagina viene richiesta dalle applicazioni, aumentato quando la pagina viene richiesta e decrementato quando viene rilasciato.
Un'altra operazione importante è il *flush-Page* che mette a 0 il dirty count e scrive tutte le pagine in memoria. 
## Politiche di rimpiazzamento 
Nei sistemi operativi una comune politica adottata per decidere quale pagina rimpiazzare è la LRU (Least Recently Used), ovvero si rimpiazza la pagina che da più tempo non è in uso.
Nei DBMS, LRU non è sempre una buona scelta, in quanto per alcune query il “pattern di accesso” ai dati è noto, e può quindi essere utilizzato per operare scelte più accurate, in grado di migliorare anche di molto le prestazioni.

L' **hit ratio**, ovvero la frazione di richieste che non provocano una operazione di I/O, indica sinteticamente quanto buona è una politica di rimpiazzamento.
	Esempio: esistono algoritmi di join che scandiscono N volte le tuple di una relazione. 
	In questo caso la politica migliore sarebbe la MRU (Most Recently Used), ovvero rimpiazzare la pagina usata più di recente!

## Struttura di una pagina

La struttura *fisica* di una pagina è un insieme, di dimensione fissa, di caratteri.
La struttura *logica* comprende informazioni di servizio ed un'area che contiene le stringhe che rappresentano i record.

RID : Identificatore del record $\langle PID,\ record \rangle$
	![[Pasted image 20240229055315.png]]

Il formato tipico di una pagina in un DBMS è rappresentato da :
- Page header, in cui si tiene traccia di dove finisce la pagina
- Directory, che contiene un puntatore per ogni record nella pagina
- Free space 
- Record
![[Pasted image 20240229055452.png]]
Con la soluzione del puntatore per i record nella directory l'identificatore dei record (RID) è formato dalla coppia:
- PID : identificatore della pagina
- Slot : posizione all'interno della pagina

Si può sia individuare velocemente un record sia permettere la sua riallocazione nella pagina senza modificare il RID.


---
Subject: "[[Indice - Basi di dati]]"
tags:
  - BD
Creation: 2024-02-28
---
# DBMS
Un [[DBMS]] è un sistema software che gestisce grandi quantità di dati persistenti e condivisi.

### Funzionalità
- Gestire grandi quantità di dati problemi di effiecienza
- La persistenza e la condivisione richiedono meccanismi per garantire l'affidabilità dei dati (fault tolerance), il controllo degli accessi ed il controllo per la concorrenza,
- funzionalità per l'efficacia per la descrizione die dati, lo sviluppo di applicazioni e l'amministrazione di un DB

## Gestione integrata e con
La **gestione integrata** e la **condivisione dei dati** permettono di evitare ripetizioni (ridondanza dovuta a copie multiple dello stesso dato), e quindi un inutile spreco di risorse (memoria).
Inoltre, la **ridondanza** può dar luogo a problemi di **inconsistenza delle copie** e, in ogni caso, comporta la necessità di propagare le modifiche, con un ulteriore spreco di risorse (CPU e rete)

I Dati possono essere usati in diversi database per ciò è utile creare una base di dati unica.
	Esempio: il settore Ordini di un’azienda manifatturiera memorizza i propri dati in un file, non condiviso con gli altri settori aziendali. 
	Ogni volta che arriva un ordine, i dati relativi devono essere trasmessi al settore Spedizioni, affinché l’ordine possa essere evaso. 
	A spedizione eseguita, i dati relativi devono essere ritrasmessi al settore Ordini.
	![[Pasted image 20240228182310.png]]

## [[Modelli dei dati|Modello dei dati]]

Dal punto di vista utente un DB è visto come una collezione di dati che modellano una certa porzione della realtà di interesse.
L’astrazione logica con cui i dati vengono resi disponibili all’utente definisce un modello dei dati.
Più precisamente un [[Modelli dei dati|modello dei dati]] è una collezione di concetti che vengono utilizzati per descrivere i dati, le loro associazioni/relazioni, e i vincoli che questi devono rispettare.
Un ruolo di primaria importanza nella definizione di un modello dei dati è svolto dai meccanismi che possono essere usati per strutturare i dati (cfr. i costruttori di tipo in un linguaggio di programmazione).

Si vuole quindi che ci sia una divisione tra il modello dati e la logica di accesso.
Si parla quindi di ***indipendenza fisica*** in quanto la riorganizzazione dei dati non deve avere effetti collaterali sui programmi applicativi, e ***indipendenza logica*** in quanto si può accedere ai dati indipendentemente dalla loro organizzazione.

# Architettura di un DBMS
![[Pasted image 20240229051936.png]]
__DB fisico__: ci sono i file che risiedono nella memoria permanente. contiene i vari schemi fisici che descrivono il modello logico. La gestione del DB fisico è a carico del DBMS manager.

__Gestore del file__ : scrive pagine e si interfaccia con la memoria permanente
__Gestore del buffer__ : serve per intermediario tra la memoria fisica e i buffer ossia la memoria volatile del server. 
Si deve anche occupare di interfacciarsi con il gestore delle query.

**Gestore delle query** : serve per interpretare e gestire le query e si deve interfacciare con gli utenti o le applicazioni.

**Gestore delle transazioni** : non è detto che una operazioni riguarda una transazione, ma ne può riguardare di più e serve quindi una componente che me le gestisca

![[Pasted image 20240229051952.png]]
si può quindi dividere un DBMS in macchina fisica e in macchina logica.
La macchina fisica ha a che fare con dati e indici. Gestisce le strutture di accesso e le transazioni. 
La macchina logica invece deve gestire le interrogazioni, il catalogo e il DDL.

-> DBMS non destinati a Big data. Tali DBMS hanno cose in comune ma hanno struttura diversa
# [[DBMS - Memoria|Gerarchia delle memorie]]
La memoria di un sistema di calcolo è organizzata in una gerarchia. 
Al livello più alto memorie di piccola dimensione, molto veloci, e costose.
Scendendo lungo la gerarchia la dimensione aumenta, diminuiscono la velocità e il costo. 

**Prestazioni di una memoria**: dato un indirizzo di memoria, le prestazioni si misurano in termini di tempo di accesso, determinato dalla somma della latenza, ossia il tempo necessario per accedere al primo byte, e del tempo di trasferimento, ovvero il tempo necessario per muovere i dati.
$$Tempo di accesso = latenza + \frac{dimensione\ dati\ da \ trasferire}{velocità\ di\ trasferimento}$$


## Implicazioni per i DBMS

Un DB, a causa della sua dimensione, risiede normalmente su dischi, ed eventualmente anche su altri tipi di dispositivi.
I dati devono essere trasferiti in memoria centrale per essere elaborati dal DBMS.
Il trasferimento non avviene in termini di singole tuple, bensì di blocchi (o pagine, termine comunemente usato quando i dati sono in memoria).
Poiché spesso le operazioni di I/O costituiscono il bottleneck del sistema, si rende necessario ottimizzare l’implementazione fisica del DB, attraverso:
- Organizzazione efficiente delle tuple su disco • Strutture di accesso efficienti
- Gestione efficiente dei buffer in memoria 
- Strategie di esecuzione efficienti per le query
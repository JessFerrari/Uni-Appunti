---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Base di dati]]"
tags:
  - BD
Creation: 2024-02-08
---

>  Un DBMS (Data Base Management System) è un sistema centralizzato per la gestione delle [[Base di dati|basi di dati]]. 
> Ne garantisce le caratteristiche attraverso il controllo dei dati, rendendoli accessibili solo dagli utenti autorizzati
> Offre opportuni linguaggi per:
> • definire lo schema di una basi di dati (lo schema va definito prima di creare dati) 
> • scegliere le strutture dati per la memorizzazione dei dati
> • memorizzare i dati rispettando i vincoli definiti nello schema
> • recuperare e modificare i dati interattivamente (linguaggio di interrogazione o query language) o da programmi.

Un Data Base Management System (DBMS) è un sistema (prodotto software) in grado di gestire collezioni di dati che siano (anche):
- grandi 
- persistenti (con un periodo di vita indipendente dalle singole esecuzioni dei programmi che le utilizzano)
- condivise (utilizzate da applicazioni diverse),
garantendo: 
- Affidabilità (resistenza a malfunzionamenti hardware e software-recovery) : protezione dei dati da malfunzionamenti hardware o software (fallimenti di transazione, di sistema e disastri) e da interferenze indesiderate dovute all’accesso concorrente ai dati da parte di più utenti.
- Sicurezza (con una disciplina e un controllo degli accessi) : protezione dei dati da usi non autorizzati
- Integrità: mantenimento delle proprietà specificate in modo dichiarativo nello schema (vincoli d’integrità)



Come ogni prodotto informatico, un DBMS deve essere efficiente (utilizzando al meglio le risorse di spazio e tempo del sistema) ed efficace (rendendo produttive le attività dei suoi utilizzatori).

### OLTP

I sistemi tradizionali usano elaborazioni di tipo OLTP(On Line Transitional Processing), [[Transazioni|transizionali]], il quale è caratterizzato dall’uso principale dei DBMS.
Tradizionale elaborazione di transazioni, che realizzano i processi operativi per il funzionamento di organizzazioni:

- Operazioni predefinite e relativamente semplici
- Ogni operazione coinvolge “pochi” dati
- Dati di dettaglio, aggiornati

![[04_DBMS.png]]
### OLAP

I sistemi informatici direzionali hanno dati organizzati in Data Warehouse (DW) e gestiti da un opportuno sistema OLAP (On Line Analytical Processing), direzionali.
Le applicazioni, dette di Business intelligence, sono strumenti di supporto ai processi di controllo delle prestazioni aziendali e di decisione manageriale.

Terminologia anglosassone:

- Management Information Systems (MIS)
- Decision support systems (DSS), data or model based
- Executive Information System (EIS)
![[05_OLAP.png]]


## OLTP vs OLAP

![[06_OLTPvsOLAP.png]]


## Funzionalità DBMS

![[07_DBeDBMS.png]]

- *__Definizione delle basi di dati__*
	Con i DBMS si definiscono delle [[Base di dati|basi di dati]] grazie ad un [[DDL|linguaggio per la definizione della base di dati (DDL)]].
	
	
 
- *__Controllo delle basi di dati__*

- *__Distribuzione delle basi di dati__*

- *__Uso delle basi di dati__*
	Un DBMS deve prevedere più modalità d’uso per soddisfare le esigenze delle diverse categorie di utenti che possono accedere alla base di dati (dati e catalogo)
	- Un’interfaccia grafica per accedere ai dati
	- Un linguaggio di interrogazione per gli utenti non programmatori
	- Un linguaggio di programmazione per gli utenti che sviluppano applicazioni:
	    - integrazione [[DDL]] (Per la definizione di schemi) e [[DML]](Per l’interrogazione e l’aggiornamento) nel linguaggio ospite: procedure predefinite, estensione del compilatore, precompilazione
	    - comunicazione tra linguaggio e DBMS
	- Un linguaggio per lo sviluppo di interfacce per le applicazioni
	
- *__Amministrazione delle basi di dati__*


## Problemi DBMS

- *__Gestione__* : 
- __*Funzionamento*__ :
- __*Produzione del software*__ :
- __*Pianificazione*__ :

### PRO
- [[DDL|Indipendenza dei dati]]
- Recupero efficiente dei dati
- Integrità e sicurezza dei dati 
- Accessi interattivi, concorrenti e protetti da malfunzionamenti 
- amministrazione dei dati
- Riduzione dei tempi di sviluppo delle applicazioni
- Riduzione dei costi della tecnologia e i possibili tipi di DBMS facilitano la loro distribuzione

### CONTRO

- Prima di caricare i dati è necessario definire uno schema
- Possono essere costosi e complessi da installare e mantenere in esercizio
- Sono ottimizzati per le applicazioni OLTP e non quelle OLAP

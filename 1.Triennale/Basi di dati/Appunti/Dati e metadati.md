---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Base di dati]]"
tags:
  - BD
Creation: 2024-02-08
---
Una [[Base di dati|base di dati]] è una raccolta di dati permanenti suddivisi in due categorie:

- i *__metadati__*: descrivono fatti sullo schema dei dati, utenti autorizzati, applicazioni, parametri quantitativi sui dati, ecc. Sono descritti da uno schema usando il modello dei dati adottato dal [[DBMS]] e sono interrogabili con le stesse modalità previste per i dati;

- i *__dati__*: rappresentano di certi fatti conformi alle definizioni dello schema, con le seguenti caratteristiche
	- Sono organizzati in insiemi strutturati e omogenei, fra i quali sono definite delle relazioni. La struttura dei dati e le relazioni sono descritte nello schema usando i meccanismi di astrazione del [[Modelli dei dati|modello dei dati]] del DBMS;
    
    - Sono organizzati in insiemi strutturati e omogenei, fra i quali sono definite delle relazioni. La struttura dei dati e le relazioni sono descritte nello schema usando i meccanismi di astrazione del modello dei dati del DBMS;
    
	- Sono molti, in assoluto e rispetto ai metadati, e non possono essere gestiti in memoria temporanea;
	
    - Sono accessibili mediante transazioni, unità di lavoro atomiche che non possono avere effetti parziali;

    - Sono protetti sia da accesso da parte di utenti non autorizzati, sia da corruzione dovuta a malfunzionamenti hardware e software;
    
    - Sono utilizzabili contemporaneamente da utenti diversi.

![[07_DBeDBMS.png]]
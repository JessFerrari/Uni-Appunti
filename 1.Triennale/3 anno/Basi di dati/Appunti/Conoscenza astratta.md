---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Aspetto ontologico]]"
tags:
  - BD
Creation: 2024-02-12
---
La conoscenza astratta riguarda i fatti generali che descrivono la struttura della [[Conoscenza concreta|conoscenza concreta]], su come può evolversi nel tempo (___Vincoli di integrità___, statici e dinamici) e le regole per derivare nuovi fatti da quelli già noti.

I ___Vincoli di integrità statici___ definiscono condizioni sui valori della conoscenza concreta che devono essere soddisfatte a prescindere dall'evoluzione dell'universo del discorso.
Riguardano: ^c7fe4d
- i valori di una proprietà
- i valori di proprietà diverse di una stessa entità
- i valori di proprietà di entità diverse di uno stesso insieme. Collegato al concetto di [[#^a8550e|chiave]].
- i valori di proprietà di entità di insiemi diversi


> [!NOTE] Chiave
> Un'insieme di proprietà è detto chiave, rispetto ad una collezione di entità, se:
> 1. i suoi valori identificano univocamente un elemento della collezione 
> 2. ogni proprietà della chiave è necessaria a questo fine
	Esempio il codice fiscale
^a8550e

I ___Vincoli di integrità dinamici___ definiscono delle condizioni sul modo in cui la conoscenza concreta può evolvere nel tempo.
Ossia cono non può succedere in un determinato stato (le [[Transazioni|transazioni]]).

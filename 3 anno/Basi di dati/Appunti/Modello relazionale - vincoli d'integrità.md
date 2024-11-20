---
Subject: "[[Indice - Basi di dati|Basi di dati]]"
Super Topic: "[[Modello relazionale]]"
tags:
  - BD
Creation: 2024-02-17
---
# Vincoli di integrità

Esistono istanza di basi di dati che, pur sintatticamente corrette, non rappresentano informazioni possibili per l’applicazione di interesse e che quindi generano informazioni senza significato.

Uno schema relazionale è costituito da un insieme di _schemi di relazione_ e da un _insieme di vincoli_ d’integrità sui possibili valori delle estensioni delle relazioni.

Un **vincolo d’integrità** è una proprietà che deve essere soddisfatta dalle istanze che rappresentano informazioni corrette per l’applicazione. Un vincolo è espresso mediante una funzione booleana (un predicato) che associa ad ogni istanza il valore vero o falso.


I vincoli corrispondono a proprietà del mondo reale modellato dalla base di dati.
In uno schema si associano un insieme di vincoli e si considerano corrette solo le istanze che li rispettano tutti.



## Tipi di vincoli

Esistono 2 tipi di vincoli: 

- Vincoli **intra - relazionali** Sono i vincoli che devono essere rispettati dai valori contenuti nella relazione considerata.
    - Vincoli **su valori** (o **di dominio**), che coinvolgono un solo attributo (esempio con voto universitario). 
    - Vincoli **di ennupla**, che esprimono condizioni sui valori di ciascuna ennupla, indipendentemente dalle altre ennuple.

- Vincoli **inter - relazionali**: Sono i vincoli che devono essere rispettati da valori contenuti in relazioni diverse


# Vincolo di integrità referenziale

Un **vincolo di integrità referenziale** (”_foreign key_”) fra gli attributi $X$ di una relazione $R_1$ e un’altra relazione $R_2$ impone ai valori su $X$ in $R_1$ di comparire come valori della [[Modello relazionale - chiave|chiave primaria]] di $R_2$.

![[Pasted image 20240219004633.png]]

Se viene violato il vincolo di integrità referenziale viene rifiutata l'operazione, si elimina in cascata e si introducono valori nulli.
Ciò lo decide il progettista del [[DBMS]].
Con eliminazione a cascata vuol dire che se elimino una ennupla dalla tabella con la chiave primaria viene eliminata anche da quello con la chiave esterna e quindi si rischia di cancellare tutto.
Con l'opzione dei valori Null, viene inserito nell'attributo della chiave esterna null quando si elimina una ennupla dalla tabella puntata. In questo modo rischio problemi soprattutto se la chiave esterna è anche chiave primaria (vedi foto sopra).



---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
# Vincoli intrarelazionali
I [[Modello relazionale - vincoli d'integrità|vincoli di integrità]] consentono di limitare i valori ammissibili per una determinata colonna della tabella in base a specifici criteri. 
I vincoli di integrità intrarelazionali (ossia che non fanno riferimento ad altre relazioni) sono: 
- `NOT NULL `
- `UNIQUE`, che definisce chiavi 
- `PRIMARY KEY`, che definisce la chiave primaria (una sola, implica `NOT NULL`)
- `CHECK`

## `UNIQUE`

Il vincolo unique, utilizzato nella definizione dell’attributo, indica che non ci possono essere due valori uguali in quella colonna. 
Indica una chiave della relazione, ma non una chiave primaria.
Può essere espresso in due forme: 
- nella definizione di un attributo, se forma da solo la chiave 
- come elemento separato 

 Il vincolo di unicità può anche essere riferito a coppie o insiemi di attributi. 
 Ciò non significa che per gli attributi dell’insieme considerato ogni singolo valore deve apparire una sola volta, ma che non ci siano due dati (righe) per cui l’insieme dei valori corrispondenti a quegli attributi siano uguali. 
 In questo caso il vincolo viene dichiarato dopo aver dichiarato tutte le colonne mediante un vincolo di tabella, utilizzando il comando `Unique (lista attributi)`

## `PRIMARY KEY`

Il vincolo `PRIMARY KEY` è simile a unique, ma definisce la chiave primaria della relazione, ossia un attributo che individua univocamente un dato.
Si usa :
- nella definizione di un attributo, se formato da solo la chiave 
- come elemento separato.

Implica sia il vincolo `UNIQUE` che il vincolo `NOT NULL` (non è ammesso che per uno degli elementi della tabella questo valore sia non definito). 

Serve ad indentificare univocamente i soggetti del dominio. 
Questo vincolo permette spesso il collegamento fra due tabelle.

Analogamente al vincolo unique, anche il vincolo di chiave primaria può essere definito su un insieme di elementi.


# Vincoli interrelazionali 

I vincoli interrelazionali sono quei vincoli che vengono imposti quando gli attributi di due diverse tabelle devono essere messi in relazione.
Questo è fatto per soddisfare l‘esigenza di un database di non essere ridondante e di avere i dati sincronizzati. 
Se due tabelle gestiscono gli stessi dati, è bene che di essi non ce ne siano più copie, sia allo scopo di non occupare troppa memoria, sia affinché le modifiche fatte su dati uguali utilizzati da due tabelle siano coerenti.

`REFERENCES` e `FOREIGN KEY` permettono di definire vincoli di integrità referenziale 

Hanno due sintassi:
- per singoli attributi (come vincolo di colonna) 
- su più attributi (come vincolo di tabella) 

Si possono definire politiche di reazione alla violazione (ossia stabilire l‘azione che il DBMS deve compiere quando si viola il vincolo)
```MYSQL
CREATE <nome tabella>
(attributo_1…, 
 attributo_2…, 
 … 
 attributo_k REFERENCES tabella_riferita(colonna_riferita) 
 … 
 )
```

```MYSQL
CREATE <nome_tabella> 
(attributo_1 …,
 attributo_2 …,
  …
attributo_n …,
FOREIGN KEY (col_referenti) REFERENCES tab_riferita(col_riferite)
  …
   )
```

## Vincolo referenziale
![[Pasted image 20240223214353.png]]
![[Pasted image 20240223214401.png]]

## `CHECK`
Un vincolo di `CHECK` richiede che una colonna, o una combinazione di colonne, soddisfi una condizione per ogni riga della tabella. 
Il vincolo `CHECK` deve essere una espressione booleana che è valutata usando i valori della colonna che vengono inseriti o aggiornati nella riga. 
Può essere espresso sia come vincolo di riga che come vincolo di tabella. 
Se è espresso come vincolo di riga, può coinvolgere solo l’attributo su cui è definito, mentre se serve eseguire un check che coinvolge due o più attributi, si deve definire come vincolo di tabella

ESEMPIO : nessuno stipendio degli impiegati può avere valore minore di 0 (espresso come vincolo di riga). 
```MYSQL
CREATE TABLE IMPIEGATO 
( Matricola CHAR(6) PRIMARY KEY, 
 Nome CHAR(20) NOT NULL,
Cognome CHAR(20) NOT NULL,
 Dipart CHAR(15), 
 Stipendio NUMERIC(9) DEFAULT 0 CHECK (Stipendio>=0), 
 FOREIGN KEY(Dipart) REFERENCES Dipartimento(NomeDip), 
 UNIQUE (Cognome,Nome) )
```
Nessuno stipendio degli impiegati può avere valore minore di 0 (espresso come vincolo di tabella). 
```MYSQL
CREATE TABLE IMPIEGATO 
( Matricola CHAR(6) PRIMARY KEY, 
 Nome CHAR(20) NOT NULL, 
 Cognome CHAR(20) NOT NULL, 
 Dipart CHAR(15), 
 Stipendio NUMERIC(9) DEFAULT 0, 
 FOREIGN KEY(Dipart) REFERENCES Dipartimento(NomeDip), 
 UNIQUE (Cognome,Nome), 
 CHECK (Stipendio>=0) )
```

![[Pasted image 20240223215131.png]]
# Reazione alla violazione
Quando si crea un vincolo foreign key in una tabella, in SQL standard si può specificare l’azione da intraprendere quando delle righe nella tabella riferita vengono cancellate o modificate. 
Tali reazioni alla violazione vengono dichiarate al momento della definizione dei vincoli di foreign key rispettivamente mediante i comandi ON DELETE / ON UPDATE
![[Pasted image 20240223215239.png]]

- Impedire il delete (NO ACTION): Blocca il delete delle righe dalla tabella riferita quando ci sono righe che dipendono da essa. Questa è l’azione che viene attivata per default. 
- Generare un delete a catena (CASCADE): Cancella tutte le righe dipendenti dalla tabella quando la corrispondente riga è cancellate dalla tabella riferita.
- Assegnare valore NULL (SET NULL): Assegna NULL ai valori della colonna che ha il vincolo foreign key nella tabella quando la riga corrispondente viene cancellata dalla tabella riferita. 
- Assegnare il valore di default (SET DEFAULT): Assegna il valore di default ai valori della colonna che ha il vincolo foreign key nella tabella quando la riga corrispondente viene cancellata dalla tabella riferita.

Nello standard SQL la reazione alla violazione può anche essere attivata quando i dati della tabella riferita vengono aggiornati. 
Viene attivato mediante il comando ON UPDATE seguito da: 
- CASCADE : Le righe della tabella referente vengono impostati ai valori della tabella riferita 
- SET NULL : i valori della tabella referente vengono impostati a NULL SET
- DEFAULT : i valori della tabella referente vengono impostati al valore di default
- NO ACTION : rifiuta gli aggiornamenti che violino l’integrità referenziale
---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
# [[DDL]] - Data Definition Language

Il Data Definition Language (DDL) è un linguaggio SQL che consiste nell’insieme delle istruzioni SQL che permettono la creazione, modifica e cancellazione delle tabelle, dei domini e degli altri oggetti del database, al fine di definire il suo [[Modello relazionale|schema logico]].

```SQL
CREATE SCHEMA Nome AUTHORIZATION Utente 
CREATE TABLE o VIEW, con vincoli  
CREATE INDEX 
CREATE PROCEDURE 
CREATE TRIGGER
```

## I tipi
I tipi più comuni per i valori degli attributi sono: 
- `CHAR(n)` per stringhe di caratteri di lunghezza fissa n; 
- `VARCHAR(n)` per stringhe di caratteri di lunghezza variabile di al massimo n caratteri; 
- `INTEGER` per interi con la dimensione uguale alla parola di memoria standard dell’elaboratore; 
- `REAL` per numeri reali con dimensione uguale alla parola di memoria standard dell’elaboratore; 
- `NUMBER(p,s)` per numeri con p cifre, di cui s decimali; 
- `FLOAT(p)` per numeri binari in virgola mobile, con almeno p cifre significative;
- `DATE` per valori che rappresentano istanti di tempo (in alcuni sistemi, come Oracle), oppure solo date (e quindi insieme ad un tipo `TIME` per indicare ora, minuti e secondi).

## Definizione di tabelle - `CREATE TABLE`
Le tabelle (corrispondenti alle relazioni dell‘algebra relazionale) vengono definite in SQL mediante l‘Istruzione `CREATE TABLE`. 
Questa istruzione definisce uno schema di relazione e ne crea un’istanza vuota specificandone attributi, domini e vincoli.

Sintassi:
```SQL
CREATE TABLE <nome_tabella> 
( nome_colonna_1 tipo_colonna_1 clausola_default_1 vincolo_di_colonna_1, 
 nome_colonna_2 tipo_colonna_2 clausola_default_2 vincolo_di_colonna_2, 
 …….. 
 nome_colonna_k tipo_colonna_k clausola_default_k vincolo_di_colonna_k, 
 vincoli di tabella )
```

L‘istruzione `CREATE TABLE` è seguita da un nome che la caratterizza, e dalla lista delle colonne (attributi), di cui si specificano le caratteristiche. 
Alla fine si possono anche specificare eventuali [[SQL DDL - Vincoli|vincoli di tabella]].


Esempio:
```SQL
CREATE TABLE IMPIEGATO 
( Matricola CHAR(6) PRIMARY KEY, 
 Nome CHAR(20) NOT NULL, 
 Cognome CHAR(20) NOT NULL, 
 Dipart CHAR(15),
Stipendio NUMERIC(9) DEFAULT 0, 
 FOREIGN KEY(Dipart) REFERENCES Dipartimento(NomeDip), 
 UNIQUE (Cognome,Nome) )
```

L’effetto del comando `CREATE TABLE` definisce uno schema di relazione e ne crea un’istanza vuota, specificandone attributi, domini e vincoli. 
Una volta creata, la tabella è pronta per l’inserimento dei dati che dovranno soddisfare i vincoli imposti. 
Nel caso dell’esempio dato nella slide precedente, si ottiene:
![[Pasted image 20240223060004.png]]La visualizzazione dello schema di una tabella, dopo che è stata creata, può essere ottenuta mediante il comando SQL `DESCRIBE`
Ciò che si crea con un `CREATE` si può eliminare con il comando `DROP` o cambiare con il comando `ALTER`.

Con il comando `ALTER TABLE` è possibile :
1. Aggiungere una colonna `(ADD [COLUMN])` 
2. Eliminare una colonna `(DROP [COLUMN])` 
3. Modificare la colonna `(MODIFY)` 
4. Aggiungere l’assegnazione di valori di default `(SET DEFAULT)` 
5. Eliminare l’assegnazione di valori di default `(DROP DEFAULT)` 
6. Aggiungere vincoli di tabella `(ADD CONSTRAINT)`
7. Eliminare vincoli di tabella `(DROP CONSTRAINT)` 
8. Altre opzioni sono possibili nei linguaggi specifici (vedi manuali)

### Aggiungere una colonna
Sintassi: 
```MYSQL
ALTER TABLE nome_tabella 
ADD [COLUMN] nome_col tipo_col default_col vincolo_col 
```
In mancanza di altre specifiche, la nuova colonna viene inserita come ultima colonna della tabella. 
Altrimenti è possibile dare questa specifica: 
```MYSQL
ADD COLUMN <CREA_DEFINIZIONE> [FIRST/AFTER <nome_colonna)] 
```
`FIRST` permette di aggiungerla come prima colonna/`AFTER` colonna subito dopo la colonna indicata.

#### Regole per aggiungere una colonna 
Si può aggiungere una colonna in qualsiasi momento se non viene specificato `NOT NULL`.

### Eliminare una colonna
```MYSQL
ALTER TABLE nome_tabella 
DROP COLUMN nome_colonna {RESTRICT/CASCADE}
```
In SQL standard le opzioni `RESTRICT/CASCADE` sono alternative ed è obbligatorio specificare l’una o l’altra.
- `RESTRICT`: se in un'altra tabella si ha un vincolo di integrità referenziale con questa colonna, l’esecuzione del comando drop fallisce. 
- `CASCADE`: eliminando la colonna, vengono eliminate tutte le dipendenze logiche di altre colonne dello schema da questa. 

```MYSQL
ALTER TABLE Impiegato 
Drop column dipart restrict 
```
``` MYSQL
ALTER TABLE impiegato 
Drop column dipart cascade
```

### Modificare una colonna
Se si vogliono modificare le caratteristiche di una colonna dopo averla definita, occorre eseguire l’istruzione: 
```MYSQL
ALTER TABLE nome_tabella 
MODIFY nome colonna tipo_col default_col vincoli_col 
```

ESEMPIO: Supponendo che nella tabella Impiegato ci sia una colonna ‘nome’ definita come `varchar(20)`, modificarla in modo che diventi un `varchar(30)` e sia definito su di essa il vincolo not null. 
```MYSQL
ALTER TABLE impiegato 
MODIFY nome varchar(30) not null
```

### Assegnare un vincolo di default
Nell’SQL standard è possibile imporre un valore di default col comando specifico `SET DEFAULT`, con la seguente sintassi :
```MYSQL
ALTER TABLE nome_tabella 
ALTER [COLUMN] nome_colonna 
SET DEFAULT valore_default 
```

ESEMPIO: Imporre il valore di default ‘Direzione Generale’ ai valori della colonna Dipart in cui tale valore non è assegnato esplicitamente 
```SQL
ALTER TABLE Impiegato 
Alter [column] Dipart
SET DEFAULT ‘Direzione Generale
```

### Eliminare una valore di default 
In SQL standard è possibile eliminare un vincolo di default da una colonna mediante l’istruzione :
```SQL
ALTER TABLE nome_tabella 
ALTER [COLUMN] nome_colonna 
DROP DEFAULT
```
Eseguendo questa istruzione il valore di default diventa automaticamente NULL 

Esempio: Eliminare il default introdotto nell’esercizio precedente 
```MYSQL
ALTER TABLE Impiegato 
ALTER [COLUMN] Dipart 
DROP DEFAULT
```

### Aggiungere [[SQL DDL - Vincoli|vincoli di tabella]]
Se si vuole aggiungere un vincolo di tabella, si esegue il comando :
```MYSQL
ALTER TABLE nome_tabella 
ADD CONSTRAINT nome_vincolo vincolo_di_tabella 
```

ESEMPIO: Nella tabella Impiegato, aggiungere un vincolo di unicità alla coppia (nome, cognome) 
```MYSQL
ALTER TABLE impiegato 
ADD CONSTRAINT unique_const unique(nome, cognome) 
```

Occorre assegnare un nome al vincolo
![[Pasted image 20240223062809.png]]

### Eliminare [[SQL DDL - Vincoli|vincoli di tabella]]
Nello standard SQL, se si vuole eliminare un vincolo di tabella si esegue l’istruzione :
```MYSQL
ALTER TABLE nome_tabella 
DROP CONSTRAINT nome_vincolo{RESTRICT/ CASCADE} 
```
L’opzione `RESTRICT` non permette di eliminare vincoli di unicità e di chiave primaria su una colonna se esistono vincoli di chiave esterna che si riferiscono a tale colonna. 
L’opzione `CASCADE` non opera questa restrizione. 
Da notare che per eliminare un vincolo, esso deve essere definito mediante un identificatore


### Eliminare una tabella

Si può eliminare una tabella mediante l’istruzione `DROP TABLE` .
Nello standard SQL si possono anche specificare le opzioni `RESTRICT/CASCADE`
- RESTRICT: se la tabella è utilizzata nella definizione di altri oggetti dello schema, la sua eliminazione viene impedita. 
- CASCADE: vengono eliminate tutte le dipendenze degli altri oggetti dello schema da questa tabella
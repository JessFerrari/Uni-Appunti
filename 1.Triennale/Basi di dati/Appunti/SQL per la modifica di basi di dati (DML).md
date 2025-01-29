---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
# [[DML]] - Data Manipulation Language

Il DML (Data Manipulation Language) è il linguaggio [[SQL]] che serve per inserire, modificare e cancellare i dati dal database ma anche per interrogarli e quindi estrarre i dati da essi.


# Modifica dei dati
```MYSQL
INSERT INTO Tabella [ (A1,..,An)] 
( VALUES (V1,..,Vn) | AS Select ) 

UPDATE Tabella 
SET Attributo = Expr, …, Attributo = Expr 
WHERE Condizione 

DELETE FROM Tabella 
WHERE Condizione
```

## Inserimento

### Insert semplice 
Per inserire un nuovo dato in una tabella si usa il comando `INSERT`.
Sintassi: 
```MYSQL
INSERT INTO nome tabella 
[(ListaAttributi)] VALUES (ListaDiValori) 
| SQLSelect
```
Ai valori non attribuiti viene assegnato NULL, a meno che non sia specificato un diverso valore di default. L’inserimento fallisce se NULL non è permesso per gli attributi mancanti.
Non specificare gli attributi equivale a specificare tutte le colonne della tabella. 
Si deve rispettare l’ordine degli attributi

### insert mediante SELECT
Si ha la  possibilità di effettuare un insert prendendo i dati da un’altra tabella.
Questo è possibile mediante il comando di interrogazione del database `SELECT`.
 
Con questo tipo di insert si possono effettuare tanti inserimenti simultaneamente.
Esempio: 
```SQL
Tabella: Indirizzi_Studenti( Indirizzo, Telefono, Email) 
INSERT INTO Indirizzi_Studenti (Indirizzo, Telefono) 
SELECT Indirizzo, Telefono 
FROM Studenti
```

## Cancellazione - DELETE

Per eliminare un elemento bisogna individuare quale. 
Questo si può stabilire mediante la clausola `WHERE`, dove viene stabilita una condizione che individua l’elemento (o gli elementi) da cancellare. 
Spesso un particolare elemento può essere individuato mediante il suo valore nella chiave primaria.

Sintassi:
```SQL
DELETE FROM nome_tabella 
[WHERE Condizione]
```

Operazione non reversibile. 
Se la condizione è omessa questa istruzione cancella l’intero contenuto della tabella

 La condizione del delete può essere una normale condizione di SELECT.
 Questa modalità di delete permette di cancellare più righe con un’unica istruzione, purchè le righe soddisfinola condizione. 
 
 Esempio: eliminare tutte le righe della tabella esami in cui il numero di matricola non si trova nella tabella Studenti 
```SQL
 DELETE FROM Esami 
 WHERE Matricola NOT IN 
	 (SELECT Matricola FROM Studenti)
```

## Aggiornamento 
Inoltre è possibile aggiornare alcuni dati seguendo la seguente sintassi: 
```SQL
UPDATE Tabella 
SET Attributo = Espr 
WHERE Condizione
```
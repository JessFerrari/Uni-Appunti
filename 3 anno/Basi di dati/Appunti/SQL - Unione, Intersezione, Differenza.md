---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL e algebra relazionale]]"
tags:
  - BD
Creation: 2024-02-23
---
A volte può essere utile poter ottenere un’unica tabella contenente alcuni dei dati contenuti in due tabelle omogenee, ossia con attributi definiti sullo stesso dominio.
In SQL la `SELECT` da sola non permette di fare questo tipo di operazioni su tabelle. 
Esistono per questo dei costrutti espliciti che utilizzano le parole chiave:
- `UNION` 
- `INTERSECT` 
- `EXCEPT` (in oracle `MINUS`)

Tali operatori lavorano sulle tabelle come se fossero insiemi di righe, dunque i duplicati vengono eliminati (a meno che si usi la specifica `ALL`) anche dalle proiezioni!

## Unione :`UNION`

L’operatore `UNION` realizza l’operazione di unione definita nell’[[Modello relazionale - Algebra relazionale|algebra relazionale]].
Utilizza come operandi le due tabelle risultanti da comandi `SELECT` e restituisce una terza tabella che contiene tutte le righe della prima e della seconda tabella. Nel caso in cui dall’unione e dalla proiezione risultassero delle righe duplicate, l’operatore `UNION` ne mantiene una sola copia, a meno che non sia specificata l’opzione `ALL` che indica la volontà di mantenere i duplicati 
```MYSQL
SELECT … 
UNION [all] 
SELECT ...
```

Esempio:
```MYSQL
SELECT padre 
FROM paternita 
UNION 
SELECT madre 
FROM maternita
```

Gli attributi del risultato hanno il nome di quelli del primo operando

## Differenza - `EXCEPT`
L’operatore `EXCEPT` utilizza come operandi due tabelle ottenute mediante due select e ha come risultato una nuova tabella che contiene tutte le righe della prima che non si trovano nella seconda. 
Realizza la differenza dell’algebra relazionale. 
Anche qui si può specificare l’opzione ALL per indicare la volontà di mantenere i duplicati.
```MYSQL
SELECT … 
EXCEPT [ALL] 
SELECT …
```

 La differenza può essere effettuata da un’unica select che utilizza subselect
	Esempi:
```MYSQL
	SELECT Nome 
	FROM Impiegato 
	EXCEPT 
	SELECT Cognome AS Nome 
	FROM Impiegato
	---
	SELECT nome 
	FROM Impiegato 
	WHERE nome<>ALL [not in] 
		(SELECT cognome 
		FROM Impiegato)

 ```

## Intersezione - `INTERSECT`

L’operatore `INTERSECT` utilizza come operandi due tabelle risultanti dai comandi `SELECT` e restituisce una tabella che contiene le righe comuni alle due tabelle iniziali. 
Realizza l’intersezione dell’algebra relazionale.
L’opzione `ALL` serve a mantenere gli eventuali duplicati di righe. In sua assenza, si mantiene una sola copia delle righe duplicate.
```MYSQL
SELECT … 
INTERSECT [ALL] 
SELECT …
```
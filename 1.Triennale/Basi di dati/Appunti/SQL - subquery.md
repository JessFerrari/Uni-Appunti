---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
Una subquery è un comando [[SQL - sintassi|SELECT]], racchiuso tra parentesi tonde, inserito all’interno di un comando SQL, per esempio un’altra Select. 
Le subquery possono essere utilizzate nei seguenti casi: 
- In espressioni di confronto 
- In espressioni di confronto quantificato
- In espressioni IN 
- In espressioni EXISTS 
- Nel calcolo di espressioni

Esistono 3 tipi di subquery: scalare, di colonna, di tabella  

La _Subquery Scalare_ è un comando Select che restituisce un solo valore (Con operatore aggregato)
```SQL
SELECT Max(Cilindrata) 
FROM Veicoli 

SELECT Cod_Categoria 
FROM Veicoli 
Where Targa=“123456” 
```

La _Subquery di Colonna_ è un comando Select che restituisce una colonna (un solo attributo)
```SQL
SELECT cod_categoria 
FROM Veicoli 
```

La _Subquery di Tabella_ è un comando Select che restituisce una tabella (ossia più attributi)
```SQL
SELECT Targa, Cod_mod, Posti 
FROM Veicoli
```

ESEMPIO
	![[Pasted image 20240223045510.png]]

Grazie alle subquery si possono fare contemporaneamente operazioni singole (proiezioni) che utilizzare operatori aggregati
	ESEMPIO
	![[Pasted image 20240223045713.png]]

Query nidificate possono essere “meno dichiarative” in un certo senso ma spesso sono più facilmente interpretabili, in quanto si possono suddividere in blocchi più semplici da interpretare

La forma piana e quella nidificata possono essere combinate.

Le subquery non possono contenere operatori insiemistici.

Il problema si supera facilmente con intersezione e differenza (per cui esiste una forma alternativa) ma non sempre per l’unione.
Le regole di visibilità simili a quelle delle procedure nei linguaggi di programmazione: 
- non è possibile fare riferimenti a variabili definite in blocchi più interni 
- se un nome di variabile è omesso, si assume riferimento alla variabile più “vicina” 
- in un blocco si può fare riferimento a variabili definite in blocchi più esterni


Il confronto con il risultato di una query nidificata può essere basato su più attributi
	ESEMPIO
	![[Pasted image 20240223050151.png]]

L’utilizzo di variabili deve rispettare le regole di visibilità cioè, una variabile può essere usata solo all’interno dello stesso blocco e in un blocco più interno.

Query nidificate complesse possono essere di difficile comprensione, soprattutto quando si usano molte variabili comuni tra blocchi diversi.


Le subquery oltre che essere usate all’interno della clausola WHERE, possono anche essere utilizzate nel calcolo di  espressioni, dunque per definire colonne.

	![[Pasted image 20240223052449.png]]
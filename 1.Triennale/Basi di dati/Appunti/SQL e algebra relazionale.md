---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-21
---
Le query del [[SQL]] si possono descrivere con gli alberi dell'[[Modello relazionale - Algebra relazionale|algebra relazionale]], detti [[DBMS - Piani d'accesso|piani d'accesso logici]].
![[Pasted image 20240221233835.png]]![[Pasted image 20240221233850.png]]

Spesso nel riferimento alle colonne selezionate nel join è necessario specificare da quale delle tabelle la colonna è stata estratta, al fine di evitare ambiguità

Di solito in una select che definisce una join possono essere necessarie ridenominazioni:
- nel prodotto cartesiano (ossia ridenominare le tabelle coinvolte)
- nella target list (ossia ridenominare gli attributi)
- ![[Pasted image 20240221234034.png]]


	1. [[SQL - JOIN]]
	2. [[SQL - subquery]]
	3. [[SQL - Quantificazione]]
	4. [[SQL - Unione, Intersezione, Differenza]]
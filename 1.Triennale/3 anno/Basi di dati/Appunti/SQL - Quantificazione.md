---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL e algebra relazionale]]"
tags:
  - BD
Creation: 2024-02-23
---
Tutte le interrogazioni su di una associazione multivalore vanno quantificate
![[Pasted image 20240223050344.png]]

NON bisogna usare frasi ambigue e perciò si usano quantificatori (sempre, tutti, nessuno, almeno ... )

Ne esistono di 2 tipi :
- ESISTENZIALE
- UNIVERSALE

> [!NOTE] Proprietà
> L'universale negata è un'esistenziale
> L'esistenziale negata è una universale


Le condizioni in SQL permettono anche il confronto fra un attributo e il risultato di una subquery che restituisce una colonna o una tabella 
- Operatore Scalare `(ANY | ALL) SelectQuery` 
	- `ANY`: il predicato è vero se almeno uno dei valori restituiti da Query soddisfano la condizione 
	- `ALL`: il predicato è vero se tutti i valori restituiti dalla Query soddisfano la condizione 

- Quantificatore esistenziale `EXISTS SelectQuery `
	- `EXIST` : il predicato è vero se la SelectQuery restituisce almeno una tupla


Per usarli in [[SQL - subquery|subquery]] questa deve:
- essere di colonna, 
- essere inserita DOPO l'operatore di confronto quantificativo
- NON è ammesso il confronto tra due query
- Nella subquery non è possibile utilizzare le clausole `HAVING` e `GROUP BY`

Mediante `EXISTS (SELECT * ...)` è possibile verificare se il risultato di una subquery restituisce almeno una tupla.
Facendo uso di `NOT EXISTS` il predicato è vero se la subquery non restituisce alcuna Tupla.

Occorre un meccanismo per rendere più flessibile la clausola `EXIST`, rendendo le condizioni della subquery dipendenti dalla tupla della query principale (query esterna).
Per far ciò si introduce un legame fra la query e la subquery (query correlate) e si definisce una variabile (un alias) nella query esterna, che si utilizza nella subquery

![[Pasted image 20240223051347.png]]


Le forme =ANY (equivalentemente IN) e <>ALL (equivalentemente NOT IN), forniscono un modo alternativo per realizzare intersezione e differenza dell’algebra relazionale.
	![[Pasted image 20240223051804.png]]
	![[Pasted image 20240223051824.png]]

![[Pasted image 20240223051851.png]]

![[Pasted image 20240223051926.png]]
![[Pasted image 20240223051943.png]]

---
---
---
![[Pasted image 20240223052100.png]]

---
---
---
![[Pasted image 20240223052337.png]]
![[Pasted image 20240223052346.png]]
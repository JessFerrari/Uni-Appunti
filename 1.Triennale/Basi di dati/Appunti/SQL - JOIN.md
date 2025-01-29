---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL e algebra relazionale]]"
tags:
  - BD
Creation: 2024-02-21
---
# Cross join 
Il cross join implementa il prodotto cartesiano.
Si realizza mediante una `SELECT`che utilizza le due (o più) tabelle coinvolte senza specificare nessuna condizione di join
	Esempio
```SQL
SELECT Categorie.*, Fabbriche.*
FROM Categorie, Fabbriche
```

Se due tabelle del database contengono dei dati in comune, possono essere correlate mediante un’operazione di `JOIN`.
Le colonne delle due tabelle che creano la correlazione rappresentano la stessa entità, ossia i loro valori appartengono allo stesso dominio.
In genere le colonne delle due tabelle considerate sono legate da un vincolo di chiave esterna (ma non è obbligatorio).

# Equi join
IL join (o equi-join) fra due tabelle è una terza tabella le cui righe sono tutte e sole quelle ottenute dal prodotto cartesiano delle righe delle due tabelle di partenza i cui valori delle colonne espresse dalla condizione di join sono uguali.

In SQL il join viene realizzato mediante una particolare forma del `SELECT`, in cui nella clausola `FROM` vengono indicate le due tabelle coinvolte e nella clausola `WHERE` viene espresso il collegamento fra le due tabelle, mediante la condizione di join.

Il Join consiste di:
- Un prodotto cartesiano (`FROM`)
- Una selezione (`WHERE`)
- Una proiezione (`SELECT`)
	Esempio:
	- Siano $Tab1(A1,A2)$ e $Tab2(A2,A3)$ due relazioni 
	- $\pi_{A1,A4}(\sigma_{A2=A3}(Tab1\Join Tab2))$
```SQL
SELECT Tab1.A1, Tab2.A4
FROM Tab1, Tab2
WHERE Tab1.A2 = Tab2.A3
```
	![[Pasted image 20240222214140.png]]


# INNER JOIN
L’INNER JOIN è un’operazione di join in cui la condizione non sia necessariamente una condizione di uguaglianza.
	![[Pasted image 20240222214855.png]]


# SELF JOIN
Un caso molto particolare di Join è quello che mette in relazione una tabella con se stessa. 
Questo si può ottenere ridenominando due volte la tabella con due nomi diversi, trattando le due copie come se si trattasse di due tabelle diverse. 
In questo caso si parla di SELF JOIN
```SQL
	SELECT X.A1, Y.A4 
	FROM Tab1 X, Tab2 Y, Tab1 Z 
	WHERE X.A2 = Y.A3 AND X.A2 = Z.A1
```



# Clausola `JOIN`
Nei DBMS più moderni, per effettuare il join di due tabelle è possibile utilizzare una forma più esplicita (standard ANSI).
La sintassi è la seguente :
```SQL
SELECT Attributi 
FROM Tab1 JOIN Tab2 
ON CondizioneDiJoin
```

Ad esempio:
	![[Pasted image 20240222215520.png]]

Se si deve operare una equi-join, ossia un join la cui condizione sia una condizione di uguaglianza, e che sia anche un Natural Join, ossia un join creato su tutte le colonne che hanno il medesimo nome in entrambe le tabelle, possiamo utilizzare la seguente sintassi:
```MYSQL
SELECT listaAttributi 
FROM Tab1 NATURAL JOIN Tab 2
```


## Clausola `USING`
 Può succedere comunque che nelle tabelle coinvolte ci siano più attributi con lo stesso nome, e col Natural Join tutte queste coppie di attributi presi dalla due tabelle vengono identificate.
 Se invece vogliamo operare una join in cui la condizione riguarda solo una o alcune di queste coppie, si usa la clausola USING seguita dall’elenco degli attributi coinvolti nella condizione:
```MYSQL
 SELECT lista attributi 
 FROM Tab1 JOIN Tab2 
 USING (attr1,attr2,…)
```
	![[Pasted image 20240223044333.png]]

# Outer join

Quando vengono correlate mediante una join delle tabelle con colonne contenenti dati in comune, è possibile che un valore sia presente in una delle colonne e non nell’altra. 
Effettuando un equi-join la riga corrispondente a tale valore viene scartato.
In alcuni casi invece può essere necessario mantenere questi valori. 
Per fare questo si deve effettuare un outer join:
```MYSQL
SELECT lista_attributi 
FROM Tab1 LEFT [OUTER] JOIN Tab2 

SELECT lista_attributi 
FROM Tab1 RIGHT [OUTER] JOIN Tab2 

SELECT lista_attributi 
FROM Tab1 FULL [OUTER] JOIN Tab2
```
	![[Pasted image 20240223044526.png]]
L'operatore di OUTER JOIN può essere applicato usando la seguente sintassi:
- $\{LEFT | RIGHT | FULL\} [OUTER] JOIN + ON <predicato>$ 
- $\{ LEFT | RIGHT | FULL\} [OUTER] JOIN + USING <colonne>$
dove “outer“ è opzionale

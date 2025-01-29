---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
# Viste logiche
Le Viste Logiche o Viste o View possono essere definite come delle tabelle virtuali, i cui dati sono riaggregazioni dei dati contenuti nelle tabelle “fisiche” presenti nel database. 
Le tabelle fisiche sono gli unici veri contenitori di dati. 
Le viste forniscono una diversa visione dinamicamente aggiornata dei dati delle tabelle fisiche.
La vista appare all’utente come una normale tabella, in cui può effettuare interrogazioni e, limitatamente ai suoi privilegi, anche modifiche dei dati.

# Utilità delle viste
- Per nascondere certe modifiche all’organizzazione logica dei dati (indipendenza logica) 
- Per offrire visioni diverse degli stessi dati senza ricorrere a duplicazioni 
- Per rendere più semplici, o per rendere possibili, alcune interrogazioni
## Vantaggi
Le viste semplificano la rappresentazione dei dati.
Oltre ad assegnare un nome alla vista, la sintassi dell’istruzione `CREATE VIEW` consente di cambiare i nomi delle colonne.

Le viste possono essere anche estremamente convenienti per svolgere una serie di query molto complesse.

Le viste consentono di proteggere i database: le view ad accesso limitato possono essere utilizzate per controllare le informazioni alle quali accede un certo utente del database.

Le viste consentono inoltre di convertire le unità di misura e creare nuovi formati.

In generale uno dei requisiti per la progettazione di un database relazionale è la [[Normalizzazione di schemi|normalizzazione]] dei dati.
Sebbene la [[Forme normali|forma normalizzata]] del database permette una corretta modellazione della realtà che il DB rappresenta, a volte dal punto di vista dell’utente comporta una maggiore difficoltà di comprensione rispetto a una rappresentazione non normalizzata. 
Le viste permettono di fornire all’utente i dati in una forma più intuitiva.

Esistono dei dati che sono presenti nelle tabelle del database, che sono poco significativi per l’utente, e altri che devono essere nascosti all’utente (esempio: lo stipendio di un dipendente, la password di un account etc.). 
L’uso delle viste da parte dell’utente permette di limitare il suo accesso ai dati del database, eliminando quelli non interessanti per lui e quelli che devono essere tenuti nascosti. 
L’uso delle viste può essere considerato come una tecnica per assicurare la sicurezza dei dati.

Un vantaggio delle viste riguarda __l’indipendenza logica__ delle applicazioni e delle operazioni eseguite dagli utenti rispetto alla struttura logica dei dati. 
Ciò significa che è possibile poter operare modifiche allo schema senza dover apportare modifiche alle applicazioni che utilizzano il database.

## Limitazioni
Non è possibile utilizzare gli operatori booleani `UNION`, `INTERSECT` ED `EXCEPT`; 
Gli operatori intersect ed except possono essere realizzati mediante una select semplice mentre l'union no.
Non è possibile utilizzare la clausola `ORDER BY`.


## Sintassi
l comando DDL che consente di definire una vista ha la seguente sintassi :
```MYSQL
CREATE VIEW NomeVista [ ( ListaAttributi ) ] AS SelectSQL [ with [ local | cascaded ] check option ] 
```
I nomi delle colonne indicati nella lista attributi sono i nomi assegnati alle colonne della vista, che corrispondono ordinatamente alle colonne elencate nella select. 
Se questi non sono specificati, le colonne della vista assumono gli stessi nomi di quelli della/e tabella/e a cui si riferisce.

Esempio:
Creare una vista contenente la matricola, il nome, il cognome e lo stipendio degli impiegati del dipartimento di Amministrazione il cui stipendio è maggiore di 1000 euro 
```MYSQL
Create view ImpiegatiAmmin 
	(Matricola, Nome, Cognome, Stipendio) AS 
	Select Matr, Nome, Cognome, Stip 
	From Impiegato 
	Where Dipart = 'Amministrazione' and Stipendio > 1000
```
La vista ottenuta è composta da quattro colonne denominate Matricola, Nome, Cognome, Stipendio corrispondenti agli attributi Matr, Nome, Cognome, Stip della tabella Impiegato e contiene i valori che soddisfano la clausola WHERE

## Modifica di una vista
Sebbene il contenuto di una vista sia dinamico, la sua struttura non lo è. 
Se una vista è definita su una subquery `Select * From T1` ed in seguito alla tabella T1 viene aggiunta una colonna, questa nuova definizione non si estende alla vista.
Ossia la vista conterrà sempre le stesse colonne che aveva prima dell’inserimento della nuova colonna in T1.

## Viste di gruppo
Una vista di gruppo è una vista in cui una delle colonne è una funzione di gruppo.
In questo caso è obbligatorio assegnare un nome alla colonna della vista corrispondente alla funzione di gruppo
![[Pasted image 20240224001922.png]]
Una vista di gruppo è anche una vista che è definita in base ad una vista di gruppo.
![[Pasted image 20240224002015.png]]
## Eliminazione delle viste
Le viste si eliminano col comando `DROP VIEW`. 

Sintassi: `Drop View nome_view {Restrict/Cascade}` 

- `Restrict`: la vista viene eliminata solo se non è riferita nella definizione di altri oggetti 
- `Cascade`: oltre che essere eliminata la vista, vengono eliminate tutte le dipendenza da tale vista di altre definizioni dello schema

## Tabelle inizializzate e tabelle calcolate
![[Pasted image 20240224002238.png]]

## Viste modificabili
Le tabelle delle viste si interrogano come le altre, ma in generale non si possono modificare. 

Deve esistere una corrispondenza biunivoca fra le righe della vista e le righe di una tabella di base, ovvero: 
1. SELECT senza DISTINCT e solo di attributi 
2. FROM una sola tabella modificabile  
3. WHERE senza SottoSelect 
4. GROUP BY e HAVING non sono presenti nella definizione.

Possono esistere anche delle restrizioni su SELECT su viste definite usando GROUP BY.
### Aggiornamento della vista
Le operazioni INSERT/UPDATE/DELETE sulle VIEW non erano permesse nelle prime edizioni di SQL.
I nuovi DBMS permettono di farlo con certe limitazioni dovute alla definizione della VIEW stessa.
Può essere utile aggiornare la vista  nel caso di [[SQL DDL - Controllo degli accessi|accesso dati controllato]].
![[Pasted image 20240224002552.png]]
![[Pasted image 20240224024853.png]]
![[Pasted image 20240224024907.png]]
### Operazione `with check option`
L’opzione With Check Option messa alla fine della definizione della vista assicura che le operazioni di inserimento e di modifica dei dati effettuate utilizzando la vista soddisfino la clausola Where della subquery.
![[Pasted image 20240224024840.png]]

Supponiamo che una vista V1 sia definita in termini di un’altra vista V2. 
Se si crea V1 specificando la clausola WITH CHECK OPTION, il DBMS verifica che la nuova tupla t inserita soddisfi sia la definizione di V1 che quella di V2 (e di tutte le altre eventuali viste da cui V1 dipende), indipendentemente dal fatto che V2 sia stata a sua volta definita WITH CHECK OPTION.
Questo comportamento di default è equivalente a definire V1
```MYSQL
WITH CASCADED CHECK OPTION 
```
Lo si può alterare definendo V1 
```MYSQL
WITH LOCAL CHECK OPTION 
```
Ora il DBMS verifica solo che t soddisfi la specifica di V1 e quelle di tutte e sole le viste da cui V1 dipende per cui è stata specificata la clausola WITH CHECK OPTION
![[Pasted image 20240224025116.png]]
### Esempi non standard
Il dipartimento che impiega il massimo budget in stipendi dei dipendenti 
```MYSQL
Select Dipart 
	from Impiegato 
	group by Dipart 
	having sum(Stipendio) >= all 
		(select sum(Stipendio) 
		from Impiegato 
		group by Dipart)
```

- Soluzione con le viste
```MYSQL
CREATE VIEW BudgetStipendi(Dipartimento,TotaleStipendi) AS 
SELECT Dipart, sum(Stipendio) 
FROM Impiegato 
GROUP BY Dipart 

SELECT Dipartimento 
FROM BudgetStipendi 
WHERE TotaleStipendi = (SELECT max(TotaleStipendi) 
					   FROM BudgetStipendi)
```
La vista è utilizzata come una normale tabella. 
Di solito vengono utilizzate in questo modo quando si devono usare a catena due diversi operatori aggregati (la massima somma, il minimo numero…)


Calcolare la media del numero degli uffici distinti presenti in ogni dipartimento :
- Interrogazione scorretta in quanto ci sono due operatori aggregati annidati 
```MYSQL
SELECT avg(count(distinct Ufficio)) 
FROM Impiegato 
GROUP BY Dipart 
```
- Con una vista 
```MYSQL
CREATE VIEW UfficiDipart (NomeDip,NroUffici) AS 
SELECT Dipart, count(distinct Ufficio) 
FROM Impiegato GROUP BY Dipart 

SELECT avg(NroUffici) 
FROM UfficiDipart
```

![[Pasted image 20240224001844.png]]
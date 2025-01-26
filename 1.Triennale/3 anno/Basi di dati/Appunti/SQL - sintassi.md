---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-21
Esempi: "[[Esempi SQL]]"
---
# SELECT, WHERE & FROM

Le query vengono effettuate mediante il comando `Select`

Sintassi :
```SQL
SELECT ListaAttributi 
FROM ListaTabelle 
[ WHERE Condizione ]
```

bisogna specificare 
- la _target list_, ossia la lista degli attributi interessati. Specificandola si scelgono alcuni degli attributi della/e tabella/e considerata/e.
	Implementa l'operazione di proiezione dell'[[Modello relazionale - Algebra relazionale|algebra relazionale]] ( $\pi_{X}(R)$ )
	![[Pasted image 20240221041006.png]]
- la clausola `FROM` per stabilire in quale/quali tabella/tabelle sono contenuti i dati che ci occorrono. Sceglie le tabelle del database da cui vogliamo estrarre le informazioni.
	Se le tabelle sono 2 la clausola `FROM` insieme alla clausola `WHERE` implementa il _theta join_. ($R\Join _{cond} S$)
	![[Pasted image 20240221041539.png]]
- la clausola `WHERE` per esprimere le condizioni che i dati cercati devono soddisfare. Serve a scegliere le righe della tabella che soddisfano una certa condizione.
	Implementa la selezione dell'[[Modello relazionale - Algebra relazionale|algebra relazionale]] ( $\sigma_{cond}(R)$ )


La query considera il prodotto cartesiano tra le tabelle in $ListaTabelle$ ($\Join$), fra queste selezione solo le righe che soddisfano la $Condizione$ ($\sigma$) ed infine valuta le espressioni specificate nella target list $ListaAttributi$ ($\pi$).
-> La `SELECT` implementa quindi : proiezione, selezione e join
![[Pasted image 20240221190025.png]]
# Lista degli attributi

![[Pasted image 20240221042103.png]]

# FROM - Lista delle tabelle - JOIN

![[Pasted image 20240221042146.png]]

# Condizione

![[Pasted image 20240221042205.png]]



# Sintassi della SELECT - Proiezione

- Sottoselct : 
```SQL
	SELECT [DISTINCT] Attributi
	FROM Tabelle
	[WHERE Condizione]
	[GROUP BY A1, ..., An [HAVING Condizione]] 
```
- Select :
```SQL
Sottoselect
	{(UNION | INTERSECT | EXCEPT)
	Sottoselect}
	[ORDER BY Attributo [DESC] {, Attributo [DESC]}]

```

Esempio : $\pi _{Lista Di Tutti Gli Attributi } (Persone)$
``` SQL
SELECT *
FROM Persone
```
Per selezionare tutti gli attributi si usa *

# WHERE - Selezione

Si può effettuare la selezione con la clausola `WHERE` che permette di specificare le condizioni che devono soddisfare le righe cercate. Questa clausola è opzionale e si si omette si selezionano tutte le righe della tabella specificata.

Esempio : $\pi_{nome, eta, reddito}(\sigma _{eta<30}(Persone))$
```SQL
SELECT nome, eta, reddito
FROM persone 
WHERE eta < 30
```

La condizione che segue il costrutto `WHERE` è una condizione booleana. Fa quindi uso di :
	- Operatori di confronto: =, <, >, <> o $\neq$ , $\leq$, $\geq$ 
	- Connettori logici : AND, OR, NOT
	- Operatori di confronto BETWEEN, IN, LIKE, IS NULL

# Alias delle colonne - Ridenominazione

L'alias serve a dare a una colonna un nome diverso rispetto a quello che è utilizzato nella definizione della tabella.
Implementa l'operatore di ridenominazione ($\rho_ {a\leftarrow b}(R)$).
si usa la parola `AS` tra il nome della colonna e l'alias.
L'alias richiede le virgolette se ci sono degli spazi

```SQL
SELECT Figlio AS Filglio_M
FROM Maternita
```

# Operatori
Tutti gli operatori sono presenti anche in forma _negativa_ aggiungendo un NOT davanti (`NOT BETWEEN`, `NOT IN`, `NOT LIKE`, `IS NOT NULL`)
- `BETWEEN` consente la selezione di righe con attributi in un particolare range
	Esempio: Cercare gli impiegati (nome e dipartimenti) che guadagnano tra 1000 e 1500 euro e visualizzare nome e dipartimento
``` SQL
SELECT nome, dipartimento 
FROM Impegati
WHERE Stipendi BETWEEN 1000 AND 1500
```

- `IN` si usa per selezionare le righe che hanno un attributo che assume valori contenuti in una lista
	Esempio : selezionare i nomi dei professori che tengono i corsi di BD1, BD2, Algoritmi e Sistemi
``` SQL
	SELECT Nome
	FROM Insegnanti
	WHERE Corso IN ('BD1', 'BD2', 'Algoritmi', 'Sistemi' )
```

- `LIKE` è usato per effettuare ricerche 'wildcard', ossia con un simbolo jolly di una stringa di valori. Le condizioni di ricerca possono contenere letterali, caratteri o numeri. Esistono 2 tipi di wildcard: 
	- %, denota 0 o più caratteri 
	- _ denota un carattere
	
	Esempio: Fra le persone elencate nella tabella Persone, determinare quelle il cui nome termina per 'a'
``` SQL
SELECT *
FROM Persone
WHERE Nome LIKE '%a'
```
A volte può succedere che uno dei simboli coinvolti nel pattern matching sia proprio _ oppure %.
In questo caso, si sceglie un simbolo che non è ammesso fra i simboli della stringa (supponiamo ‘#’) detto simbolo `ESCAPE`, nell’espressione per la ricerca si fa precedere il simbolo _ o % cercato dal simbolo escape, e poi si specifica che ‘#’ e’ il simbolo di escape.
	Esempio : Modelli il cui nome inizia per C_F
``` SQL
SELECT *
FROM Modelli 
WHERE nome_modello LIKE 'C#_F%' ESCAPE '#' 
```

- `ISNULL` è una soluzione al fatto che il valore di una ennupla può mancare per vari motivi. Verifica se il contenuto di un operando è Null.
	- `A IS NULL` è true se A vale NULL, false altrimenti
	- `A IS NOT NULL` è true se A non vale Null, false altrimenti 
	Esempio : Selezionare i veicoli che non hanno valore per la cilindrata
``` SQL
SELECT *
FROM Veicoli 
WHERE Cilindrata IS NULL  
```
I valori NULL rappresentano l’assenza di informazione, cioè:

- Valore sconosciuto
- Valore non disponibile
- Attributo non disponibile

Ciascun valore NULL è considerato _diverso_ dagli altri valori NULL

Il risultato del confronto logico con un valore che è NULL da come output: sconosciuto (UNKNOWN).
Non viene visualizzato l'unknown 

**Tabelle**
-  _AND_
        
| Primo | Secondo | Result |
        | --- | --- | --- |
        | T | S | S |
        | F | T | F |
        | F | S | F |
        
- _OR_
        
|Primo|Secondo|Result|
        |---|---|---|
        |T|S|T|
        |F|T|T|
        |F|S|S|
        
- NOT

| Primo | Result |
| ---- | ---- |
| T | F |
| F | T |
| S | S |
![[Pasted image 20240221180529.png]]
![[Pasted image 20240221180754.png]]

# Ordinamento, operatori aggregati e raggruppamento 
## Ordinamento del risultato 

Si ha la possibilità di dare un ordinamento del risultato di una SELCT in base ad _un'attributo crescente o decrescente_. 
Si usa la clausola `ORDER BY Attributo [ASC/DESC]`
Le righe vengono quindi ordinate in base ad Attributo in modo Crescente o Decrescente. Se non si specifica l'ordine il default è ascendente. 
	Esempio : Trovare nome e reddito delle persone con meno di trenta anni in ordine alfabetico
```SQL
SELECT Nome, Reddito
FROM Persone 
WHERE Eta < 30
ORDER BY Nome
```

Si può voler ordinare i dati in base a una certa chiave (attributo) e poi ordinare i dati che coincidono su quella chiave in base a un’altra chiave (attributo) ed effettuare coì un **Doppio ordinamento**.
	Esempio: ordinare gli studenti in base al loro cognome, in modo tale che due persone con lo stesso cognome siano ordinate in base al nome, e persone con lo stesso nome e cognome siano ordinate in base all’ordine inverso della data di nascita
```SQL
SELECT *
FROM Studenti 
ORDER BY Cognome, Nome, DataNascita [DESC] 
```


## Operatori aggregati 
Nella target list si possono avere anche espressioni che calcolano i valori a partire da insiemi di ennuple e che restituiscono una tabella molto particolare, costituita da un singolo valore scalare.
Esistono 5 possibili operatori aggregati :
`COUNT` : conteggio
`MIN`  : minimo
`MAX` : massimo
`AVG` : media
`SUM` : somma

Se un argomento è null lo è l'intera espressione

Non è possibile utilizzare in una stessa select una proiezione su alcuni attributi della tabella considerata e operatori aggregati sulla stessa tabella.

O si usano le proiezioni normali o gli operatori aggregati.
Si possono usare più operatori aggregati insieme.
### COUNT
`COUNT` restituisce il numero di righe della tabella o il numero di valori di un particolare attributo
	Esempio : Il numero di figli di Franco
```SQL
SELECT count(*) as NFigliFranco
FROM Paternita
WHERE Padre = 'Franco'
```
- ( * ) seleziono tutte le righe
- ALL : tutti i valori non nulli delle righe selezionate
- DISTINCT : tutti i valori non nulli distinti delle righe

Se la specifica viene omessa di default è ALL

### MAX e MIN
Le funzioni MAX e MIN calcolano rispettivamente il maggiore e il minore degli elementi di una colonna. L’argomento delle funzioni max e min può anche essere un’espressione aritmetica.

### SUM
La funzione SUM calcola la somma dei valori di una colonna. 
Le specifiche ALL e DISTINCT permettono di sommare tutti i valori non nulli o tutti i valori distinti. 
Il default in mancanza di specifiche è ALL

### AVG
G La funzione AVG calcola la media (average) dei valori non nulli di una colonna. Le specifiche ALL e DISTINCT servono a calcolare la media fra tutti i valori o tra i valori distinti. 
Il default è ALL.

## Raggruppamento - `GROUP BY` 
A volte può essere richiesto di calcolare operatori aggregati non per l’intera tabella, ma raggruppando le righe i cui valori coincidono su un certo attributo. 
Si usa la clausola `GROUP BY`.
	Esempio: si vuole sapere la media degli stipendi degli impiegati per ogni dipartimento.
```SQL
	SELECT Dipart, AVG(stipendio) 
	FROM Impiegati 
	GROUP BY Dipart
```
Si può mettere nella target list Dipartimento in quanto ho raggruppato per i dipartimenti.
Quando si effettua un raggruppamento, questo deve essere effettuato su tutti gli elementi della target list che non sono operatori aggregati (ossia sull’insieme degli attributi puri). 
Questo ha senso perché nel risultato deve apparire una riga per ogni «gruppo».
Si possono usare anche gli operatori aggregati ma devono essere differenti da quelli che si raggruppano.
Tutti gli attributi che si proiettano quando si raggruppa devono essere raggruppati

Se la SELECT contiene sia espressioni aggregate (MIN, COUNT…) che attributi non aggregati, allora DEVE essere presente la clausola GROUP BY
## Condizioni sui gruppi - `HAVING`
Si possono applicare condizioni sul valore aggregato per ogni gruppo mediante la clausola HAVING.
	Esempio:  I dipartimenti la cui media degli stipendi è maggiore di 1700 euro
```SQL
SELECT Dipart, AVG(stipendio) 
FROM Impiegati 
Group by Dipart 
HAVING AVG(stipendio)>1700
```

Se la condizione coinvolge un attributo, si usa la clausola `WHERE`, mentre se coinvolge un operatore aggregato si usa la clausola `HAVE`.
![[Pasted image 20240221190056.png]]
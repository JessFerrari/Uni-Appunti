---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - esempio
  - BD
Creation: 2024-02-21
---
![[Pasted image 20240221042737.png]]
![[Pasted image 20240221042753.png]]

- Tutti gli attributi della tabella persone
$\pi _{Lista Di Tutti Gli Attributi } (Persone)$
``` SQL
SELECT *
FROM Persone
```

Trovare nome, età e reddito delle persone con meno di 30 anni
$\pi_{nome, eta, reddito}(\sigma _{eta<30}(Persone))$
```SQL
SELECT nome, eta, reddito
FROM persone 
WHERE eta < 30
```

Trovare tutti i dati degli studenti di Pisa 
$\pi_{tuttiIDati}(\sigma _{Provincia = 'PI'}(Studenti))$
``` SQL
SELECT *
FROM Studenti
WHERE Provincia = 'PI'
```

Trovare la matricola, l'anno di nascita e il nome degli studenti di Pisa
$\pi_{matricola, annoDiNascita, nome}(\sigma _{Provincia = 'PI'}(Studenti))$
``` SQL
SELECT Nome, Matricola, AnnoDiNascita
FROM Studenti
WHERE Provincia = 'PI'
```


### Prodotto e giunzione 

Trovare tutte le possibili coppie Studenti-Esame
``` SQL
SELECT *
FROM Studenti, Esami
```

Trovare tutte le possibili coppie Studenti-Esame sostenuto dello studente
``` SQL
SELECT *
FROM Studenti s, Esami e
WHERE s.Matricola = e.Matricola
```

Trovare il nome e la data degli esami per gli studenti che hanno superato l'esame di BD con 30

``` SQL
SELECT Nome, Data
FROM Studenti s, Esami e
WHERE s.Matricola=e.Matricola AND e.Materia='BD' AND e.Voto=30
```

# SQL - operatori di confronto

Selezionare le persone che si chiamano Mario
``` SQL
SELECT *
FROM Persone
WHERE Nome = 'Mario'
```

Selezionare gli impiegati che guadagnano più di 1200 euro
``` SQL
SELECT *
FROM Impiegato
WHERE stipendi > 1200
```

Selezionare il nome e il cognome delle persone che non hanno età superiore a 30 anni

``` SQL
SELECT Nome, Cognome
FROM Persone
WHERE eta <= 30
```

Selezionare tutti gli impiegati tranne quelli che lavorano nel dipartimento di produzione 
``` SQL
SELECT *
FROM Impegati
WHERE Dipartimento <> 'Produzione'
```

Cercare gli impiegati (nome e dipartimenti) che guadagnano tra 1000 e 1500 euro e visualizzare nome e dipartimento
``` SQL
SELECT nome, dipartimento 
FROM Impegati
WHERE Stipendi BETWEEN 1000 AND 1500
```

Selezionare i nomi dei professori che tengono i corsi di BD1, BD2, Algoritmi e Sistemi
``` SQL
SELECT Nome
FROM Insegnanti
WHERE Corso IN ('BD1', 'BD2', 'Algoritmi', 'Sistemi' )
```

Selezionare le persone che hanno più di 30 anni e che non abitano a Pisa
``` SQL
SELECT *
FROM Persone
WHERE eta > 30 AND NOT(citta='Pisa')
```

Selezionare gli impiegati che lavorano nel dipartimento di produzione e quelli che lavorano in segreteria

``` SQL
SELECT *
FROM Impiegati
WHERE Dipartimento = 'Produzione' AND dipartimento = 'Segrteria'
```

Fra le persone elencate nella tabella Persone, determinare quelle il cui nome termina per 'a'
``` SQL
SELECT *
FROM Persone
WHERE Nome LIKE '%a'
``` 

Selezionare le sequenze di DNA in cui ci sono almeno due simboli ‘G’ che distano 3 caratteri
``` SQL
SELECT *
FROM DNA
WHERE Seq LIKE '%G___G%'
``` 

Modelli il cui nome inizia per C_F
``` SQL
SELECT *
FROM Modelli 
WHERE nome_modello LIKE 'C#_F%' ESCAPE '#' 
```

Selezionare i veicoli che non hanno valore per la cilindrata
``` SQL
SELECT *
FROM Veicoli 
WHERE Cilindrata IS NULL  
```

Selezionare gli impiegati che hanno più di 40 anni o che non è specificata l'età
``` SQL
SELECT *
FROM Impiegati
WHERE Età>40 OR Età IS NULL
```

### Esempi particolari target list

Evidenziare i cognomi degli impiegati e il loro stipendio aumentato del 20%
```SQL
SELECT Cognome, Stipendio * (120/100)
FROM Impiegati
```

Evidenziare i cognomi degli impiegati e il loro stipendio aumentato del 20% e rinominare la colonna corrispondente al salario aumentato con la denominazione “Aumento”
```SQL
SELECT Cognome, Stipendio * (120/100) AS Aumento
FROM Impiegati
```


### ORDER BY
Trovare nome e reddito delle persone con meno di trenta anni in ordine alfabetico
```SQL
SELECT Nome, Reddito
FROM Persone 
WHERE Eta < 30
ORDER BY Nome
```

Ordinare gli studenti in base al loro cognome, in modo tale che due persone con lo stesso cognome siano ordinate in base al nome, e persone con lo stesso nome e cognome siano ordinate in base all’ordine inverso della data di nascita
```SQL
SELECT *
FROM Studenti 
ORDER BY Cognome, Nome, DataNascita [DESC] 
```

## Operatori aggregati 
Restituire il numero di figli di Franco
```SQL
SELECT count(*) as NFigliFranco
FROM Paternita
WHERE Padre = 'Franco'
```

Contare il numero di studenti iscritti al corso di BD e di Laboratorio di Basi di Dati
```SQL
SELECT count(*) as nStudenti
FROM EsamiBD
```

Contare il numero di esami di BD superati positivamente 
``` SQL
SELECT count([ALL] BD) “ContaBD” 
FROM EsamiBD
```

Numero di voti distinti dati all’esame di LBD 
```SQL
SELECT count(distinct LBD) “ContDistLBD” 
FROM EsamiBD
```

L’età della persona più anziana nella tabella persone
```SQL
SELECT max(Eta)
FROM Persone
```

Il più basso dei voti assegnati all’esame di BD
```SQL
SELECT min(Voti)
FROM EsamiBD
```

Calcolare la somma degli stipendi mensili degli impiegati del settore Produzione.
```SQL
SELECT SUM (ALL Stipendio)
FROM Impiegati
WHERE Dipartimento = 'Produzione'
```

Calcolare la media degli stipendi degli impiegati del dipartimento di Produzione e che hanno meno di 30 anni
```SQL
SELECT AVG (ALL Stipendio)
FROM Impiegati
WHERE Dipartimento = 'Produzione' AND Eta<30
```
Studenti ordinati per Nome 
```SQL
SELECT * 
FROM Studenti 
ORDER BY Nome;
```

Numero di elementi di Studenti 
```SQL
SELECT count(*) 
FROM Studenti;
```


Anno di nascita minimo, massimo e medio degli studenti: 
```SQL
SELECT min(AnnoNascita), max(AnnoNascita), avg(AnnoNascita) 
FROM Studenti;
```


## GRUP BY e HAVING 

si vuole sapere la media degli stipendi degli impiegati per ogni dipartimento.
```SQL
	SELECT Dipart, AVG(stipendio) 
	FROM Impiegati 
	GROUP BY Dipart
```

 I dipartimenti la cui media degli stipendi è maggiore di 1700 euro
```SQL
SELECT Dipart, AVG(stipendio) 
FROM Impiegati 
Group by Dipart 
HAVING AVG(stipendio)>1700
```

Le città per cui la media dei voti dei suoi studenti di meno di 21 anni è maggiore di 26 
```SQL
SELECT città, avg(voto) 
FROM EsamiBD 
WHERE eta < 21 
GROUP BY città 
HAVING avg(voto) > 26
```


## [[SQL e algebra relazionale]]
![[Pasted image 20240221233906.png]]

## JOIN
![[Pasted image 20240222214527.png]]
![[Pasted image 20240222214537.png]]
![[Pasted image 20240222214612.png]]
![[Pasted image 20240222214625.png]]

---
![[Pasted image 20240222214638.png]]

---
![[Pasted image 20240222214855.png]]

---
![[Pasted image 20240222215149.png]]

---
![[Pasted image 20240222215208.png]]


## Join su più tabelle
![[Pasted image 20240222215255.png]]
![[Pasted image 20240222215310.png]]

## Clausola JOIN
![[Pasted image 20240222215536.png]]

---
![[Pasted image 20240223044333.png]]

---

![[Pasted image 20240223044526.png]]


----
![[Pasted image 20240223044627.png]]

--- 
![[Pasted image 20240223045535.png]]

---
![[Pasted image 20240223045718.png]]


---
![[Pasted image 20240223045739.png]]


---
![[Pasted image 20240223045750.png]]

---
![[Pasted image 20240223045804.png]]

---
![[Pasted image 20240223045817.png]]

---
![[Pasted image 20240223045837.png]]

![[Pasted image 20240223045859.png]]

---
![[Pasted image 20240223050004.png]]

---
![[Pasted image 20240223050111.png]]

---
![[Pasted image 20240223051211.png]]

---
![[Pasted image 20240223051343.png]]

---
![[Pasted image 20240223051406.png]]

---
![[Pasted image 20240223051427.png]]

---
![[Pasted image 20240223051449.png]]
![[Pasted image 20240223051501.png]]
![[Pasted image 20240223051604.png]]
![[Pasted image 20240223051617.png]]![[Pasted image 20240223051628.png]]

---
![[Pasted image 20240223051704.png]]![[Pasted image 20240223051726.png]]

---

![[Pasted image 20240223052502.png]]

---

![[Pasted image 20240223051809.png]]
![[Pasted image 20240223051821.png]]

---
![[Pasted image 20240223051856.png]]
![[Pasted image 20240223051922.png]]

---
![[Pasted image 20240223051949.png]]
![[Pasted image 20240223052000.png]]

![[Pasted image 20240223052013.png]]

![[Pasted image 20240223052040.png]]

---
---
![[Pasted image 20240223052114.png]]
![[Pasted image 20240223052126.png]]

---
---
![[Pasted image 20240223052159.png]]

![[Pasted image 20240223052220.png]]
![[Pasted image 20240223052240.png]]![[Pasted image 20240223052252.png]]![[Pasted image 20240223052304.png]]![[Pasted image 20240223052318.png]]

---
----
---
![[Pasted image 20240223053205.png]]
![[Pasted image 20240223053217.png]]

---
![[Pasted image 20240223053237.png]]


---

![[Pasted image 20240223054655.png]]
![[Pasted image 20240223054713.png]]

![[Pasted image 20240223055259.png]]


---
---
---
[[SQL - Data Definition Language (DDL)]]

![[Pasted image 20240223061526.png]]
---
Subject: "[[Indice - Basi di dati]]"
tags:
  - BD
Creation: 2024-02-21
Slide: "[[ALL_BD.pdf|da slide 540 a 840]]"
Esempi: "[[Esempi SQL]]"
Esercizi: "[[Esercizi SQL]]"
---
 # Interrogazione di una base dati
L’interrogazione di una base di dati è uno degli aspetti più importanti del linguaggio SQL. 
I comandi di interrogazione, o QUERY, permettono di effettuare una ricerca dei dati presenti nel database che soddisfano particolari condizioni, richieste dall’utente

Esempio:
```SQL
SELECT s.Nome, e.Data
FROM Studenti s, Esami e
WHERE e.Materia = 'BD' AND e.Voto = 30 AND e.Matricola = s.Matricola

SELECT s.Nome As Nome, 2018 - s.AnnoNascita As Eta,0 As NumeroEsami

FROM Studenti s
WHERE NOT EXISTS (SELECT * FROM Esami e WHERE e.Matricola = s.Matricola 
```

Nei linguaggi di interrogazione di basi di dati si distinguono: 
- [[DML|Data Manipulation Language (DML)]], per l'interrogazione e l'aggiornamento di istanze di basi di dati 
- [[DDL|Data Definition Language (DDL)]], per la definizione di schemi e altre operazioni, come la creazione di tabelle

SQL è un calcolo su multiinsiemi, ossia gestisce le ripetizioni.



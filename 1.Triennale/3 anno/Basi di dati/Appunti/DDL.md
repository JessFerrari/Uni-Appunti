---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS]]"
tags:
  - BD
Creation: 2024-02-08
---
![[08_DDL.png]]
_Data Definition Language_ (DDL) è un linguaggio per la definizione di schemi (logici, esterni, fisici) e altre operazioni generali

```sql
CREATE TABLE orario (
    insegnamento CHAR(20),
	docente      CHAR(20),
	  aula         CHAR(4),
    ora          CHAR(5)
)
```


Il DDL è un linguaggio per la definizione di basi di dati diviso in 3 livelli:
- Vista Logica (o vista esterna o vista)
- Schema Logico
- Schema Fisico

Il livello di vista serve per far vedere i dati, ma solo quelli che si scelgono che devono essere visti. Descrive come deve apparire la struttura della base di dati ad una certa applicazione (Schema esterno o vista).

Esempio di vista logica: 

```sql
InfCorsi (IdeC char(8), Titolo char(20), NumEsami int)
```


Il livello logico descrive la struttura degli insieme dei dati e delle relazioni fra loro, secondo un certo modello dei dati, senza nessun riferimento alla loro organizzazione fisica nella memoria permanente (Schema logico).

Esempio di schema logico:

```sql
Studenti(Matricola char(8), Nome char(20), login char(8), AnnoNascita int, Reddito real)
Corsi(IdeC char(8), Titolo char(20), Credito int)
Esami(Matricola char(8), IdeC char(8), Voto int)
```

Il livello fisico è come io voglio rappresentare i dati. Descrive come vanno organizzati fisicamente i dati nelle memorie permanenti e quali strutture dati ausiliarie prevedere per facilitarne l’uso (Schema fisico o interno).

Esempio di schema fisico: 
Relazioni Studenti e Esami organizzate in modo seriale, Corsi organizzata sequenziale con indice.

I tre livelli favoriscono l'indipendenza fisica e l'indipendenza logica:
	- Indipendenza fisica: i programmi operativi non devono essere modificati in seguito a modifiche dell'organizzazione fisica dei dati
	- Indipendenza logica: i programmi applicativi non devono essere modificati in seguito a modifiche dello schema logico.
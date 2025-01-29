---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Base di dati]]"
tags:
  - BD
  - esempio
Creation: 2024-02-08
---
Definizione di basi di dati
```SQL
create database EsempioEsami
```
Definizione schema:

```sql
create table Esami (Materia char(5), Candidato char(8),
Voto int, Lode char(1),Data char(6))
```

Inserzione dati:

```sql
insert into Esami values ('BDSI1','080709',30, 'S',
070900)
```

Interrogazione:

```sql
select Candidato
from Esami 
where Materia = "BDSI1" and Voto = 30
```

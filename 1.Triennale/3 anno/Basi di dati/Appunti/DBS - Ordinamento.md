---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS]]"
tags:
  - BD
Creation: 2024-03-04
---
# Ordinamento di archivi

L’ordinamento di archivi è importante per il risultato ordinato di query (order by) e per eseguire alcune operazioni relazionali (come join, select distinct, group by).

> [!NOTE] Recap algoritmi di ordinamento
> [[Mergesort]] : costo $N*Log(N)$
> [[Quicksort]]

A livello di pagine si usa il [[DBMS - Merge sort Z-way|merge sort Z-way]], ma la sua utilità dipende dalla query in questione: se in prima di un [[SQL - sintassi#Ordinamento, operatori aggregati e raggruppamento|GROUP BY]] si ha una join allora si usa il [[DBMS - Nested loops|nested loop]]
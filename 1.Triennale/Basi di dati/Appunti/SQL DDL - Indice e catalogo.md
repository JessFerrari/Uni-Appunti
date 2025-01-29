---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
# Creazione di indici

Non è un comando standard dell'SQL e quindi ci sono differenze nei vari sistemi.

```MYSQL
 CREATE INDEX NomeIdx ON Tabella(Attributi) 
```
 
```MYSQL
  CREATE INDEX NomeIdx ON Tabella WITH STRUCTURE = BTREE, KEY = (Attributi) 
```
  
```MYSQL
   DROP INDEX NomeIdx
```

![[Pasted image 20240224031303.png]]![[Pasted image 20240224031315.png]]
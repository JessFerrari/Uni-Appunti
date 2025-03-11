---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Gerarchia di memoria]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
## Principio di località

In generale si ha una probabilità di avere un miss che si spera che sia bassa, ma questo non lo si può definire a priori ma dipende dal programma. Per ridurla si usa comunque un metodo chiamato PRINCIPIO DI LOCALITÀ. Tale principio non è solamente utilizzato solo per le gerarchie di memoria ma anche per tante strutture dati e algoritmi.

Facendo un' analisi dei programmi si è notato che la maggior parte tendono ad accedere alle stesse locazioni di memoria (LOCALITÀ SPAZIALE) per un determinato periodo di tempo (LOCALITÀ TEMPORALE) , in quanto non sono scritti per accedere in memoria in modo casuale.

Se non venisse usato tale principio il miss rate sarebbe molto alto, in quanto non verrebbero spostate nella cache gli indirizzi di memoria che si sa che si useranno.

Esistono quindi due tipo di località :

- Località spaziale, che si riferisce al fenomeno per cui i dati vicini a dati referenziati di recente sono più probabili ad essere acceduti. Ad esempio gli array all'interno di un loop. La gerarchia di memoria ne trae vantaggio muovendo i dati tra i vari livelli a blocchi.
- Località temporale, che si riferisce al fenomeno per cui i dati acceduti recentemente sono più probabili ad essere acceduti di nuovo. Ad esempio le variabili all'interno di un loop. La gerarchia di memoria ne trae vantaggio tenendo i dati recentemente referenziati vicino alla CPU.

I dati vengono trasferiti tra due livelli di memoria adiacenti alla volta e il processore accede solo al primo livello.

I dati vengono sempre trasferiti a blocchi sfruttando la località spaziale.
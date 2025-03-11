---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Cache]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---

### Direct mapped memory

La DIRECT MAPPED MEMORY, contiene tanti set quanti numero di blocchi, la capacità corrisponde ai blocchi per le parole che può contenere, C=B∗b, e per determinare l'indirizzo che la parola avrà in cache si fa : $\log_2B.$

![[DirectMapping.png.png]]


In questo caso particolare in cui b=1 e S=B=8 per determinare in quale set l'indirizzo dovrà andare ci serviranno $log_2 8=3$ bit.

Questo tipo di formazione in cui c'è solo 1 parola per blocco non viene usata in quanto non fa sfruttare la località spaziale, di solito se ne hanno 4 o 8.

Una parte dei bit dell'indirizzo sarà predisposta a mappare al set ma ovviamente ci saranno più indirizzi che vengono mappati al solito set e quindi per distinguere i vari indirizzi si utilizzano i TAG composti dai bit più significativi dell'indirizzo.

Siccome si potranno avere dei dati non significativi nella cache dovremmo anche riservare un bit per la validità.

![[memory pt2.png]]

Una parte dei bit indicherà a quale set appartiene il dato, e mediante un comparatore si andrà a verificare se i tag corrispondono, e in tal caso vorrà dire che si è trovato il dato.

Se vado ad utilizzare la località spaziale, e quindi avere più parole per blocco, gli ultimi bit che prima essendo tutti multipli di 4 erano sempre 00, ora vanno a ricoprire un ruolo importante in quanto diventano le entrate di un mux con il quale si selezionerà la parola del blocco.![[memoria pt3.png]]


Si verifica trashing quando si hanno sempre miss e alla fine la lettura diventa lunga come quella in memoria

PRO :

- È semplice da realizzare
- Nel caso di cache hit è molto veloce

CONTRO :

- È molto rigido
- Possono essere presenti molti conflitti
---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Cache]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
## Gestione delle scritture

Facendo le scritture si possono avere due casi :

- WRITE HITS (solito tag) : se l'istruzione di store scrivesse i dati solo nella cache allora a quel punto la cache e la memoria principale avrebbero dati diversi rendendo la memoria inconsistente.

Si risolve attraverso due tecniche : write through e write back

- WRITE MISSES (tag diverso) : si usano due strategie: la write allocate, con la quale si recuperano i blocchi dalla memoria in cache e poi si sovrascrive la parola mancante ( usata nella write back), e la no write allocate, con la quale si va a scrivere la parola direttamente nel livello successivo di memoria ( usata nella write through)
    
    ### WRITE THROUGHT
    
    Nella politica WRITE THROUGH quando si hanno dei write hits questi vengono sempre caricati sia nella cache che nel successivi livelli di memoria. Questa è una soluzione semplice, facile da implementare e i dati sono sempre uguali in tutti i livelli di memoria. Però la velocità di scrittura dipende dalla velocità del più basso livello di memoria, c'è quindi anche un maggior traffico in memoria dato che per ogni istruzione di scrittura ci possono essere scritture in tutti i livelli.
    
    ### WRITE BACK
    
    Nella politica WRITE BACK i write hits vengono caricati solo in cache e i blocchi modificati vengono aggiornati nei livelli inferiori solo quando quel blocco verrà espulso dalla cache. La velocità è quella della chache e c'è poco traffico in memoria rispetto alla write through. Si deve però tenere traccia dei blocchi modificati, c'è maggior complessità architetturale e le linee di cache potrebbero essere aggiornate costantemente.
    
    Il write back può aumentare le prestazioni soprattutto quando la CPU genera più istruzioni di store di quanto la memoria principale ne possa gestire. Tuttavia il costo di un cache write è più alto se viene effettuato un write miss in quanto si dovrebbe pima riscrivere il dato in memoria, se è stato modificato, e poi si può riutilizzare il blocco. Questo processo richiede almeno due cicli, uno per controllare il dato modificato e l'altro per scrivere, anche nel caso di write hit.
    
    ### ottimizzazioni
    
    Si può usare un write buffer per contenere contemporaneamente il dato da scrivere mentre il blocco di cache è controllato per verificare l'hit. Il processore guarda il dato e lo mette nel buffer durante il normale ciclo di accesso alla cache. Assumendo che sia un cache hit il nuovo dato verrà scritto dal buffer alla cache nel prossimo ciclo non utilizzato di accesso alla cache.
    
    Viene usato un write buffer per contenere le parole che verranno scritte in memoria. L'esecuzione continua immediatamente dopo aver scritto i dati nella cache e dentro il write buffer. Questo perché così le store nella memoria principale verranno fatte in parallelo con la computazione normale della CPU. La CPU stallerà solamente quando il write buffer sarà pieno quindi il traffico è un fattore critico soprattutto per il modello write through.
    

## Rimpiazzo

In una direct mapped cache il blocco richiesto può andare in una esatta posizione e quindi non si ha scelta. Se il blocco da rimpiazzare è stato modificato e si usa la write back bisogna aggiornare per forza i livelli più bassi di memoria.

In una cache associativa si ha la scelta di dove posizionare il blocco richiesto :

- Nella completamente associativa tutti i blocchi sono candidati al rimpiazzo
- Nella parzialmente associativa bisogna scegliere uno degli n blocchi del set

Per rimpiazzare i blocchi si possono usare due diverse politiche :

- LRU, LEAST RECEBTLY USED : è lo schema più usato, considera la località temporale, il blocco rimpiazzato è quello che è stato inusato per maggior tempo.

L'implementazione hardware è difficile, per un 2-way si può usare un bit che dirà di rimpiazzare l'altro, per un 4-way ne si può usare due ma pii diventa più complicato

- RANDOM : riesce ad avere più o meno le stesse prestazioni dello schema LRU


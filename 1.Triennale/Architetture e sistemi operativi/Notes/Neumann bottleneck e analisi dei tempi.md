---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Gerarchia di memoria]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---

## Neumann bottleneck e analisi dei tempi

Le memorie statiche sono molto veloci e vengono usate per i registri ma hanno un costo molto alto, mentre le memorie dinamiche, che hanno capacità maggiore, sono più lente, ma meno costose.

Dato che la memoria è più lenta del processore ci si ritrova nella situazione in cui non ci è possibile continuare ad effettuare calcoli senza aspettare una risposta dalla memoria, rallentando tutto il sistema (NEUMANN BOTTLENECK) Si vorrebbe quindi avere una memoria molto capiente, come una memoria dinamica, e contemporaneamente molto veloce come una memoria statica, in grado di superare velocemente il von Neumann bottleneck, ossia il ritardo dovuto alle prestazioni dell'architettura caratteristico delle macchine di von Neumann in quanto l'unità di controllo è separata dalla memoria. Però sono due necessità contrastanti e perciò devo creare l'illusione di avere nel complesso una memoria del genere usando l'intera gerarchia. Si divide quindi la memoria in livelli dove il livello più in alto è il più piccolo e il più veloce e quello più in basso è il più grande ma il più lento, e si vuole quindi dare l'illusione di avere una memoria grande quanto l'ultimo livello ma veloce quanto il primo.

All'inizio i dati si trovano nell'ultimo livello della memoria e quando vengono utilizzati questi vengono spostati dal livello n al livello soprastante n-1 e questo spostamento è invisibile al programmatore. A questo punto il livello soprastante n-1 contiene un sottoinsieme di dati presenti al livello n (INCLUSIVE MEMORY LEVELS).

Cosa succede però se il livello n-1 è pieno ? Devo togliere qualcosa da quel livello di memoria e per sapere cosa togliere ci sono diverse tecniche.

Quando si richiede un dato il processore fa sempre riferimento al livello più vicino, a quello più alto e se questo è presente in quel livello si dice che si fa HIT se invece non è presente si ha una MISS e allora si ha la necessità di andare a riprenderlo dai livelli sottostanti. Quando si ha una miss vengono scatenate una serie di azioni affinchè il dato non viene trasportato al livello giusto in modo che si abbia una hit.

Si hanno anche altre terminologie come :

- HIT RATE, ossia la frequenza con la quale si ha avuto hit
    
    $HR=\frac{\#hit}{\#accessi\ in\ memoria\ }=1-MR$
    
- MISS RATE, ossia la frequenza con cui ha avuto miss
    
    $MR=\frac{\#miss}{\#accessi \ in \ memoria}=1-HR$
    
- MISS PENALTY, ossia il tempo che si impiega per spostare il dato da n a n-1 (OVERHEAD)
    
- MISS TIME, ossia è il tempo totale che mi è costato per fare una hit (miss penalty + hit time)
    
- AMAT (AVARAGE MEMORY ACCESS TIME), ossia il tempo di accesso alla memoria cache.
    
    $AMAT=hit\ time+miss\ rate*(miss\ penalty)$
    
    $AMAT=t_{M_0}+MR_{M_0}*(t_{m_1}+MR_{M1}*(t_{M_2}+MR_{M_2}*(t_{M_3}...)))$
    
    $AMAT=hit\ time+(1-hit\ time)*miss\ penalty$


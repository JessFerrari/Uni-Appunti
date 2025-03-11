---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Gerarchia di memoria]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
## La cache

La cache è una piccola memoria vicina al processore che ha la funzione di evitare i lunghi tempi di accesso in memoria . All'interno di un'architettura ci sono diversi livelli di cache, di solito L1, L2 e L3, in cui la L!è privata mentre la L2 eL3 sono condivise. Le cache sono organizzate il linee ognuna delle quali contiene un blocco di memoria per le parole. La prima volta che un processore richiede una parola di memoria durante la fase di fetch si presenta un cache miss, successivamente il blocco contenente tale parola viene trasferito nella cache e poi viene rieseguito il calcolo avendo però una cache hit. Ad ogni richiesta se la parola è presente già all'interno della cache si ha un cache hit se no si presenta di nuovo un cache miss. Ovviamente sono più alti le hit che i miss. Avere un sistema di cache fa si che diminuisca il miss rate in quanto l'accesso in cache è più veloce rispetto all'accesso nella RAM.

Grazie all'utilizzo delle cache si ha un aumento delle prestazioni:

$CPU_{time}=ClockCicles_ClockClycleTime=IC_CPI*ClockCycleTime$

Dove IC (instruction count) è il numero di istruzioni eseguite e CPI (ClockCycle Per Instruction) è definito come $\frac{ClockCycle}{IC}$. quanti cicli di clock utilizza per istruzione.

il $CPU_{time}$ può essere ulteriormente suddiviso in $CPI_{perfect}$, ossia i cicli con cui la CPU esegue le istruzioni senza avere miss, e il $CPI{stall}$, ossia i cicli di clock che la CPU spende aspettando la memoria. Il CPI sarà quindi la somma dei due:

$CPI=CPI_{perfect}+CPI_{stall}$

Si può trovare il valore del CPI anche moltiplicando il miss rate delle istruzioni di memoria per la miss penalty:

$CPI_{stall}=\frac{accessi\ in\ memoria}{istruzioni\ per\ programma}_miss\ rate_miss\ penalty$

il $CPI_{stall}=CPI_{stall \ istruzioni}+CPI_{stall\ dati}$

Il problema della cache è che porta dell'aumento di complessità e perciò può accadere che i tempi di accesso al posto che migliorare peggiorino, e quindi in alcuni casi è meglio non metterla all'interno del sistema.

L'obiettivo nella progettazione di un caching system è quello di minimizzare l'AMAT, quindi ridurre il miss rate, il miss penalty e l'hit time. Bisogna inoltre tenere conto di quanto deve essere grande un blocco di cache , quanti blocchi devono essere presenti per ogni livello, come conoscere se un dato è presente o no in cache e come riutilizzare i blocchi.

Una cache di capacità C è organizzata in S set ognuno dei quali contiene B blocchi ( o linee) e ogni blocco contiene b parole.

Per mappare i dati dall'indirizzo di memoria in cache si usa la funzione di mapping.

## Trovare un dato in cache

Le cache vengono suddivise in 3 in base al numero di blocchi per ogni set :

- Direct mapped : #S=#B
- N-way set-associative : ogni set contiene N blocchi. S=B/N
- Fully associative cache : S=1

> [!NOTE]  Da ricordare che:
>Vengono considerati sistemi con indirizzi da 32 bit, parole da 32 bit e la memoria contiene  $2^{30}$ parole 


## Confronti e considerazioni


Il vantaggio di una dimensione di blocco maggiore di uno è che in caso di miss vengono copiate in cache la parola non trovata ed anche le parole adiacenti nel blocco di memoria principale.

Gli accessi successivi hanno dunque una maggiore probabilità di dare luogo ad hit grazie alla località spaziale.

Tuttavia una dimensione di blocco grande significa che a parità di capacità della cache che questa ha meno blocchi e quindi può dare luogo a un maggior numero di conflitti e quindi di miss, inoltre serve più tempo per prelevare dalla memoria principale tutte le parole da trasferire in cache e il tempo necessario per caricare in cache il blocco mancante è proprio il miss penalty.

Incrementare l'associatività di N riduce generalmente il tasso di miss causato dai conflitti ma questo implica l'uso di comparatori di tag e quindi più lentezza e maggior costo.

Incrementare la dimensione di blocco b sfrutta la località spaziale ma diminuisce il numero di set e quindi può causare più conflitti.


| Organizzazione        | N. ways | N. sets       |
| --------------------- | ------- | ------------- |
| Direct mapping        | $1$     | $B$           |
| Partially associative | $1<n<B$ | $\frac{B}{N}$ |
| Fully associative     | $B$     | $1$           |


## Problemi
La cache è essenziale per ridurre il von Neuman bottleneck e raggiungere performance ragionevoli per i sistemi moderni, infatti ogni sistema moderno ne utilizza almeno due livelli.

Nonostante ciò la cache introduce problemi nei sistemi multi processori. In particolare se ne hanno due :

- Il problema della coerenza
- False sharing

Entrambi i problemi hanno a che fare con la concorrenza in quanto c'è parallelismo a livello hardware (più core che condividono una stessa cache) e anche a livello software con i threads ( in particolare per il false sharing).

Si prende in considerazione un'architettura dove ci sono almeno due core e cache dati private e cache condivise. Quello che succede è che nella cache privata posso memorizzare sia dati privati che pezzi di codice condivisi.

Finchè l'accesso è in lettura non ci sono problemi, ma quando il dato è condiviso ed entrambi i core cercano di scriverlo, e questo dato si trova in entrambe la cache private, il thread che parte dopo vedrà un dato più vecchio.

SI VUOLE CHE NEL CASO SI AGGIORNI UN DATO PUBBLICO SCRITTO NELLE CACHE PRIVATE, IL CORE CHE NON HA ACCESSO A QUELLA CACHE MA HA IL DATO SCRITTO ANCHE NELLA SUA CACHE PRIVATA LO VEDA AGGIORNATO E NON VEDA IL DATO VECCHIO

Si suppone di partire con un dato in memoria al tempo 0 : x = 1. Al tempo 1 il primo processo che si trova in esecuzione sul core A legge x e lo carica sia nella cache L1 sia L2(quella condivisa). Cora A chiede a L1, si aha miss. L1 chiede a L2 e si ha miss, L2 chide alla memoria, si legge l'intero blocco contenente x , poi viene caricata in L2 condivisa e poi viene messa in L1 Al tempo 2 il secondo core chiede di nuovi x e si trova in L2 e quindi fa prima Poi però in un terzo momento A scrive 0 in x iin L1 che poi viene aggiornato anche in L2 e in memoria. Il problema è che in L1 del core B la variabile x è rimasta con 1 e non con 0 e quindi le cache non sono tutte coerenti

Un protocollo usato per risolvere questo problema è il "write invalidate protocol" che quando vede che il contenuto è condiviso va ad invalidare i dati nelle altre cache e al prossimo accesso si ha un miss.


## Ottimizzazioni software

L'obiettivo sarebbe quello di scrivere codice che sfrutti le potenzialità della cache usando il più possibile la località spaziale e temporale. Due delle tecniche più conosciute sono quelle del loop interchange e del data blocking : il primo è una tecnica per aumentare la località spaziale ed entra in gioco in linguaggi come C in cui gli array di matrici sono allocati row-major ordering e quindi semplicemente invertendo l'ordine di alcuni for è possibile sfruttare al meglio questa caratteristica. Il secondo è un modo per aumentare la località temporale suddividendo in blocchi più piccoli compiti che sarebbero stati effettuati in blocchi più grandi.
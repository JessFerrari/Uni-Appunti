L’apprendimento è una delle maggiori sfide per fornire INTELLIGENZA.

Il machine learning, ossia l’apprendimento automatico, serve per creare IA con strumenti statistici.

viene utilizzato per sistemi intelligenti adattivi, sistemi statistici intelligenti (Data Analysis) e metodi di computer science innovativi (in particolare per problemi complessi).

Il ML viene utilizzato per sistemi di classificazione in cui avere solo una KB non basta e servono anche dati di training.

NON si usa il ML dove la teoria è poca ed è difficile formalizzare la conoscenza, in ambienti incerti e rumorosi e in ambienti dinamici.

Per eseguire ML vengono richiesti DATI su cui fare training e TOLLERANZA sui risultati [come si vedrà più avanti si parla di approssimazione e nella soluzione viene sempre considerato il rumore]

IL ML TROVA SOLUZIONI APPROSSIMATE (la soluzione è approssimata e non la metodologia) A PROBLEMI DIFFICILI DA FORMALIZZARE IN MANIERA COMPLETA E COSTRUISCE UN MODELLO ROBUSTO CON AMPIO RAGGIO DI APPLICAZIONE.

> Dati dei DATI si fa una PREEDZIONE del risultato del problema grazie ad un MODELLO attraverso:

- TASK
- ALGORITMO DI LEARNING
- VALIDAZIONE

Il MODELLO si costruisce in base al problema che deve essere formalizzato. POSSONO ESSERE PRESENTI AMBIGUTÀ E RUMORE.

> L’apprendimento è l’approssimazione di una funzione nota da esempi. Può essere supervisionato o non supervisionato.

## Supervised Learning

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8674f074-456d-4e20-b6af-eedaafcdc71a/Untitled.png)

> Dato un insieme di esempi di training $<input,output>=<x,d>=<x,c(x)>$ si vuole trovare una BUONA APPROSSIMAZIONE DELLA FUNZIONE c. [della funzione $f$ se si guarda la figura]. Tale approssimazione è una funzione $h\in H$ (dove $H$ è lo spazio delle ipotesi) che viene usata per predire il valore di $c(x')$ su dati sconosciuti $x'$

Il target $d$ è un’etichetta che può assumere valori o CATEGORICI, e in questo caso si parla di CLASSSIFICAZIONE, o NUMERICI ($d\in\R \ o\ \R^k$ ), e in questo caso si parla di REGRESSIONE.

Sia la CLASSIFICAZIONE che la REGRESSIONE sono approssimazione di funzione.

## Unsupervised learning

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe5ce595-9522-4660-bc39-54452a2c8d5f/Untitled.png)

Il training set p dato da dati non etichettati $<x>$ e il task consiste nel trovare una naturale divisione dei dati.

Si raggruppano i dati simili e si trova la norma di tali gruppi per classificarli.

## MODELLO

Il MODELLO descrive le relazioni tra i dati basandosi sul problema.

Definisce le classi di funzioni che il sistema di apprendimento può implementare, ossia lo spazio delle ipotesi $H$ in cui sono presenti le IPOTESI, funzioni, $h(x,w)$ [quelle tra cui si sceglie quella che approssima la funzione target].

Un TRAINING EXAMPLE in un task supervisionato ha la forma <x, d> = <x, c(x)+noise> dove c(x)+noise è detto TARGET VALUE.

I modelli possono essere di tipo diverso:

- Lineare : $h_w(x)=w_1x+w_o$ [vedi pagina 3]
- Simbolic rule (con rappresentazione discreta) : $\\if(x_1=0||x_2=1) \rightarrow h(x)=1 \\ else \rightarrow h(x)=0$
- Probabilistico
- Memory based

## ALGORITMO DI APPRENDIMENTO

> Basandosi sui Dati, sul Task e sul Modello

l’apprendimento è una RICERCA EURISTICA dell’ipotesi $h$ che approssima al meglio la funzione target all’interno dello spazio delle ipotesi $H$, ossia quella con MINIMO ERRORE.

Non viene fatta una ricerca esaustiva ma si cerca il miglior fitting dei parametri liberi, ovvero il loro miglior adattamento al problema

Lo spazio delle ipotesi $H$ può non coincidere con il l’intero insieme delle funzioni e la ricerca potrebbe non essere esaustiva. Ciò perché è necessario fare assunzioni secondo un BIAS INDUTTIVO [vedi dopo]

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e600ac90-ab5b-4362-9007-833db1f0b0cd/Untitled.png)

## Generalizzazione

Quando si apprende si deve scegliere una funzione che approssimi bene la funzione target c(x)+noise. Tale approssimazione deve GENERALIZZARE L’ERRORE, ossia deve dare buoni risultati anche per dati che non appartengono all’insieme di training, e quindi sconosciuti.

Si deve evitare di fare OVERFITTING sui dati di training.
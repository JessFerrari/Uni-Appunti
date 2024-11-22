Un aspetto fondamentale del ML è valutare la sua capacità di generalizzazione dell’ipotesi ed un ruolo importante in ciò lo ha la VALIDAZIONE.

Qui si capirà quando un modello di ML è un buon modello e come usarlo bene.

Non è necessariamente bene che se un ipotesi si comporta bene sul training allora si adatta bene al modello. come si è già visto può avvenire overfitting.

Sui dati di test si valuta la CAPACITÀ DI GENERALIZZAZIONE e le performance di un sistema di ML si misurano in base alla accuratezza di predizione.

- CLASSIFICAZIONE : MSE per la loss, il mean error rate per l’outcome
- REGRESSIONE : MSE, root MSE, Mean Absolute Error, Max Absolute Error

Se c’è un errore alto allora l’accuratezza è bassa.

### 2 fasi di validazione :

- Model selection : si stimano le prestazioni, ossia l’errore di generalizzazione, di vari modelli per scegliere il migliore
- Model assessment : una volta scelto il modello finali si vuole valutare l’errore di predizione su nuovi dati di test

È buona norma tenere separati gli obbiettivi con data set diversi.

Il modo più semplice per farlo è tenere i dati in tre insiemi disgiunti [**HOLD OUT**] :

- dati di training, su cui si fanno le modifiche dei parametri
- dati di validazione
- dati di test

Assieme, l’insieme di training e quello di validazione, prendono il nome di insieme di sviluppo o di design, in quanto si calibra il modello quanto si vuole.

Il training serve per fare fit sui dati, il validation per scegliere il modello migliore (model selection), mentre il test per fare la fase finale di model assessment.

Se si usa la stima fatta sul validation set per la stima del rischio finale si fanno errori in quanto non è una buona stima del comportamento del test.

Non si possono nemmeno usare i risultati del set per la model selection. Se dopo fare i test si da un’aggiustatina si sta facendo model selection con i dati sbagliati.

❓ Che succede se il test viene usato in un ciclo ripetuto di design ? → si sta facendo model selection e non si è arrivati davvero alla fine, si sono bruciati i dati di test.![[MLsystem.png]]


Qui sotto un meta algoritmo sul funzionamento:

![[FunzionamentoMLsystem.png]]

Un iperparametro è un parametro che non è dinamicamente appreso ma è scelto dallo sviluppatore. Ad esempio il grado del polinomio o il $\lambda$ della regressione.

L’iperparametro con il miglior risultato sarà quello utilizzato nel modello
Si scegli il miglior modello osservando la validation, scegliendo gli iper parametri attraverso la grid search![[Iper parametro.png]]


In questo caso si sceglie il secondo modello in quanto ha il valore di validation maggiore.

A prima vista verrebbe da dire di prendere il terzo ma il modello non va scelto in base ai dati di training, per il rischio dei overfitting, ma nemmeno sui dati di test.

Ad esempio estremo:

Si hanno 20-30 esempi (pochi) con 100 variabili di input randomiche in cui anche il target è randomico, ossia non si ha nessuna possibilità di fare un modello che lo possa predire.

Per questo problema si può scegliere un modello che può indovinare per caso e può dare l’illusione di poter risolvere il task al 100% in tutte le 3 fasi.

Si possono scegliere solo delle istanze che coincidono con il target (le migliori guardando tutto il dataset), magari una che coincide. Così questa avrà accuratezza al 100% con il target ma non appena si aggiunge un’istanza il risultato è a caso.

Se uso il test set per scegliere il modello migliore mi illudo perché se per un’istanza i risultati sono buoni, o addirittura ottimi, ma per altri no.

> Errore stimato su training o validation per model selection NON è utile per stima del rischio. I dati di TR o VL non vanno usati per scopi di test.

Inoltre, usare tutto il data set per feature/model selection lede la correttezza della stima [Feature Selection bias]


## K-fold

L’HOLD OUT può usare in modo non efficiente i dati e per questo si usano altre tecniche come la K-fold.

I dati vengono ripartiti i 4 gruppi, $D_1, D_2, D_3, D_4$.

Facendo conto che questi dati servono per fare training e validation, si parte facendo il training su $D_1,D_2,D_3$ e validation su $D_4$ e ci si segna il risultato.

Nell’iterazione dopo si fa training su $D_1,D_2,D_4$ e validation su $D_3$ e si segna il risultato.

Poi si usa $D_2$ come validation e gli altri di training e poi $D_1$.

Alla fine di ciò si sceglie il modello basandosi sul risultato migliore. Si fa validation su tutti i dati.

![[k-fold.png]]


# Behavior of learning

Quello che succede in qualsiasi sistema di learning è che l’errore diminuisce man mano che la complessità aumenta.

Infatti se la complessità è molto bassa si ha underfitting.

Anche avere una complessità troppo alta può creare problemi in quanto si ha overfitting sul training set, e quindi tale errore sarà molto basso, ma sui dati di test questo sarà comunque alto.

Anche il numero di dati influisce sull’accuratezza. Se uso un polinomio di grado 9, quindi alta complessità con la quale si potrebbe finire in overfitting, e un numero alto di dati l’approssimazione sarà molto buona.
![[Pasted image 20241122103039.png]]
La SLT studia la capacità di generalizzazione di un modello rispetto al training error e le zone di over e under fitting, mettendo in evidenza il ruolo della complessità del modello e quello del numero di dati usati.

- si vuole approssimare un funzione non nota $f(x)$ con una funzione $d=f+noise$ detta target .
- Si vuole minimizzare la risk function $R=\int{L(d,h(x))dP(x,d)}$
- Dati un target d, una probabilità di distribuzione $P(x,d)$ e una loss definita come $L(h(x),d)=(d-h(x))^2$
- Trovare $h\in H$ che minimizza R avendo solo un data set finito

$$ R_{emp}=\frac 1 l\sum_{p=1}^l(d_p-h(x_p))^2 $$

$R_{emp}$ = rischio empirico $R$=rischio teorico

Si vuole minimizzare R con il rischio empirico

## Vapnik-Chervonenkis-dim

Data la VC-dim, ossia una misura di complessità dello spazio delle ipotesi riguardante la flessibilità dei dati per il fitting, si ha che il rischio reale è minore uguale del rischio empirico + una la VC-confidence la quale dipende da:

- $\frac 1 l$
- $VC$
- $\frac 1 \delta$

$$ R\leq R_{emp}+\epsilon(\frac 1 l, VC, \frac 1 \delta) $$

- $\epsilon$ è una funzione che cresce con la VC-dim, ed esce con valori alti di $l$ e $\delta$
- il rischio empirico decresce usando modelli complessi, quindi con un’alta VC-dim
- $\delta$ è la confidence, è un limite superiore dell

Se ci sono molti dati allora la confidence diminuisce e il rischio reale si avvicina a quello empirico.

Fissato il numero di dati :

Se il modello è troppo semplice, ossia si ha una VC-dim bassa, si ha underfitting.

Se il modello è molto complesso, ossia si ha VC-alta, si ha overfitting.![[VC-dimension.png]]

La STATISTICAL LEARNING THEORY (SLT) permette un inquadramento formale del problema della generalizzazione e dell’ overfitting fornendo limitazioni superiori analitiche e quantitative al rischio R di predizione su tutti i dati, indipendentemente dal tipo di algoritmo o dai dettagli del modello.

Il ML è ben fondato
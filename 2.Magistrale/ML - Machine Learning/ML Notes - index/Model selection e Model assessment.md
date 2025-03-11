---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
Creation: 2025-01-09
---
# Motivazioni della validation 
Usare solo il training set porta ad un eccessivo bias ed una varianza molto alta, e quindi non può essere considerato un buon stimatore dell'errore di test.
Bisogna quindi riconoscere quali sono gli iperparametri che fanno variare la complessità del modello e che influenzano l'errore di test, e cercare un metodo per stimare l'errore atteso del modello.

 Questa stima si può fare in due modi:
 - Analiticamente: 
	 - AIC/BIC (Akaike/Bayesian Information Criterion), che si limita solo ai modelli lineari
	 - MDL (Minimum Description Length)
	 - SRM (Structural Risk Minimization e *[[VC-Dimension]]*)
- Con il ***Resampling***:
	- k-fold cross validation
	- Bootstrap : è una tecnica di resampling z per stimare le proprietà di un modello quando i dati a disposizione sono pochi.

# Model selection e model assessment
- **Model selection** (on Validation set): estimating the performance (generalization error) of different learning models in order to choose the best one; that include hyper-parameters of the model. -> ==returns a model==

- **Model assessment** (on Test set): having chosen a final model estimating/evaluating its prediction error/risk (generalization error) on new test data; measures the performance of the ultimately chosen model -> ==returns an estimation==

# Grid search e random search
Per ricercare i migliori iperparametri si utilizzano due tecniche: la grid search e la random search.

La grid search è una ricerca esaustiva su tutte le possibili combinazioni dei valori che i vari iperparametri di un modello possono assumere.
I trial sono indipendenti uno dall'altro e si può parallelizzare. 
Il numero di trials aumenta con il numero di iperparametri e dei valori che questi possono assumere.
Si può effettuare una ***nested grid search***, ossia utilizzare più livelli di grid search. All'inizio si ricerca su intervalli più ampi per poi diminuirli.

La random search riduce i costi computazionali della grid search perché non fa la ricerca esaustiva come la precedente e permette di esplorare anche i valori intermedi tenendo fissi quelli meno influenti.

![[grid search.png]]
A sinistra rappresentazione della grid search e a destra della random search.
# Hold out
For the basic setting, we can simply divide the dataset $D$ in three sets: Training $TR$, Validation $VL$ and test $TS$, and use $TR$ for training, $VL$ for model selection and $TS$ for model assessment.

We can call te union of $TR$ and $VL$ *Development/design set*.
![[hold out sets.png]]
![[Hold out.png]]
Se venisse utilizzato il test set per modificare il modello da scegliere questo potrebbe non generalizzare su nuovi dati e con le stesse performance ottenute sul test.


Se i dati fossero insufficienti per essere organizzati in 3 macro insiemi può aiutare la ***k-fold cross validation***

# K-fold cross validation 
La k-fold cross validation è un metodo per utilizzare li'intero dataset, o almeno l'itero design set per training e validation.

Viene diviso il dataset D in k sottoinsieme mutualmente esclusivi. Ad ogni iterazione si tiene l'i-esimo sottoinsieme per la validation e gli altri ${D}/{D_{i}}$ per il training.
![[kfold.png]]

Con la k-fold cross validation non si ottiene un modello unico ma tanti quanti sono i fold e si ottiene una varianza sui diversi fold.
Dopo che si è scelto il modello questo viene allenato su tutto il design set

- Computazionalmente molto costosa

Per rendere il campionamento dei dati rappresentativo si usa la stratificazione, evitando di avere partizioni fortunate o sfortunate.
Si va a controllare che i membri del sottogruppo siano nelle solite proporzioni del dataset originario.

# Model assessment
Per fare model assessment serve un test set mai usato.
Questo si può ottenere con hold out, quindi dal dataset separare una percentuale per il test ed usare il resto per il training, oppure con la k-fold

Con la k-fold si usa l'i-esimo fold per il test e si ottengono diverse stime.
Per averne una unica poi si fa la media sulle s time ottenute.

## Merging model selection e model assessment
Per avere sia un modello che una stima bisogna combinare i metodi precedenti.
Si possono quindi ottenere diversi modi:
- Hold-out generale per test, validation e test set
- cross validation per test e training + set separato per il test
- model selection con holdout ed esterna cv per il test
- *DOUBLE CROSS VALIDATION*

## Double cross validation (Nested k-fold cross validation)
Viene fatto un ciclo di k-fold esterno dove si ottiene una parte per il test, che non si tocca ed una per il design.
Si hanno quindi k design set e su ognuno di questo viene effettuata un ulteriore k-fold per il training set e per il validation set.

Questo metodo fornisce numerosi modelli e numerose stime, utilizza i dati in modo efficiente ma è molto costoso dal punto di vista computazionale.

![[nested k-fold.png]]
# Bootstraping
Tecnica di resampling z per stimare le proprietà di un modello quando i dati a disposizione sono pochi

### Funzionamento
Dato un dataset con $N$ esempi vengono creato un resample con $N$
esempi presi casualmente dal dataset originario.
Ciò vuol dire che ogni esempio può essere ripetuto o mai selezionato.
Il processo di resampling viene ripetuto molte volte per generare diverse versioni del dataset.

Per ogni resample si può allenare su di esso un modello e valutarne le performance con i dati che non sono stati utilizzati


I __[[Machine Learning Model|modelli]] instance-based__ di [[Machine Learning |machine learning]] sono modelli non parametrici generati da un [[Machine Learning Algorithms|algoritmi di learning]] che memorizzano tutte le istanze dei dati e calcolano le predizioni basandosi sulla __somiglianza__ tra l'istanza da predire e quelle presenti nel dataset.

I modelli __instance-base__ non sono un __ipotesi esplicita e analitica__ e si basano direttamente sul confronto dei dati da predire con le istanze dei dati già visti in training.

Gli [[Machine Learning Algorithms|algoritmi di learning ]] che generano dei __modelli instance-based__ sono detti "__lazy__" perché non viene costruita nessuna ipotesi durate il training e vine rimandato tutto rimandato alla fare si inferenza

Vantaggi:  
- __Flessibilità__: Grazie all'uso diretto dei dati, questi modelli sono particolarmente efficaci nel trattare relazioni complesse e non lineari.  
- __Adattabilità__: Aggiungere nuovi dati al sistema è semplice e non richiede la ricostruzione di un modello.  

Svantaggi:  
- __Requisiti di memoria elevati__: La necessità di conservare tutto il dataset può diventare proibitiva per dataset molto grandi.  
- __Scalabilità limitata__: Fare predizioni può risultare lento, poiché richiede il confronto con tutte le istanze memorizzate.  

Tra gli esempi più comuni di modelli instance-based troviamo:  
- __[[K-nn|k-Nearest Neighbors]]__  
- __Kernel regression__  




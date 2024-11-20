---
Subject: "[[Indice - Basi di dati]]"
tags:
  - BD
Creation: 2024-02-24
Slide: "[[ALL_BD.pdf|da slide 384 a 539]]"
---
# Teoria relazionale: introduzione

Ci sono due metodi per produrre uno [[Modello relazionale|schema relazionale]], partire da un buon schema ad oggetti e tradurlo o partire da uno schema relazionale fatto da altri e modificarlo.
Inoltre per ogni relazione ci sono diverse rappresentazioni valide e quindi uno dei problemi e la _scelta_ di questa rappresentazione.
Ci sono vari parametri su cui basare la scelta tra cui il _costo delle operazioni_ e la presenza o Assenza di _anomalie_


> [!NOTE] Normalizzazione
La teoria della progettazione relazionale studia cosa sono le “anomalie” e come eliminarle (**normalizzazione**), particolarmente utile se si parte da schemi relazionali fatti da altri.

La normalizzazione serve per risolvere anomalie come :
- Ridondanze
- Potenziali inconsistenze
- Anomalie nelle inserzioni
- Anomalie nelle eliminazioni

### Obiettivi della teoria della progettazione relazionale

- **Equivalenza** di schemi: in che misura si può dire che uno schema rappresenta l’altro
- **Qualità** degli schemi ([[Forme normali|forme normali]]), in base a dei criteri di bontà, per definire formalmente cosa significa che uno schema è migliore di un altro in base all'assenza di anomalie
- **Trasformazione** degli schemi (normalizzazione di schemi) attraverso algoritmi


Dalla _teoria di normalizzazione_ deriva il processo di __*normalizzazione degli schemi relazionali*__ che trasforma una _rappresentazione esistente_ in una rappresentazione in _forma normale_.

Una [[Forme normali|forma normale]] di una schema relazionale è una forma _equivalente_ al originaria che assicura le buone qualità di un [[Base di dati|Database]], ovvero è migliore secondo la _teoria della normalizzazione_

Il  _processo di normalizzazione_ tiene conto solo dell'eliminazione delle _anomalie_ e NON tiene conto del _costo del operazioni_.


##### Assunto della normalizzazione 
La _Teoria della Normalizzazione_ assume l'esistenza di uno  _schema di relazione Universale del DB_, che assicura che _attributi_ con lo _stesso nome_ anche in _relazioni_ diverse abbiano lo stesso significato, ovvero condividono il dominio e il _fatto_ che stanno rappresentando .
Questo permette di evitare di fare _ridenominazioni_ durante le operazioni di normalizzazione e permette di usare sempre il [[Modello relazionale - Algebra Relazionale|Join Naturale]]   

###### Schema di relazione universale (Definizione)
 uno _Schema di relazione universale_ $U$ di un _database Relazionale_ ha come attributi l'unione degli attributi di tutte le relazioni del _database_
 
##### Anomalie
Le anomalie per un database sono definite come

1. _Ridondanza Logica_: Ripetere più volte la stessa informazione e problematico sia per spreco di  memoria e per l aggiornamento delle informazioni 
	1. Anomalia di aggiornamento: per via della ridondanza aggiornare un valore significa doverlo aggiornare ovunque e questo può portare facilmente ad inconsistenze
	2. Anomalie di cancellazione:  situazioni deve fare certe cancellazioni "corrette" portano al eliminazioni involontaria di certi dati
	3. Anomalia di Inserimento: per fare un inserimento corretto bisogna  fare degli inserimento in più inutili (correlati al dato che vogliamo inserire) o si deve aspettare che abbiano senso
2. Ridondanza concettuale: non ci sono duplicazioni dello stesso dato, ma sono memorizzate informazioni che possono essere ricavate da altre già contenute nel DB.
3. _Impossibilità di rappresentare certi fatti_: questo succede quando la rappresentazione di certi _fatti_ dipende dalla rappresentazione di altri fatti

ESEMPIO:![[Pasted image 20240224052309.png]]
- ___Ridondanza___: Lo stipendio di ciascun impiegato è ripetuto in tutte le ennuple relative. Questo succede perché lo stipendio dipende solamente dall’Impiegato. Stessa cosa succede per il bilancio, esso dipende solo dal progetto ed è ripetuto.
- ___Anomalia di aggiornamento___: Se lo stipendio di un impiegato varia, è necessario andarne a modificare il valore in diverse ennuple
- ___Anomalia di cancellazione___: Se un impiegato interrompe la partecipazione a tutti i progetti, dobbiamo cancellare tutte le ennuple in cui appare, e in questo modo l’impiegato non sarà più presente nel database.
- ___Anomalia di inserimento___: Un nuovo impiegato non può essere inserito fino a che non gli viene assegnato un progetto



Per evitare questi problemi si decompongono le relazioni in più relazioni diverse collegate tra loro tramite uno degli attributi.

La [[Decomposizione dei schemi|decomposizione]] è un processo delicato e va fatto con cura infatti si possono incappare nei problemi di PERDITA DI INFORMAZIONI e PERDITA DI DIPENDENZA FUNZIONALE

- _Perdita di informazioni_: questo avviene quando il [[Modello relazionale - Algebra Relazionale|Join]] tre le due relazioni prodotto della decomposizione produce più ennuple della relazione originale, ovvero avviene quando viene scelta come chiave esterna per una delle due relazione un attributo che non rappresenta univocamente quel _[[Aspetto ontologico|entità]]_, ovvero che non è una [[Modello relazionale - chiave|chiave valida]] per quel entità 

- _Perdita di dipendenze funzionali_: questo avviene quando una [[Dipendenze funzionali|dipendenza funzionale]] presente nella relazione originale non è più deducibile dalle due _relazioni_ di decomposizione. 

## Linee guida per la progettazione
1. __Semantica degli attributi__ 
Si La progettazione deve essere fatta in modo che sia semplice spiegarne il significato. Non si uniscano attributi provenienti da più tipi di classi e tipi di associazione in una unica relazione. 

2. __Ridondanza__ 
Si deve progettare in modo che nelle relazioni non siano presenti anomalie di inserimento, cancellazione o modifica. 
Se sono presenti delle anomalie (che si vogliono mantenere), le si deve rilevare chiaramente e assicurarsi che i programmi che aggiornano la base di dati operino correttamente

3. __Valori Nulli__ 
Per quanto possibile, si deve evitare di porre in relazione di base attributi i cui valori possono essere (frequentemente) nulli. 
Se è inevitabile, ci si assicuri che essi si presentino solo in casi eccezionali e che non riguardino una maggioranza di tuple nella relazione 

4. __Tuple spurie__ 
Si devono progettare schemi di relazione in modo tale che essi possano essere riuniti tramite [[Modello relazionale - Algebra Relazionale#Giunzione|JOIN]] con condizioni di uguaglianza su attributi che sono o chiavi primarie o chiavi esterne in modo da garantire che non vengano generate tuple spurie. 
Non si devono avere relazioni che contengono attributi di «accoppiamento» diversi dalle combinazioni chiave esterna-chiave primaria.

### Forme normali
Le _forme normali_ sono un criterio di valutazione su ciò controllare i _schemi relazionali_ esistenti in modo da trasformarli in schemi che rispettano i criteri

#### Prima e seconda forma normale
le prime de _forme normali_ sono elencante per motivi storici siccome sono vere implicitamente con i sistemi moderni usati
1. _prima forma normale_: ogni valori dei domini di una relazione sono _atomici_
2. _seconda forma normale_: tutti gli attributi dipendono dalla [[Modello relazionale - chiave|chiave primaria completa]]
3. [[Forme Normali - Terza forma|Terza forma normale]]
4. [[Forme Normali - Boyce-Codd|Forma normale Boyce-Codd]]
5. [[Forme normali - Quarta forma normale|Quarta forma normale]]

ognuna di questa _implica la precedente_


#### Scelta tra BCNF e 3NF
la scelta tra la _3NF_ e la _BCNF_ nel processo di normalizzazione richiede al progettista di decidere in anticipo.
La strategia di controllare prima la possibilità di una decomposizione in BCNF che preservi le dipendenze, e in caso negativo adottare la 3NF, non è praticabile dato che richiede un algoritmo con _[[Complessità|complessità]] esponenziale_.

siccome abbiamo che 
[[Forme Normali - Boyce-Codd|BCNF]]: algoritmo di analisi esponenziale (con polinomiale che non si usa)
- BCNF ci garantisce che si preservano i dati
- controllare che ci siano anche le dipendenze è polinomiale
3NF: algoritmo di sintesi che preserva dati e dipendenze

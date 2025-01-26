---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello relazionale]]"
tags:
  - BD
Creation: 2024-02-19
Esercizi: "[[Esercizi algebra relazionale]]"
Esempi: "[[Esempi raggruppamento]]"
---
 Nel modello relazionale si distinguono due tipi si distinguono 2 linguaggi relazionali:
- l'_algebra relazionale_: composta da operatori su relazioni che danno come risultato altre relazioni. Non si usa come linguaggio di interrogazione dei DBMS ma come rappresentazione interna delle interrogazioni. Sono operatori simili a quelli del [[SQL]].
- il _calcolo relazionale_: linguaggio dichiarativo di tipo logico dal quale è stato derivato l'[[SQL]]


Gli operatori dell'algebra relazionale sono operatori [[Insiemi|insiemistici]] in quanto le relazioni sono insiemi. 
Questi operatori sono:
- unione, intersezione, differenza
- ridenominazione
- selezione
- proiezione 
- join
	1. join naturale
	2. prodotto cartesiano
	3. theta-join
	4. self join

I risultati di questi operatori devono essere relazioni

## Unione, intersezione, differenza
L'unione, intersezione e differenza si possono applicare solo a relazioni definite sugli stessi attributi (nome e tipo), ossia possono operare solo su tuple uniformi.


> [!NOTE]- Unione
> Questa prima tabella :
>
| Matricola | Nome | Età |
| ---- | ---- | ---- |
| 724 | Rossi | 23 |
| 725 | Verdi | 27 |
>  
>  Unita a questa :
>  
| Matricola | Nome | Età |
| ---- | ---- | ---- |
| 726 | Rossi | 32 |
| 727 | Verdi | 75 |
>  Danno come risultato:
>  
| Matricola | Nome | Età |
| ---- | ---- | ---- |
| 724 | Rossi | 23 |
| 725 | Verdi | 27 |
| 726 | Rossi | 32 |
| 727 | Verdi | 75 |
>  
>  Se:
>  $\#S$ = cardinalità prima tabella e $\#R$ = cardinalità seconda tabella
>  Allora si ha che la cardinalità risultante sarà $Q=S+R$ 
 
> [!NOTE]- Differenza
> Questa prima tabella :
>
| Matricola | Nome | Età |
| ---- | ---- | ---- |
| 724 | Rossi | 23 |
| 725 | Verdi | 27 |
| 726 | Neri | 28 |
>  
>  Meno a questa :
>  
| Matricola | Nome | Età |
| ---- | ---- | ---- |
| 726 | Neri | 28 |
| 727 | Verdi | 75 |
| 729 | Neri | 32
>  Danno come risultato:
>  
| Matricola | Nome | Età |
| ---- | ---- | ---- |
| 724 | Rossi | 23 |
| 725 | Verdi | 27 |
>  Se:
>  $\#S$ = cardinalità prima tabella e $\#R$ = cardinalità seconda tabella
>  Allora si ha che la cardinalità massima risultante sarà $Q=S$ e quella minima $Q = \emptyset$

## Ridenominazione

La ridenominazione è un operatore monadico, ossia che agisce soltanto su un operatore. si indica con la lettera $\rho$.
Si usa per riminare un'attributo di una tabella quando si potrebbe fare l'unione o la differenza con un'altra ma si è impossibilitati a causa del nome.
![[Pasted image 20240219151413.png]]
Su quest'esempio, dopo aver fatto la ridenominazione, si possono usare gli operatori di unione e differenza.


## Proiezione

La proiezione è un'operatore monadico che produce come un risultato che ha parte degli attributi dell'operando e contiene ennuple cui contribuiscono tutte le ennuple dell'operando ristrette agli attributi nella lista.

Proiezione : $\pi _{ListaAttributi}(Operando)$

In pratica prende solo gli attributi specificati della relazione operando.
![[Pasted image 20240220010128.png]]

Se nella lista, presa la lista degli attributi, ci sono dei duplicati non si considerano

La cardinalità della relazione finale è al più tante ennuple quante l'operando, ma può contenerne meno se ci sono dei duplicati.

- Se $X$ è una superchiave di $R$ allora $\pi_X(R)$ contiene esattamente tante ennuple quante $R$
- Se $X$ non è superchiave per $R$ allora $\pi_X(R)$ potrebbe avere meno ennuple in quanto possono esistere valori ripetuti per $X$

## Selezione (o restrizione)

La selezione è un'operatore monadico che produce come risultato una relazione che:
- ha lo stesso schema dell'operando 
- contiene un sottoinsieme delle ennuple dell'operando, quelle che soddisfano una _condizione_ espressa combinando, con i connettivi logici (and $\land$ , or $\lor$ , not $\lnot$  ), condizioni atomiche del tipo $A\ \theta \ B$ o $A \ \theta \ c$, dove $\theta$ è un operatore di confronto, A e B sono attributi su cui l'operatore $\theta$ abbia senso e c una costante compatibile con il dominio di A.
Si denota con $\sigma$ con la condizione messa a pedice.

![[Pasted image 20240220011759.png]]

Se ci sono valori Null vengono scartati in quanto è vera solo per i valoro non nulli.
Per ottenere anche i valori null esistono forme apposite di condizioni come $isNull$ e $isNotNull$ 

![[Pasted image 20240220012137.png]]

Combinando selezione e proiezione, possiamo estrarre interessanti informazioni da una relazione.
![[Pasted image 20240220012223.png]]


## Prodotto 

Il prodotto è come il prodotto cartesiano
	![[Pasted image 20240220012428.png]]
 
## Intersezione

Si può derivare l’operatore di intersezione usando gli operatori prodotto, ridenominazione, selezione e proiezione.

$R \cap S = \{ x|x\in R \; \exists y \in S, x=y \}$

Come fare? Supponiamo di avere $R(A,B)$ e $S(A,B)$

- $\rho_S$ _ridenominiamo_ gli attributi di $S$ anteponendo il prefisso $S$
- $\sigma_{A=S.A \;AND \; B=S.B}(R \times \rho_SS)$ _selezioniamo_ a questo punto le ennuple per cui $A=S.A$ e $B=S.B$
- $\pi_{A,B}(\sigma_{A=S.A \;AND \; B=S.B}(R \times \rho_SS) )$ _proiettiamo_ a questo punto le colonne $A$ e $B$

	![[Pasted image 20240220012744.png]]
	In questo caso si rinomina una tabella, si fa il prodotto tra le due relazioni, si proiettano le ennuple (righe) dove le matricole sono uguali, ed infine si selezionano solo gli attributi (colonne) che ci interessano.

Dato che dopo un prodotto cartesiano è sempre seguito nella maggior parte dei casi da selezione o restrizione si scrivono le operazioni mediante albero per non fare confusione con le parentesi
![[Pasted image 20240220013651.png]]

## JOIN
L'operatore di join ci permette di correlare dati in relazioni diverse.
Combinando selezione e proiezione si possono estrarre informazioni da una relazione ma non si possono però correlare informazioni presenti in relazioni diverse.
Ne esistono di 4 tipi : join naturale, join esterno, theta join e self join

### Join naturale
![[Pasted image 20240220014656.png]]
Operatore binario (generalizzabile) che correla dati in relazioni diverse sulla base di valori uguali in ___attributi con lo stesso nome___.
Produce un risultato sull’unione degli attributi degli operandi con ennuple che sono ottenute combinando le ennuple degli operandi con valori uguali sugli attributi in comune.
Presi $R_1(X_1)$,$R_2(X_2)$. $R_1 \Join R_2$ è una relazione su $X_1 \cup X_2$:
$R_1 \Join R_2 = \{ t \; su \; X_1 \cup X_2 \;| \; esistono \; t_1 \in R_1 \; e \; t_2 \in R_2 \; con \; t[X_1]=t_1 \; e \; t[X_2]=t_2 \}$ 
	In questo esempio vengono presi i valori uguali di matricola e data, ma è sbagliato in quanto l'attributo Data si riferisce a cose diverse e quindi si potrebbe avere un risultato vuoto. ![[Pasted image 20240220015330.png]]
	
- Un join è completo se tutte le ennuple contribuiscono al risultato 
- Un join non è completo se in $R_2$ esiste almeno una ennupla che ha un valore per gli attributi scelti non presente in $R_1$
- Un join è vuoto se in $R_2$ nessuna ennupla ha valori uguali a quelli in $R_1$ per gli attributi scelti
- Un join è completo con n x m ennuple se i valori sono tutti in relazione

Alcune ennuple che non contribuiscono al risultato vengono tagliate fuori

___Cardinalità del join:___
- Prese le relazioni $R_1(A,B)$ e $R_2(B,C)$ il join di $R_1$ e $R_2$ contiene un numero di ennuple compreso fra zero e il prodotto di $|R_1|$ e $|R_2|$ : $0\leq |R_1 \Join R_2|\leq |R_1| \times|R_2|$

- Se il join fra $R_1$ ed $R_2$ è completo allora contiene un numero di ennuple almeno uguale al massimo fra $|R_1|$ e $|R_2|$ 

- Se il join coinvolge una chiave $B$ di $R_2$, allora il numero di ennuple è compreso tra 0 e $|R_1|$ : $0 \leq |R_1 \Join R_2| \leq |R_1|$ 

- Se il join coinvolge una chiave $B$ di $R_2$ e un vincolo di integrità referenziale tra attributi di $R_1$ ($B$ in $R_1$) e la chiave di $R_2$, allora il numero di ennuple è pari a $|R_1|$ : $|R_1 \Join R_2| = |R_1|$   

- Un join naturale su relazioni senza attributi in comune contiene sempre un numero di ennuple pari al prodotto delle cardinalità degli operandi (le ennuple sono tutte combinabili)
##### Join naturale e proiezioni
Queste due proprietà servono per la [[Normalizzazione di schemi|decomposizione dei tabelle]] per la conservazione di dati

Avendo le relazioni $R_1(X_1)$ e $R_2(X_2)$, se facendo prima il join tra $R_1$ ed $R_2$ e poi la proiezione solo con gli attributi di $R_1$ non è detto che il risultato coincida con la relazione di partenza
	$\pi_{X_1}(R_1 \Join R_2)\subseteq R_1$
	![[Pasted image 20240220024652.png]]

Avendo la relazione $R(X)$, in cui $X=X_1 \cup X_2$ , mettendo in join la proiezione su $R$ con gli attributi $X_1$ con la proiezione su $R$ con gli attributi $X_2$ non è detto che coincida con quella di partenza.
	$R\subseteq (\pi_{X_1}(R))\Join (\pi_{X_2}(R_2))$ 
	![[Pasted image 20240220024803.png]]
### Join esterno 
Nel join naturale alcune ennuple che non contribuiscono al risultato vengono tagliate fuori.
Il join esterno estende, con valori nulli, le ennuple che verrebbero tagliate fuori da un join naturale.
Esiste in tre versioni : 
- sinistro, che mantiene tutte le ennuple del primo operando, estendendole con valori nulli, se necessario
- destro, che mantiene tutte le ennuple del secondo operando, estendendole con valori nulli, se necessario
- completo, che mantiene tutte le ennuple del primo e del secondo operando, estendendole con valori nulli, se necessario
![[Pasted image 20240220021701.png]]
![[Pasted image 20240220021715.png]]![[Pasted image 20240220021740.png]]
### Theta join
Un join naturale su relazioni senza attributi in comune, contiene sempre un numero di ennuple pari al prodotto delle cardinalità degli operandi (le ennuple sono tutte combinabili)

Il prodotto cartesiano concatena tuple non necessariamente correlate dal punto di vista semantico. Il prodotto cartesiano è più utile nel caso sia fatto seguire da una selezione ($\sigma_{Condizione} (R_1 \Join R_2)$) come ad esempio una selezione che mantiene solo le tuple con valori uguali sull’attributo.

Questo tipo di operazione viene chiamata _theta-join_ e si indica sintatticamente con $R_1 \Join_{Condizione} R_2$.

Nel caso in cui la condizione sia sempre l’uguaglianza allora si parla di **equi-join**.
![[Pasted image 20240220025157.png]] ![[Pasted image 20240220025225.png]]
### Self join
Possiamo effettuare una join con la solita tabella.

Supponiamo ad esempio di considerare la seguente relazione:
![[Pasted image 20240220021918.png]]
E di volere ottenere la relazione Nonno-Nipote. In questo caso dobbiamo utilizzare due volte la stessa tabella.

Tuttavia in questo caso avremo che $Genitore \Join Genitore = Genitore$ in quanto gli attributi coincidono. Effettuiamo quindi prima una ridenominazione: $\rho_{Nonno, Genitore \leftarrow Genitore, Figlio}(Genitore)$
![[Pasted image 20240220022008.png]]
A questo punto effettuando un natural join con la tabella genitore otterremo l’informazione cercata.![[Pasted image 20240220022027.png]]



# Quantificatore esistenziale
almeno uno che soddisfa la condizione
	![[Pasted image 20240220195756.png] 
	![[Pasted image 20240220195610.png]]		![[Pasted image 20240220195712.png]]
	Sono uguali in quanto sono trasformazioni logiche ![[Pasted image 20240220200047.png]]
	Per selezionare gli studenti che non hanno mai preso un voto maggiore di 28 uso la differenza insiemistica  ![[Pasted image 20240220200134.png]]
# Quantificatore universale
Voglio selezionare solo gli studenti che hanno sempre preso voti maggiori di 28. Per far ciò prima seleziono quelli che hanno preso di meno di 28 e poi sottraggo questa relazione dalla relazione degli studenti ![[Pasted image 20240220200721.png]]
ma in questo modo gli studenti che non hanno mai ottenuto esami vengono restituiti nella relazione finale. 
Per evitare ciò prima di sottrare si selezionano gli studenti che hanno sostenuto esami.![[Pasted image 20240220201020.png]]


# Non distributività della proiezione rispetto alla differenza

^32312d

In generale vale che : $\pi_A(R_1-R_2) \neq \pi_A(R_1)-\pi_A(R_2)​$ 

Se $R_1$ e $R_2$ sono definite su $AB$ e contengono valori uguali su $A$ e diversi su $B$ NON è possibile che ci sia uguaglianza.

Può esserci se i valori di A sono tutti diversi.
# Raggrupamento

Raggruppamento: ${ _{\{ A_i\}} Y_{ \{ f_i \} } }(R)$


Gli $A_i$ sono attributi di $R$ e le $f_i$ sono espressioni che usano funzioni di aggregazione (max, min, count, sum, …)

Il valore del raggruppamento è una relazione calcolata come segue:

- Si partizionano le ennuple di $R$ mettendo nello stesso gruppo tutte le ennuple con valori uguali degli $A_i$
- Si calcolano le espressioni $f_i$ per ogni gruppo
- Per ogni gruppo si restituisce una sola ennupla con attributi i valori degli $A_i$ e delle espressioni $f_i$

Se raggruppo su due attributi prima raggruppo sul primo e poi raggruppo ogni raggruppamento sul secondo.
L'ordine degli attributi di raggruppamento è concettualmente diverso ma poi il risultato è uguale.

[[Esempi raggruppamento]]

Se raggruppo su [[Modello relazionale - chiave|chiave primaria]] ottengo la colonna della chiave primaria e se faccio $Count(*)$ esce 1 per ogni ennupla.


# Proprietà

- ___TRASFORMAZIONI ALGEBRICHE___
	Si basano su regole di equivalenza fra espressioni algebriche e consentono di scegliere diversi ordini di join e di anticipare proiezioni e restrizioni 
	![[Pasted image 20240221023637.png]]
- ___ATOMIZZAZIONE DELLE SELEZIONI___
	$\sigma _{F_1 \land F_2}(E) = \sigma_{F_1} (\sigma_{F_2}(E))$  
	Una selezione congiuntiva può essere sostituita da una cascata di selezioni atomiche
- ___IDEMPOTENZA DELLE PROIEZIONI___
	Una proiezione può essere trasformata in una cascata di proiezioni che eliminano i vari attributi in fasi diverse se la relazione E è definita su un insieme di attributi che contiene Y oltre che X
	$\pi_X(E)=\pi_X(\pi_{XY}(E))$
	
	Non ha effetto sull’efficienza. Ha effetto sulla leggibilità della query.
- ___Anticipazione della selezione rispetto al Join (Pushing Selection down)___
	$\sigma_F(E_1\Join E_2)=E_1\Join \sigma_F(E_2)$
	
	Vale se F fa riferimento solo ad attributi di E2. 
	Aumenta l’efficienza della query perché la selezione riduce il numero delle righe di E2 prima del join.
- ___Anticipazione della proiezione rispetto al join (Pushing Projections down)___
	$\pi_{X_1Y_2}(E_1\Join E_2)=E_1\Join\pi_{Y_2}(E_2)$ 
	
	Vale se $E_1$ e $E_2$ sono definite rispettivamente su $X_1$ ed $X_2$, se $Y_2\subseteq X_2$ e se gli attributi in $X_2-Y_2$ non sono coinvolti nel join.
	
	Non ha effetto sull'efficienza ma sulla leggibilità 
- ___Distributività della selezione rispetto all’unione___
	$\sigma_F(E_1\cup E_2) = \sigma _F (E_1)\cup \sigma_F(E_2)$ 
- ___Distributività della selezione rispetto alla differenza___
	$\sigma_F(E_1 - E_2) = \sigma _F (E_1) - \sigma_F(E_2)$ 
- ___Distributività della proiezione rispetto all’unione___
	$\pi_X(E_1\cup E_2)=\pi_X(E_1)\cup \pi_X(E_2)$
- [[#^32312d|Non Distributività della proiezione rispetto alla differenza]]
	In generale vale che : $\pi_A(R_1-R_2) \neq \pi_A(R_1)-\pi_A(R_2)​$ 
	
	Se $R_1$ e $R_2$ sono definite su $AB$ e contengono valori uguali su $A$ e diversi su $B$ NON è possibile che ci sia uguaglianza.
	
	Può esserci se i valori di A sono tutti diversi.
- ___Inglobamento di una selezione in un prodotto cartesiano a formare un join___
	$\sigma_F(R_1\Join R_2) = R_1\Join_F R_2$
- ___Altre equivalenze___
	- $\sigma_{F_1\lor F_2}(R)\equiv \sigma_{F_1}(R)\cup \sigma_{F_2}(R)$
	- $\sigma_{F_1\land F_2}(R)\equiv \sigma_{F_1}(R)\cap \sigma_{F_2}(R)$
	- $\sigma_{F_1\land\lnot F_2}(R)\equiv \sigma_{F_1}(R)- \sigma_{F_2}(R)$
- Valgono proprietà commutativa e associativa di tutti gli operatori binari (unione, intersezione, join) tranne la differenza

# Operatore algebrici non insiemistici 
- $\pi^b_{\{A_i\}}(R)$ : proiezione multiinsiemistica (senza eliminazione dei duplicati)
- $\tau_{\{A_i\}}(R)$ : ordinamento

# Calcolo relazionale su ennuple
Il calcolo relazionale è un linguaggio che permette di definire il risultato di un’interrogazione come l’insieme di quelle ennuple che soddisfano una certa condizione 𝜙. 
	L'insieme delle matricole degli studenti che hanno superato qualcuno degli esami elencati nella relazione Materie(Materia) si può definire come:
	$\{ t.Matricola\ | \ t\in Studenti, \ \exists m\in Materie.\ \exists e\in ProveEsami.\ e.Candidato = t.Matricola\land e.Materia = m.Materia \}$
	Che equivale a : $\pi_{Matricola}(Studenti\Join_{matricola=candidato}(ProveEsami \Join Materie))$
	
	
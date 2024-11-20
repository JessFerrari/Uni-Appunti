---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Forme normali]]"
tags:
  - BD
Creation: 2024-02-26
Esempi: "[[Esempi forme normali]]"
---
# Forme Normali - Boyce-Codd
---
La forma normale _normale di Boyce-Codd_  un [[Normalizzazione di schemi|criterio per la rimozione di anomalie]] (Normalizzazione).

L'idea su cui si basa la la forma _normale di Boyce-Codd_ è che una [[Dipendenze funzionali|dipendenza funzionale]] $X \to A$ dove $X$ non ha [[Copertura#Attributo estraneo|attributi estranei]] indica che nel dominio che si modella esiste una collezione $C$ di entità che sono univocamente identificate da $X$.


Quindi se una relazione contiene $X$ allora posso accadere solo due cose
1. la _relazione_ modella $C$ allora $X$ deve essere [[Modello relazionale - chiave|chiave]]
2. la _relazione_ NON modella $C$ allora $X$ deve essere una [[Modello relazionale - chiave|chiave esterna]]


##### Forma normale Boyce-Codd
_Sia_ $R\langle T,F\rangle$ uno [[Modello Relazionale|schema relazionale]] 
	$R$ è in _BCNF_ (Boyce-Codd normal form)
	_se e solo se_ 
	$\forall X\to Y \in F^+$  vale che $X$ è _[[Modello relazionale - chiave|superchiave]]_ con $X \to Y$ _dipendenza non banale_

Si ha che quindi la definizione _dipende_ dalla [[Schema relazionale - Chiusura|chiusura]] di $F$ e non quindi dalla _[[Copertura|copertura scelta]]_.

Le dipendenze che non sodisfano questa proprietà sono dette _anomale_

> [!nota]
> nella pratica non si usa direttamente questa forma siccome calcolare $F^+$ è un operazione _molto costosa_.

##### Teorema
_sia_ $R\langle T,F\rangle$ uno [[Modello Relazionale|schema relazionale]]
_se e solo se_ $\forall X\to Y \in F$  vale che $X$ è _[[Modello relazionale - chiave|superchiave]]_ 
- con $X \to Y$ _dipendenza non banale_
_allora_ $R$ è in _BCNF_ (Boyce-Codd normal form)

##### Corollario
_sia_
- $R\langle T,F\rangle$ uno [[Modello Relazionale|schema relazionale]]
- $F$ in forma di [[Copertura|copertura canonica]]
_se e solo se_  $\forall X\to Y \in F$  vale che $X$ è _[[Modello relazionale - chiave|superchiave]]_ in questo caso anche _chiave_
- con $X \to Y$ _dipendenza elementare_ e _non banale_
_allora_ $R$ è in _BCNF_ (Boyce-Codd normal form)



#### Normalizzazione in BCNF
Il processo di normalizzazione in BCNF è fatto tramite un algoritmo detto di __analisi__ per la trasformazione di un _schema relazionale_ con _dipendenze anomale_ in uno senza dipende anomale in _forma normale BCNF_


$R<T,F>$ è decomposta in $R_1(X,Y)$ e $R_2(X,Z)$ e su di esse si ripete il procedimento esponenziale.

_Input_: $R<T,F>$ con $F$ copertura canonica

_Output_: decomposizione in BCNF che preserva i dati
```pseudo
	\begin{algorithm}
	\caption{Normalizazione in forma BCNF}
	\begin{algorithmic}
	\Function{NormalizationBCNF}{$R\langle T,F\rangle$}
	\State $\rho = \{R\langle T,F\rangle\}$
	\State $n=1$
	\While{$\exists R\langle T_i,F_i\rangle \in \rho$ non in BCNF per dipendenze $X \to A$}
	\State $n=n+1$
	\State $T'=X^+$
	\State $F'=\pi_{T'}(F_i)$
	\State $T'' = T_i - (T'-X)$
	\State $F'' = \pi_{T''}(F_i)$
	\State $\rho=\rho - R_i\langle T_i,F_i\rangle + \{R_i\langle T',F'\rangle,R_n \langle T'',F'' \rangle\}$
	\EndWhile
	\EndFunction
	\end{algorithmic}
	\end{algorithm}
```
La _[[Decomposizione dei schemi|decomposizione]]_ trovata da questo algoritmo non è l'unica possibile, l'output dipende dal ordine con cui si valuta $F$.
Data una relazione, non è sempre possibile ottenere una decomposizione in FNBC.

L'algoritmo preserva i dati ma non necessariamente le dipendenze.

L'algoritmo ha [[Complessità|complessità]] _esponenziale_ a causa del calcolo della [[Decomposizione dei schemi|proiezione delle dipendenze funzionali]], esistono algoritmi polinomiali ma non si utilizzano in pratica perché la decomposizione creta è poco "_naturale_" e troppo _decomposta_.

L'algoritmo non garantisce sempre che la decomposizione risultate _preservi le dipendenze_ infatti ci sono dei schemi che non possono essere trasformati in BCNF mantenendo l'equivalenza.
Contrariamente _preserva sempre i dati_ e questo viene dal _seguente teorema_:

##### Teorema
_sia_
- $R\langle T,F\rangle$ uno [[Modello Relazionale|schema relazionale]]
- $\rho= \{ R_1,\dots R_m \}$ una [[Decomposizione dei schemi|decomposizione]] di $R$ che _preserva i dati_
- $\sigma=\{ S_1,S_2 \}$ una _decomposizione_ di $R_1$ che _preserva i dati_ rispetto a $\pi_{T_1}(F)$
_allora_ anche la decomposizione $\rho = \{ S_1,S_2,R_2,\dots R_m \}$ preserva _i dati rispetto_ a $F$
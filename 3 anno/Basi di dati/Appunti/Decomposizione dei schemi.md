---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Normalizzazione di schemi]]"
tags:
  - BD
Creation: 2024-02-26
---
# Decomposizione di schemi
La _decomposizione_ degli [[Modello Relazionale|schemi relazionali]] è un operazione necessaria per la rimozione delle _anomalie_.
Questo si fa _scomponendo_ schemi che si presentano con _relazioni grandi_ in _relazioni più piccole_ che sodisfano certe proprietà ovvero sono in _[[Forme normali|forme normali]]_.

La decomposizione è un'operazione delicata in quanto potrebbe far perdere informazione.

## Intuizione
L'intuizione è che si devono estrarre gli attributi che vengono determinati da attributi non chiave, ossia creare uno schema per ogni funzione.
![[Pasted image 20240226064738.png]]

Se lo schema fosse stato questo qui sotto che ammette le [[Dipendenze funzionali|dipendenze funzionali]] Impiegato->Sede e Progetto->Sede non si potrebbe decomporre in base ad esse perché si perderebbe l'informazione che l'impiegato e il progetto devono essere nella stessa sede.
![[Pasted image 20240226065135.png]]
Inoltre se le andassi a ricongiungere cin un join si andrebbero a creare delle tuple spurie![[Pasted image 20240226065231.png]]

## Decomposizione (Definizione)

Dato uno [[Modello Relazionale|schema relazionale]] $R(T)$  
	$\rho=\{ R_{1}(T_{1}),\dots R_{K}(T_{K}) \}$ è una _decomposizione_ di $R(T)$ $\iff$ _se_ $\bigcup_{i}T_{i} =T$ 

>[!note]
>le relazione nella decomposizione $\rho$ non sono _necessariamente disgiunte_
![[Pasted image 20240226181505.png]]
	Due proprietà desiderabili sono :
	- La conservazione dei dati
	- La conservazione delle dipendenze





## Conservazioni dei dati
Garantisce la ricostruzione delle informazioni originarie senza generazione di tuple spurie.
### DEFINIZIONE:
$\rho= \{ R_{1}(T_{1}),\dots,R_{k}(T_{k})\}$ è una _decomposizione_ di uno [[Modello relazionale|schema relazionale]] $R \langle T,F \rangle$ se e solo se
	per ogni relazione $r$ che soddisfa $R \langle T,F \rangle$ (ISTANZA VALIDA) vale che il join delle proiezioni di $r$ sugli insiemi di attributi $T_1,...T_k$ danno la relazione $r$ di partenza$$r = \pi_{T_1}(r)\bowtie\dots \bowtie\pi_{T_k}(r)$$
_allora_ $\rho$ è una _decomposizione che preserva i dati_ 



### Decomposizione con perdita di informazioni
	![[Pasted image 20240226181957.png]]
	Se si facesse il join di Studenti ed Esami non si perderebbe nessuna tupla ma si creerebbero delle tuple spurie.
	Ad esempio se due persone hanno lo stesso nome e hanno sostenuto due esami diversi, dopo la giunzione si avrebbe che una persona ha svolto anche l'esami dell'altra.

### Decomposizione senza perdita di informazioni
	![[Pasted image 20240226182340.png]]
	In questo modo non avrei perdita di informazioni in quanto il join verrà effettuato su una chiave.
	Perciò l'unico modo per non avere perdita di informazioni è avere una chiave.

Uno schema $R\langle T,F\rangle$ si decompone senza perdita dei dati negli schemi $R_1(X_1)$ ed $R_2(X_2)$ se, per ogni possibile istanza $r$ di $R(X)$, il [[Modello relazionale - Algebra relazionale#Join naturale|join naturale]] delle [[Modello relazionale - Algebra relazionale#Proiezione|proiezioni]] di $r$ su $X_1$ ed $X_2$ produce la tabella di partenza (non si hanno ennuple spurie).
$$\pi_{X_1}(r) \Join \pi_{X_2} (r) = r​$$
La decomposizione senza perdita è garantita se l’insieme degli attributi comuni alle due relazioni $(X_1 ∩ X_2)$ è chiave per almeno una delle due relazioni decomposte. 
### Teorema della decomposizione senza perdita di informazione
Sia $r$ una relazione su un insieme di attributi $X$ e siano $X_1$ e $X_2$ due sottoinsiemi di $X$ la cui unione sia pari ad $X$ stesso. ($X_1\cup X_2=X$)
Inoltre sia $X_0$ l’intersezione di $X_1$ e $X_2$ ($X1\cap X_2=X_0$) allora: 
	$r$ si decompone senza perdita di informazione su $X_1$ e $X_2$ se :
	- soddisfa la dipendenza funzionale $X_0 \to X_1$ 
	oppure 
	- la dipendenza funzionale $X_0 \to X_2$.

> [!Tip] Tip
> Se l'insieme degli attributi comuni alle due relazioni $(X_1\cap X_2)$ è chiave per almeno una delle due relazioni decomposte, allora la decomposizione è senza perdita di informazioni 

Ciò perché 
	Se l’insieme degli attributi comuni alle due relazioni $(X_1 ∩ X_2)$ è chiave per almeno una delle due relazioni decomposte allora la decomposizione è senza perdita
#### Dimostrazione

Supponiamo r sia una relazione sugli attributi ABC e consideriamo le sue proiezioni r1 su AB e r2 su AC. 
	Supponiamo che r soddisfi la dipendenza funzionale A → C. 
	Allora A è chiave per r su AC e quindi non ci sono in tale proiezione due tuple diverse sugli stessi valori di A

Il join costruisce tuple a partire dalle tuple nelle due proiezioni

- Sia $t=(a,b,c)$ una tupla del join di $r_1$ e $r_2$.
- Mostriamo che appartiene ad $r$ (vale a dire che non è spuria):
    - $t$ è ottenuta mediante join da $t_1=(a,b)$ di $r_1$ e $t_2=(a,c)$ su $r_2$.
    - Allora per definizione di proiezione esistono due tuple in $r$, $t_1'=(a,b, * )$ e $t_2'=(a, *,c)$ (dove $*$ sta per un valore non noto).
    - Poiché $A \rightarrow C$, allora esiste un solo valore in $C$ associato al valore $a$. Dato che $(a, c)$ compare nella proiezione, questo valore è proprio $c$.
    - Ma allora nella tupla $t_1'$ il valore incognito deve essere proprio $c$. Quindi $(a, b, c)$ appartiene ad $r$.

### Decomposizioni Binarie

#### Teorema

Sia $R<T,F>$ uno [[Modello relazionale|schema di relazione]], la decomposizione $\rho = \{ R_1(T_1), R_2(T_2) \}$ _preserva i dati_ se e solo se:

- $T_1 \cap T_2 \rightarrow T_1 \in F^+$ 
	oppure 
- $T_1 \cap T_2 \rightarrow T_2 \in F^+$

Ossia preserva i dati se la dipendenza funzionale tra l'intersezione dei due insiemi d'attributi che derivano uno o l'altro insieme si trova nella [[Schema relazionale - Chiusura#^6c6857|chiusura]] di $F^+$, ossia se $T_1 \cap T_2$ è [[Dipendenze funzionali#Chiave|chiave]]  

##### Dimostrazione_
$( \ \Longleftarrow\ )$: 
_Sopponiamo_ che $T_{1} \cap T_{2} \rightarrow T_1 \in F^+$
_sia_ 
- $r$ un istanza valida di $R\langle T,F\rangle$ 
- $s=\pi_{T_1}(r) \bowtie\pi_{T_2}(r)$ una decomposizione di $R$
- $t$ una _ennupla_
assumendo $t \in s$ bisogno dimostrare che $t \in r$
per _definizione_ di $s$ _esistono_ due _ennupla_ $u,v\in r$ tale che
- $u[T_1]=t[T_1]$
- $v[T_2]=t[T_2]$
- $u[T_1 \cap T_2] =v[T_1 \cap T_2]=t[T_1 \cap T_2]$
_siccome_ $T_1 \cap T_2 \rightarrow T_1 \in F^+$ vale che 
- $u[T_1]=v[T_1]\implies t=v$

Il caso $T_{1} \cap T_{2} \rightarrow T_2 \in F^+$ è _analogo_ con $t=u$

$( \implies )$: 
Sopponiamo che _pero ogni_ istanza valida $r$ di $R \langle T,F\rangle$ valga che $r =\pi_{T_1}(r) \bowtie \pi_{T_2}(r)$ 

Bisogna dimostrare che valga $T_1 \cap T_2 \rightarrow T_1 \in F^+$ o $T_1 \cap T_2 \rightarrow T_2 \in F^+$ 
dimostriamo per [[Tipi di dimostrazioni|assurdo]] assumendo che nessune delle due implicazioni _condizioni sino verificate_

_sia_
- $W = (T_1 \cap T_2)^+$
- $Y_1=T_1-W$
- $Y_2=T_2 - W$
abbiamo che $Y_1,Y_2$ sono non vuoti per _ipotesi_ e $Y_1,Y_2,W$ sono una [[Partizione|partizione]] di $T$ 

per ogni $A_i\in T,1\leq i\leq k$ consideriamo due valori $a_i,a_i'\in dom(A_i)$ con $a_i\not=a_i'$
_costruiamo_ le relazione $r$ con attributi $WY_1Y_2$ formate dalle due ennuple
- $e_{1}=a_{i} \ \ \ 1 \leq i\leq k$
- $e_{2}=\begin{cases}a_{i}&if&A_{i} \in W\\ a_{i}'& if & A_{i}\in Y_{1}Y_{2}\end{cases}$
$r$ _soddisfa ogni dipendenza_ $V \rightarrow Z \in F$ infatti 
- _se_ $V \not\subseteq W \implies e_1[V] \not=e_2[V]$ ed $r$ soddisfa ovviamente la dipendenza 
- _se_ $V \subseteq W\implies(T_1 \cap T_2 )\rightarrow V$ e per _[[Schema relazionale - Assiomi di Armstrong|transitività]]_ vale $(T_1 \cap T_2 )\rightarrow Z$ quindi $Z \subseteq W$  e $e_1[Z]=e_2[Z]$ e quindi $r$ sodisfa la [[Dipendenze funzionali|dipendenza]]

poiché $Y_1,Y_2$ non sono _vuoti_ $\pi_{T_1}(r)$ e $\pi_{T_2}(r)$ contengono due _ennuple_ e la loro [[Modello relazionale - Algebra Relazionale|giunzione naturale]] ne contiene $4$ che sono più di quelle di $r$ quindi $$\pi_{T_1}(r)\bowtie\pi_{T_2}(r)\not=r$$ _contradicendo l ipotesi_.

>[!note]
>questo risultato è stato _generalizzato_ con un numero $n$ di relazioni nella decomposizione anzi che solo 2



## Conservazione delle dipendenze

Una delle proprietà della decomposizione degli schemi relazionali e quello di conservare le _[[Dipendenze funzionali|dipendenze]]_.
Garantisce il mantenimento dei vincoli di integrità (di dipendenza funzionale) originari.

Una decomposizione conserva le dipendenze se ciascuna delle dipendenze funzionali dello schema originario coinvolge attributi che compaiono tutti insieme in uno degli schemi decomposti.

Questo è importante siccome _se non_ si conservassero le dipendenze dello schema originale si potrebbero inserire nel database delle _ennuple_ che soddisfano le dipendenze delle singole tabelle della decomposizione ma _non_ le dipendenze della tabella originali, rendendo cosi i due schemi relazionali non equivalenti
![[Pasted image 20240226190241.png]]
In questa decomposizione si perde il fatto che impiegati che partecipano ad un progetto devono essere nella stessa sede. Infatti se si aggiungesse che Verdi partecipa al progetto Marte non ci sarebbero problemi per le due relazioni di decomposizione ma non rispetterebbe il vincolo della relazione iniziale. 


### Proiezione di un insieme di dipendenze (definizione)
Dato lo  [[Modello Relazionale|schema relazionale]] $R \langle T,F\rangle$ e $T_i \subseteq T$ un sotto _insieme di attributi T_
la decomposizione $\rho =\{R_1,...,R_n \}$ _preserva le dipendenze_ se e solo se l'unione delle dipendenze nella [[Modello relazionale - Algebra Relazionale|proiezione]] di $F$ su $T_i$, definita come $$\pi_{T_i}(F)=\{ X \rightarrow Y \in  F^+ \mid X,Y \subseteq T_i \}$$ è una copertura di F.

> [!NOTE] ### Proposizione
> Dato lo schema $R<T,F>$, il problema di stabilire se la decomposizione $\rho = \{ R_1, ..., R_n \}$ preserva le dipendenze ha [[Complessità|complessità]] di tempo polinomiale
> 

##### Algoritmo banale per il calcolo della copertura della proiezione delle dipendenze
un algoritmo _banale_ di [[Complessità|complessità]] _esponenziale_ per calcolare un _copertura_  di $\pi_{T_i}(F)$ è il seguente
```pseudo
	\begin{algorithm}
	\caption{Copertura di $\pi_{T_i}(F)$ }
	\begin{algorithmic}
	\Function{FindCover}{F,$T_i$}
	\State $\pi_{T_i}=\emptyset$
	\For{$\boldsymbol{each} \ Y \subset T_i$ }
	\State $Z:=Y^+_F-Y$
	\State $\pi_{T_i} =\pi_{T_i} \cup Y\rightarrow (Z \cap T_i)$
	\EndFor 
	\Return $\pi_{T_i}$
	\EndFunction 
	\end{algorithmic}
	\end{algorithm}
```

##### Decomposizione che preserva le dipendenze (definizione)
Dato lo [[Modello relazionale|schema relazionale]] $R \langle T,F\rangle$ 
la decomposizione su $R$ $\rho=\{ R_1(T_1),\dots R_n(T_n) \}$ preserva le dipendenze se e solo se l'unione delle dipendenze in $\pi_{T_i}(F)$ è una [[Copertura|copertura]]
 $\bigcup \pi_{T_i}(F) \equiv F$ dove $\pi_{T_i}$ è una _proiezione_ su $F$ 



> [!Tip] Conservazione dei dati e delle dipendenze 
> Sia $\rho=\{R_i\langle T_i,F_i\rangle \}$ una decomposizione di $R_i\langle T_i,F_i\rangle$ che preserva le dipendenze e tale che $T_j$ per qualche $j$ è una superchiave per $R_i\langle T_i,F_i\rangle$ allora $\rho$ preserva i dati

 


##### Determinare se una decomposizione preserva le dipendenze
per controllare che una data decomposizione preservi le dipendenze dobbiamo controllare che $\forall X \rightarrow Y \in F$ valga che $X \rightarrow Y \in G^+$ con la  $G^+$ [[Schema relazionale - Chiusura|chiusura]] e $G = \bigcup \pi_{T_i}(F)$ 

Calcolando la [[Schema relazionale - Chiusura|chiusura]] di $X$ rispetto a $G$ indicata con $X^+_G$ si può evitare di _calcolare esplicitamente_ $G^+$
```pseudo
	\begin{algorithm}
	\caption{Copertura di $X$ rispetto $G$}
	\begin{algorithmic}
	\Function{CalcoloXPIU}{$\rho$,$X$}
	\State $X_G^+=X$
	\While{$X_G^+$ è cambiato}
	\For{$\boldsymbol{each} \ i=1 \ \boldsymbol{to}\ k$}
	\State $X_G^+=X_G^+\cup ((X^+_G \cap T_i)^+_G\cap T_i)$
	\EndFor
	\EndWhile
	\Return $X_G^+$
	\EndFunction
	\end{algorithmic}
	\end{algorithm}
```
e $(X^+_G \cap T_i)^+$ viene [[Schema relazionale - Chiusura|con l algoritmo di chiusure veloce]] che ha [[Complessità|complessità polinomiale]]
ed agni passo l _istruzione_ nel for  aggiunge a $X^+_G$ gli attributi $A_i$ tali che $(X_G^+ \cap T_i \rightarrow A_i \in \pi_{T_i}(F)$ 

e quindi l'algoritmo di determinazione segue come
```pseudo
	\begin{algorithm}
	\caption{decidere se $\rho$ preserva le dipendenze}
	\begin{algorithmic}
	\Function{CheckIfPreserveDipendency}{$\rho$}
	\For{$\boldsymbol{each}\  X \rightarrow Y \in F$}
	\State $X_G^+ =$ \Call{CalcolaXPIU}{$\rho$,$X$}
	\If{$Y \not\subseteq X_G^+$}
	\Return false
	\EndIf
	\EndFor
	\Return true
	\EndFunction
	\end{algorithmic}
	\end{algorithm}
```
e questo è un algoritmo _polinomiale_

#### Decomposizione che preserva Dati e dipendenze

Il _preservare_ dati e _dipendenze_ di una decomposizione sono due __proprietà indipendenti__, ma esiste un criterio per assicurare di averli entrambi.

##### Criterio di Sufficienze
_sia_
- $R \langle T,F\rangle$
- $\rho=\{ R_i\langle T_i,F_i\rangle \}$ una _decomposizione_ di $R$
_Se_
- $\rho$ _preserva e dipendenze_
- $\exists j. T_j$ è [[Modello relazionale - chiave#Superchiave|superchiave]] per $R$
_allora_ $\rho$ preserva _anche i dati_


###### _Dimostrazione_
si assume senza perdita di generalità che $T_1$ sia [[Modello relazionale - chiave#Superchiave|superchiave]] di $R$
Dobbiamo dimostrare che per ogni istanza $r$ di $R$ valga $$\pi_{T_1}(r) \bowtie \dots \bowtie \pi_{T_n}(r) \subseteq r$$ sia $e \in  \pi_{T_1}(r) \bowtie \dots \bowtie \pi_{T_n}(r)$ 
per _[[Modello relazionale - Algebra Relazionale|definizione di giunzione]]_ si ha che esistono $e_i \in \pi_{T_i}(r)$ tale che per $i$ in $i,\dots,n,e_i[T_i]=e[T_i]$
per _[[Modello relazionale - Algebra Relazionale|definizione di proiezione]]_  esistono $e_i' \in r$ tale che per $i$ in $1,\dots,n,e'_i[T_i]=e_i[T_i]$ da cui $e'_i[T_i]=e[T_i]$

allora basta dimostrare che $e=e_1'$ siccome da questo segue la tesi poiché $e'_1 \in r$

Costruendo la relazione $s$ con schema $R(T)$ con solo le due ennuple $e$ e $e'_1$ se questa soddisfa $F$ allora vale $e=e_1'$ siccome queste due coincidono sulla _superchiave_

Poiché la scomposizione _preserva le dipendenze_, è sufficiente dimostrare che $s$ soddisfa $\pi_{T_i}(F)$ per ogni $i$  
osservando che per goni dipendenze $X \rightarrow Y$ e per ogni $T' \subseteq T$ che includa $X,Y$ un relazione $r \in \langle T,F \rangle$ soddisfa la dipendenza se e solo se la soddisfa $\pi_{T'}(r)$.
Quindi anche $s$ soddisfa $\bigcup_i\pi_{T_i}(F) \iff \pi_{T_i}$ ovvero $\{ e[T_i],e'[T_i]\}$ soddisfa $\pi_{T_i}(F)$ per ogni $i$

$\{ e[T_i],e'[T_i]\}$ soddisfa $\pi_{T_i}(F)$  poiché $\{ e[T_i],e'[T_i]\} \subseteq \pi_{T_i}(r)$ e quindi $e_i'[T_i]=e_i[T_i]$ e $e'_1$ ed $e_i'$ sonno entrambi in $r$
---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Dipendenze funzionali derivate]]"
tags:
  - BD
Creation: 2024-02-25
---
# Chiusura di un'insieme F

^6c6857

Dato F un insieme di dipendenze funzionali, la chiusura $F^+$ di F è denotata con$$F^+=\{X\to Y|F\vdash X\to Y\} $$
$F^+$ è l'insieme completo di tutte le Dipendenze funzionali che sono implicate da quelle di partenza.

***Problema dell'implicazione***: decidere se una dipendenza funzionale appartiene a F+  
	La sua risoluzione con l’algoritmo banale (di generare F+ applicando ad F ripetutamente gli assiomi di Armstrong) ha una [[Complessità|complessità]] esponenziale rispetto al numero di attributi dello schema.

# Chiusura di insieme  attributi su insieme di dipendenze (Definizione)
_Sia_
- $R\langle T,F \rangle$ uno [[Modello relazionale|schema relazionale]] 
-  $X \subseteq T$ un sotto insieme di _attributi_
 _allora_ la _chiusura_ di $X$ rispetto a $F$ è data da $$X_F^+=\{ A \in  T \mid F \vdash X \rightarrow A \}$$
Ovvero è l'[[Insiemi|insieme]] di tutti gli _attributi_ che _[[Dipendenze funzionali|dipendono funzionalmente]]_ direttamente o tramite [[Dipendenze funzionali derivate|derivazione]] da $X$ utilizzando gli [[Schema relazionale - Assiomi di Armstrong|assiomi di Armstrong]]  

Si scrive $X^+$ quando $F$ è chiaro dal contesto

***Problema dell'implicazione*** : controllare se una dipendenza funzionale $V\to W\in F^+$  
Un algoritmo efficiente per risolvere il problema dell’implicazione senza calcolare la chiusura di F scaturisce dal seguente teorema.
##### Teorema
_Sia_ $F$ un [[Insiemi|insieme]] di _[[Dipendenze funzionali|dipendenze funzionali]]_ 
_Se_ la [[Dipendenze funzionali derivate|derivazione]] è fatta con gli [[Schema relazionale - Assiomi di Armstrong|Assiomi di Armstrong]]
_Allora_ $$F \vdash X \rightarrow Y \iff Y \subseteq X^+$$
è possibile derivare X->Y se Y fa parte della chiusura $X^+$

L'algoritmo ha costo polinomiale


_Dimostrazione_: _Sia_ $Y = A_1 \dots A_k, A_i \in  T$.
$(\implies)$ :
	per _decomposizione_ vale che $F \vdash X \rightarrow A_i \ \ 1 \leq i \leq k$
	per _definizione_ di $X^+$ vale che $A_i \in  X^+,\ \  1 \leq i \leq k$ 
	_quindi vale_ $Y \subseteq X^+$
	
$(\ \Longleftarrow\ )$ :
	per _definizione_ di $X^+$ vale che $F \vdash X \rightarrow A_i \ \ 1 \leq i \leq k$
	per _unione_ vale che $F \vdash X \rightarrow A_1, \dots , A_k$ 
	_quindi vale_   $F \vdash X \rightarrow Y$	

# Algoritmo per calcolare $X_F^+$

Sia X un insieme di attributi e F un insieme di dipendenze.
Si vuole calcolare $X_F^+$.

1. Si inizializza $X^+$ con l'insieme $X$
2. Se fra le dipendenze funzionali di F c'è una dipendenza $Y\to A$ con $Y\subseteq X^+$ allora si inserisce A in $X^+$, ossia $X^+=X^+\cup \{A\}$
3. Si ripete il passo 2 fino a quando non ci sono altri attributi da aggiungere a $X^+$
4. Si da in output $X_F^+=X^+$

## Chiusura lenta
Un semplice algoritmo per calcolare $X^+$ è 

***Algoritmo CHIUSURA LENTA*** 

**input** R<T, F> X $\subseteq$ T 
**output** $X^+$

**begin** 
$X^+ = X$                        
while ($X^+$ cambia) do                                      
	for $W → V$ in F with $W\subseteq X^+$ and $V \lor X^+$ 
		do $X^+ = X^+ \cup V$
 **end**


Si da in input $X^+_F=X^+$, si inizializza $X^+$ con $X$, finché ci sono attributi da aggiungere a $X^+$ se fra le DF di F ce n'è una W->V e W fa già parte della chiusura si aggiunge V a $X^+$

#### Terminazione
L’algoritmo termina perché ad ogni passo viene aggiunto un nuovo attributo a X+.
Essendo gli attributi in numero finito, a un certo punto l’algoritmo deve fermarsi.

#### Correttezza
Per dimostrare la correttezza, si dimostra che $X_F^+$ = $X ^+$ per induzione

##### Analisi della [[Complessità|complessità]]
_Sia_ 
- $|T|=\#a$ il _numero_ degli attributi
- $|F|=\# p$ il _numero_ delle [[Dipendenze funzionali|dipendenze funzionali]]

Il __ciclo while__ viene eseguito 
- _Al più_ $p$ volte siccome ogni dipendenza funzionale da il suo contributo alla chiusura _al più_ una volta
- _Al più_ $a$ volte siccome si possono aggiungere _al più_ $a$ attributi.
risultando in esecuzione $O(min(a,p))$

Per ogni ciclo While, il __ciclo interno for__ viene eseguito al più $p$ volte e ogni volta si controllano _due inclusioni di [[Insiemi|insiemi]]_.
Il test di inclusione _tra insiemi ordinati_ di $a$ elementi ha una [[Complessità|complessità]] di tempo $O(a)$
e quindi la [[Complessità|complessità]] del ciclo interno è $O(pa)$

Quindi in totale l’algoritmo _Chiusura lenta_ ha [[Complessità|complessità]] di tempo, nel caso peggiore $O(ap \cdot min(a, p))$.



# Chiusura veloce - non lo chiede
Questo algoritmo è migliore a livello di [[Complessità|complessità]] di tempo $O(ap)$ )



## Esempio chiusura lenta

$F = {DB → E, B → C, A → B}$, 
Si deve trovare $(AD)^+$:
Si vogliono conoscere gli attributi che sono determinati funzionalmente da un insieme di dipendenze A e D. 

1. X+ = AD , Inizializzo la chiusura con l'insieme di attributi 
2. X+ = ADB, applico A->B dato che è l'unica DF applicabile, e aggiungo B
3. X+ = ADBE, ora applico la DF DB->E e aggiungo E
4. X+ = ADBEC , ed infine applico B->C ed aggiungo C

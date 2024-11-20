---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Normalizzazione di schemi]]"
tags:
  - BD
Creation: 2024-02-27
Esempi: "[[Esempi forme normali]]"
---
# Forme Normali - Terza forma
---
#### Terza Forme normale 
La _terza forma normale_ è un criterio per qualità per la rimozione delle anomalie 
La _terza forma normale_ è meno restrittiva della [[Forme Normali - Boyce-Codd|BCNF]]
La _terza forma normale_ preserva i [[Decomposizione dei schemi|dati e le dipendenze]] ed è calcolabile in tempo polinomiale, Ma può mantenere certe _anomalie_.

#### Intuizione
Intuizione: Una relazione $r$ è in _terza forma normale_ (3NF) se, per ogni FD non banale $X \rightarrow Y$ definita su $r$, è verificata almeno una delle seguenti condizioni:

- $X$ contiene una chiave $K$ di $r$ (come nella BCNF)
- oppure ogni attributo in $Y$ è contenuto in _almeno_ una chiave $K$ di $r$

##### Terza forma normale (Definizione)
_sia_
- $R \langle T,F\rangle$ uno [[Modello Relazionale|schema relazionale]]
$R$ è in _terza forma normale_ (3NF) 
	_se e solo se_ 
$\forall X \to A \in F^+$ se $X$ è [[Modello relazionale - chiave|superchiave]] o se $A$ è attributo primo
 

**Vantaggi e svantaggi**
CONTRO
- la 3NF è _meno restrittiva_ della BCNF:
	- Tollera alcune ridondanze ed anomalie sui dati
		- Es. Per ogni occorrenza di un dirigente viene ripetuta la sua sede
	- Certifica meno la qualità dello schema ottenuto
    
PRO:
- La 3NF è _sempre ottenibile_, qualsiasi sia lo schema di partenza:
    - Mediante l’algoritmo di normalizzazione


**teorema**: $R<T,F>$ è in 3NF se per ogni $X \rightarrow A \in F$ non banale, allora $X$ è una superchiave oppure $A$ è primo.

### Algoritmo di sintesi: Versione Base

_Input_: Un insieme $R$ di attributi ed un insieme $F$ di dipendenze su $R$.

_Output_: Una decomposizione $\rho = \{ S_o \}_{i = 1..n}$ di $R$ tale che preservi i dati e dipendenze e ogni $S_i$ sia 3NF rispetto alle proiezioni di $F$ su $S_i$.

1. Trova una copertura canonica $G$ di $F$ e poni $\rho = \{ \}$
2. Sostituisci in $G$ ogni insieme $X \rightarrow A_1, ..., X \rightarrow A_h$ di dipendenze con lo stesso determinante con la dipendenza $X \rightarrow A_1 ... A_h$
3. Per ogni dipendenza $X \rightarrow Y$ in $G$, metti uno schema con attributi $XY$ in $\rho$
4. Elimina ogni schema di $\rho$ contenuto in un altro schema di $\rho$
5. Se la decomposizione _non_ contiene alcuno schema i cui attributi costituiscono una superchiave per $R$, aggiungi ad essa lo schema con attributi $W$, con $W$ una chiave di $R$.



La _[[Complessità|complessità]]_ del algoritmo dipende da quella del calcolo della _[[Copertura|copertura canonica]]_ pari a $O(a^2p^2)$


##### Teorema
_Sia_ $R\langle T,F\rangle$ uno _[[Modello Relazionale|schema relazionale]]_
_allora_ l'_algoritmo di sintesi_ produce una _decomposizione_ $\rho=\{ S_i \}_{i=1,\dots,n}$ che preserva [[Decomposizione dei schemi|dati e dipendenze]]

###### _Dimostrazione_
L'_algoritmo_ produce una decomposizione perché tutti gli attribuiti di $T$ appartengono allo _schema generato_.
Se ci sono attributi che non partecipano a nessuna dipendenza questi fanno parte di ogni chiave di $R$, per ciò compaiono nella grazie al passo 5.

La _decomposizione_ preserva _le dipendenza_ perché per ogni dipendenza $X\to A_i \in G$ esiste uno schema che contiene $XA_i$. 
La _decomposizione_ preserva i dati poiché grazie al passo 5, soddisfa la condizione espressa dal [[Decomposizione dei schemi|teorema di mantenimento dei dati]].

##### Proposizione
il problema di decidere se uno _schema di relazione_ è in _3NF_ è [[Complessità|NP-Completo]] perché decidere se un attributo è [[Modello relazionale - chiave|attributo primo]] è un problema NP-completo
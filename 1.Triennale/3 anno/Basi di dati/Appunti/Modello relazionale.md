---
Subject: "[[Indice - Basi di dati]]"
tags:
  - BD
Creation: 2024-02-15
---
# Modello relazionale
Il modello relazionale è un [[Modelli dei dati|modello di dati]] per la modellazione dei dati per la progettazione di una base di dati, si basa sul concetto matematico di relazione e ha una naturale rappresentazione per mezzo di tabelle.

I meccanismi per la definizione di una base di dati con questo modello sono ___il tipo ennupla___ e ___la relazione___ :

- il ___tipo ennupla___ $T$, ossia un insieme di coppie (attributo, tipo primitivo).
	Un valore di tipo ennupla è un insieme di coppie (attributo, valore) dette _campi_ (corpo della tabella)
	- Se $T$ è un tipo ennupla allora $R(T)$ è lo schema della relazione $R$
	- Lo schema di una base di dati è un'insieme di schemi di relazione $R_i(T_i)$
- la ___relazione___ o ___istanza di uno schema R(T)___ ossia un insieme di ennuple dello stesso tipo

Importante per la comprensione è il concetto di [[Modello relazionale - chiave|chiave]]: 

Un insieme di attribuiti i cui valori determinano univocamente una ennupla di una relazione R è una ___[[Modello relazionale - chiave#Superchiave|SUPERCHIAVE]]___ per R.

Una superchiave tale che togliendo un qualunque attributo essa non sia più una superchiave per R è una ___[[Modello relazionale - chiave#Chiave|CHIAVE]]___ per R.

Tra le chiavi di R ne viene scelta una come ___CHIAVE PRIMARIA___ 
Le associazioni tra i dati sono rappresentate attraverso opportuni attributi chiamati ___CHIAVE ESTERNE___, che assumono come valori quelli della chiave primaria di un'altra relazione

## Relazione

In matematica una relazione è un sottoinsieme del prodotto cartesiano di due o più insiemi. Quindi:

Presi $D_1, ..., D_n$ ($n$ insiemi anche non distinti)

Preso il prodotto cartesiano $D_1 \times ... \times D_n$ (vale a dire l’insieme di tutte le $n$-uple ($d_1, ..., d_n$) tali che $d_1 \in D_1, ..., d_n \in D_n$

Definiamo _relazione matematica_ su $D_1, ..., D_n$ un sottoinsieme di $D_1 \times ... \times D_n$ dove $D_1, ..., D_n$ sono i _domini_ della relazione.![[15_relazione.png]]

Dato che una relazione è un insieme, pertanto:
- Non c’è ordinamento tra le $n$-uple
- Le $n$-uple sono distinte
- Ciascuna $n$-uple è ordinata: l’$i$-esimo valore proviene dall’$i$-esimo dominio  

Il modello relazionale è basato sui _valori_. Questo significa che i riferimenti fra dati in relazioni diverse sono rappresentati per mezzo di valori dei domini che compaiono nelle ennuple.

In ogni base di dati si distinguono:

- Lo **schema**, sostanzialmente invariante nel tempo, che ne descrive la struttura (aspetto intensionale):
    - Le intestazioni delle tabelle
- L’**istanza**, i valori attuali, che possono cambiare anche molto rapidamente (aspetto estensionale)
    - Il “corpo” di ciascuna tabella


> [!NOTE] Schema di relazione
> Lo schema di relazione $R : {T}$ è una coppia formata da un _nome di relazione_ $R$ e da un tipo di relazione ${T}$ definito come:
> - tipo primitivi : int, real, boolean, string
> - se $T_1,...,T_n$ sono tipi primitivi e $A_1, ..., A_n$ sono etichette distinte dette _attributi_, allora $(A_1:T_1, ..., A_n:T_n)$ è un tipo ennupla di _grado n_.
> 	Due tipi ennupla sono uguali se hanno uguale il grado, gli attributi e il tipo degli attributi con lo stesso nome.
> 	L'ordine degli attributi non è significativo
> - se T è un tipo ennupla, allora ${T}$ è un tipo _insieme di ennuple_ o _tipo relazione_
> 	Due tipi relazione sono uguali se hanno lo stesso tipo ennupla
> 	


Uno schema relazionale è costituito da un insieme di schemi di relazione $R_i:\{T_i\}$, $i=1,...,k$ e da un insieme di vincoli di integrità relativi a tali schemi.



> [!NOTE] Aspetto estensionale
> Una ennupla $t=(A_1 :=V_1,...,A_n:=V_n)$ di tipo $T=(A_1:T_1,...,A_n:T_n)$  è un insieme di coppie $(A_i,V_i)$ con $V_i$ di tipo $T_i$.
> 
> Due ennuple sono uguali se hanno lo stesso insieme di coppie $(A_i,V_i)$
> 
> Un'_istanza_ dello schema $R_i:\{T_i\}$ o _relazione_ è un'insieme finito di ennuple $\{t_1,t_2,...,t_k\}$, con $t_i$ di tipo $T_i$.
> 
> La _cardinalità_ di una relazione è il numero delle sue ennuple.
> 
> Un'istanza dello schema relazionale è formata da un'istanza di ciascuno dei suoi schemi di relazione
> 
> Se $T$ è un tipo ennupla e $(A_1, ... , A_n)$ sono attributi di tipo $T$ si dice che una relazione di tipo $\{T\}$ ha attributi $(A_1,...,A_n)$ 
	si usa la notazione $R:(A_1:T_1,...;A_n:T_n)$ abbreviata in $R(A_1,...,A_n)$ se non interessa il tipo degli attributi


In una tabella l'intestazione delle colonne indicano gli attributi e le righe rappresentano le ennuple.
 Una _tabella_ rappresenta una _relazione_ se:

- I valori di ogni colonna sono fra loro omogenei
- Le righe sono diverse fra loro
- Le intestazioni delle colonne sono diverse tra loro

Inoltre, in una tabella che rappresenta una relazione:

- L’ordinamento tra le righe è irrilevante
- L’ordinamento tra le colonne è irrilevante.



> [!NOTE] Tupla
> Una tupla $t$ su un insieme di attributi $T$ è una funzione che associa a ciascun attributo $A$ in $T$ un valore del dominio di $A$
> - $t[A]$ denota il valore della tupla $t$ sull'attributo $A\in T$
> - $t[X]$ denota i valori della tupla $t$ sugli attributi $X\in T$
> 
> Un'istanza di relazione su uno schema $R(X)$ è l'insieme r di tuple su $X$
> 
> Un'istanza di base di dati su uno schema $R=\{R_1(X_1), ..., R_k(X_k)\}$ è l'insieme delle relazioni $r=\{r_1,...,r_n\}$ con $r_i$ relazione su $R_i$



Il modello relazionale impone ai dati una struttura rigida:

- Le informazioni sono rappresentate per mezzo di ennuple
- Solo alcuni formati di ennuple sono ammessi, quelli che corrispondono agli schemi della relazione

Il valore nullo denota l’assenza di un valore nel dominio (e non è un valore del dominio. 
$t[A]$, per ogni attributo $A$, è un valore del dominio $dom(A)$ oppure il valore nullo NULL.


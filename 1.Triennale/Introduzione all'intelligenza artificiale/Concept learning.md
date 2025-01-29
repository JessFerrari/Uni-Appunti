APPRENDERE vuole dire migliorare con l’esperienza su un task definito T rispetto ad una misura di prestazioni P sulla base dell’esperienza E.

In base al tipo del target d si hanno 2 tipi diversi di apprendimento:

- CLASSIFICAZIONE : $f(x)$ restituisce la classe che assume essere corretta per x. $f(x)$ è una funzione che lavora su valori discreti
- REGRESSIONE : $f(x)$ è una funzione a valori reali $(\R\ o \ \R^k)$

Fare CONCEPT LEARNING vuol dire inferire una funzione booleana basandosi su esempi positivi e negativi. Permette quindi di poter esprimere dei concetti.

> Dato un esempio <x, c(x)> in D (dove D è il training set)

$h:X\rightarrow \{0,1\}$ è SODDISFANCENTE per x se $h(x)=1$

L’ipotesi $h$ è CONSISTENTE con: - un esempio <x, c(x)> se $h(x)=c(x)$ - l’intero training set D se $h(x)=c(x)$ per ogni esempio di training del training set

In questo modo la soluzione del problema è UNICA e non si può definire qual è quella giusta finché non si provano tutte, ossia fino a quando non si completa un’intera lookup table con tutte le possibili opzioni di booleani.

Se si hanno $n$ parametri si avranno $2^n$ istanze e quindi $2^{2^n}$ possibili funzioni booleane.

In questo modo lo spazio delle ipotesi è troppo grande e per fare una buona ricerca bisogna considerare uno spazio ristretto usando un BIAS DI LINGUAGGIO.

Questo si può fare in due diversi modi

- REGOLE CONGIUNTIVE
- [Linear models](https://www.notion.so/Linear-models-a35e7eee88434421970d5ab479bb7649?pvs=21)

## REGOLE CONGIUNTIVE

Lo spazio delle ipotesi, presa la look up table, si riduce alle al numero delle regole congiuntive semplici, ossia di soli and : $2^n$.

Se si considerano anche i letterali negativi lo spazio delle ipotesi ha cardinalità $3^n+1$.

Le ipotesi si rappresentano come CONGIUNZIONI di vincoli sugli attributi.

I VINCOLI posso assumere 3 tipi di valori:

- Singolo valore
- Non importa il valore
- Nessun valore ammesso

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62929855-592a-4089-8f8e-93bf920d1062/Untitled.png)

Nella figura soprastante il target è definito da 6 ATTRIBUTI e ogni esempio è composto dai valori dati a tali attributi. Gli esempi sono positivi se il target è positivo.

Un’ipotesi $h$ definita su questi esempi è definita dall’insieme di valori che renderebbe un’istanza positiva.

Dati gli esempi sopra viene definita $h:$ <sunny, warm, ?, strong, ?, ?>

Un’ipotesi è specifica se tutti gli attributi non ammettono valore

$<\empty, \empty, \empty,\empty, \empty, \empty>$

Un’ipotesi è generale se tutti i gli attributi hanno un valore indefinito

$<?,?,?,?,?,?>$

> Date delle ISTANZE X (dove $x\in X$ è una singola istanza), una TARGET FUNCTION, uno spazio delle ipotesi $H$ e degli esempi di training positivi e negativi

Trovare un ipotesi $h\in H$ tale che $h(x)=c(x)$ per ogni $x\in X$

Apprendere vuol dire fare una ricerca nello spazio delle ipotesi $H$

❓ Se un’ipotesi è consistente con l’intero training set vale anche che $h(x)=c(x) \ \forall\ x\in X$ ?

## Strutturare la ricerca in modo efficiente

Dato che lo spazio delle ipotesi è generalmente molto ampio si deve ristrutturare in modo efficiente:

Dati 6 attributi, di cui uno può assumere 3 valori e gli altri cinque 2, si hanno:

- 3_2_2_2_2*2 = 96 istanze distinte
- $2^{96}$ concetti
- 5_4_4_4_4*4 = 5120 ipotesi SINTATTICAMENTE distinte (contando per ogni attributo anche $\empty$ e $?$)
- 4_3_3_3_3*3+1 = 973 ipotesi SEMANTICAMENTE distinte (considerando una sola ipotesi con tutti $\empty$ )

> Prese due ipotesi $h_1$ e $h_2$ tale che $h_2$ imponga meno vincoli rispetto ad $h_1$ (ossia $h_2$ è più generale, e quindi classifica più istanza positive rispetto ad $h_1$)

$h_2$ è più generale o uguale ad $h_1$ ($h_2\geq h_1$) $\iff$ $\forall \ x\in X : [(h_1(x)=1)\Rightarrow(h_2(x)=1)]$

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb60df72-3833-4723-8b4e-18a31f466315/Untitled.png)

## ALGORITMO FIND-S

Sfrutta l’ordine parziale per cercare l’ipotesi h senza enumerare tutte le ipotesi di H.

1. Si inizializza h come l’ipotesi più specifica in H (tutti $\empty$)
2. Per ogni istanza di training positiva
    - Per ogni attributo $a_i\in h$
        - Se $a_i\in h$ è soddisfatta da x non fare nulla
        - else sostituire $a_i$ in h con il prossimo valore più generale che soddisfa x
3. Restituire l’ipotesi h

Nota: se l’istanza di training è negativa non si fa nulla perché già corretto

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ad6fe019-1e6a-4206-836c-30c61759c5d4/Untitled.png)

inserisco l’esempio delle slide perché non ho voglia di riscriverlo

### PROPRIETÀ DI FIND-S

- Lo spazio delle ipotesi è descritto da congiunzioni di attributi (limitazione forte)
- Restituisce l’ipotesi più specifica e consistente con gli esempi di training positivi
- l’ipotesi restituita è consistente anche con gli esempi negativi presenti in H in quanto $c\geq h$
- Non è detto che l’ipotesi converga alla funzione target, è solo giusta per gli esempi forniti
- Non tollera il rumore

Perché scegliere l’ipotesi più specifica se ci possono essere multiple ipotesi massimali specifiche?

Per questo motivo si usa il VERSION SPACE

### VERSION SPACE

L’idea è quella di dare come output una descrizione dell’insieme delle ipotesi consistenti con il training set D e non una sola sola. Non si enumera niente.

> Il version space $VS_{H,D}$, rispetto ad uno spazio delle ipotesi H e al training set D, è il sottoinsieme delle ipotesi consistenti con tutti gli esempi di training

$VS_{H,D}=\{h\in H|Consistent(h,D)\}$

## ALGORITMO LIST-THEN ELIMINATE

1. Si definisce il version space come lista contenente tutte le ipotesi di H
2. Per ogni esempio di training <x, c(x)>
    - rimuovere dal version space tutte le ipotesi che non sono consistenti con tale esempio [$h(x)\neq c(x)$]
3. Restituire il version space finale

Il Version Space presenta 2 limiti:

- G, che rappresenta l’ipotesi più generale al suo interno, o meglio, l’insieme delle funzioni massimalmente generali
- S, che rappresenta l’ipotesi più specifica al suo interno, o meglio, l’insieme delle funzioni massimalmente specifiche

$VS_{H,D}=\{h\in H|(\exists s\in S\ \&\& \ \exists g\in G ):g\geq h\geq s\}$

## ALGORITMO CANDIDATE ELIMINATE

G = massima generalizzazione

S = massima specializzazione

Per ogni esempio di training d = <x, c(x)>

Se d è un esempio positivo

- Rimuovere da G ogni ipotesi che non è consistente con d
    
- Per ogni ipotesi $s\in S$ che non è consistente con d
    
    [GENERALIZZARE S]
    
    - rimuovere s da S
    - aggiungere in S ogni generalizzazione minimale h tale che
        - h è consistente con d
        - i membri di G siano più generali rispetto ad h
    - rimuovere da S ogni ipotesi che sia più generale delle altre ipotesi in S

Altrimenti se d è un esempio negativo

- Rimuovere da S ogni ipotesi che non è consistente con d
    
- Per ogni ipotesi $g\in G$ che non è consistente con d
    
    [SPECIALIZZARE G]
    
    - rimuovere g da G
    - aggiungere in G ogni specializzazione minimale h tale che
        - h è consistente con d
        - i membri di S siano più specifici rispetto ad h
    - rimuovere da G ogni ipotesi che sia più specifica delle altre ipotesi in G

### ESEMPIO

$G:<?,?,?,?,?,?>\\ S:<\empty,\empty,\empty,\empty,\empty,\empty>\\$

$x_1=<sunny,\ warm,\ normal,\ strong,\ warm,\ same>+$

[si generalizza S dato che è positivo]

si aggiungono tutti i valori degli attributi a S

$G:<?,?,?,?,?,?>\\ S:<sunny,\ warm,\ normal,\ strong,\ warm,\ same>\\$

$x_2:<sunny,\ warm,\ high,\ strong,\ warm,\ same>+$

[si generalizza S dato che è positivo]

il valore del terzo attributo è diverso e allora si mette ?

$G:<?,?,?,?,?,?>\\ S:<sunny,\ warm,\ ?,\ strong,\ warm,\ same>\\ \\$

$x_3:<rainy,\ cold,\ high,\ strong,\ warm,\ change> -$

[si rende più specifica G dato che è negativo]

$G:\{<sunny,?,?,?,?,?>, <?,warm,\ ?,?,?,?>, <?,?,?,?,?,same>\}\\ S:<sunny,\ warm,\ ?,\ strong,\ warm,\ same>\\ \\$

$x_4:<sunny,\ warm,\ high,\ strong,\ cool,\ change>+$

[Si deve generalizzare S e inoltre non non è consistente con G]

$G:\{<sunny,?,?,?,?,?>, <?,warm,\ ?,?,?,?>\}\\ S:<sunny,\ warm,\ ?,\ strong,\ ?,\ ?>\\ \\$

### Come classificare nuovi dati

Se le nelle nuove istanze gli attributi concordano o sono totalmente in discordo con il Version Space allora vengono facilmente classificate in positivo o negativo.

Se invece è a metà o comunque non completamente aderente viene rigettata.

# BIAS INDUTTIVO

Lo spazio delle ipotesi H non può rappresentare le regole disgiuntive (con gli OR).

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5561414c-eebe-4057-9577-5f0a8fa37d74/Untitled.png)

In questo caso S è vuoto perché è arrivato il terzo valore per il primo attributo.

Se fosse possibile usare l’or si renderebbe ambigua la classificazione

ASSUNZIONE: Lo spazio delle ipotesi H contiene la funzione target c. Ovvero la funzione c può essere descritta con una CONGIUNZIONE di letterali.

> Un sistema di apprendimento sprovvisto di un bias non è capace di generalizzare.

Dimostrazione:

Per ogni istanza non ancora osservata, questa viene classificata come positiva da metà delle ipotesi nel Version Space e negativa dall’altra metà, facendo avvenire quindi una rejection. Per ogni istanza consistente con il test $x_i$ esiste un’ipotesi h’ identica ad h eccetto per $x_i$, $h(x_i)\neq h'(x_i)$

> Un sistema di apprendimento che non fa assunzioni a priori riguardanti l’identità della funzione target non ha basi razionali per classificare ogni nuova istanza

Qualsiasi sistema di ML che funziona bene, e che quindi è in grado di generalizzare, possiede un BIAS.

DEFINIZIONE BIAS INDUTTIVO:

> Considerando delle istanze X, una target function c, degli esempi di training $D_c=\{<x,c(x)\}$ e un algoritmo di apprendimento $L(x_i, D_c)$ che classifica l’istanza $x_i$ dovo aver istruito L su $D_c$

Il BIAS INDUTTIVO di L è ogni set minimale di asserzioni B tali che per ogni funzione target c ed il corrispondente training set $D_c$ si ha che $(\forall x_i \in X)[B\land D_c\land x_i]\vdash L(x_i, D_c)$

La congiunzione è conseguenza logica dell’algoritmo
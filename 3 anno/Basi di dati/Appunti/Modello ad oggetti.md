---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modelli dei dati]]"
tags:
  - BD
Creation: 2024-02-13
Esempi: "[[Esempi modello ad oggetti]]"
Esercizi: "[[Esercizi modello ad oggetti]]"
---
 Il modello ad oggetti è un [[Modelli dei dati|modello]] con cui si modella la [[Conoscenza concreta|conoscenza concreta]] e quella [[Conoscenza astratta|astratta]]

## Rappresentazione della [[Conoscenza concreta|conoscenza concreta]]

Per rappresentare la conoscenza concreta con il modello ad oggetti si usano le nozioni di : oggetto, tipo oggetto, classe, gerarchia tra tipi e gerarchia tra classi.


#### Oggetto
 
> [!NOTE] Oggetto
> Un oggetto è un entità software con _stato_, _comportamento_ e _identità_ che modella un' [[Conoscenza concreta|entità]] dell'universo del discorso.
> 
> Lo ___stato___ è composto da un insieme di _campi_ che possono assumere qualunque valore modelli le [[Conoscenza concreta|proprietà delle entità]].
> 
> Il ___comportamento___ è costituito da procedure locali chiamate ___metodi___ che modellano le operazioni di base di un oggetto. Le operazioni applicabili ad un oggetto sono dette _messaggi a cui l'oggetto risponde_. Quando vengono utilizzati lo stato cambia.
> 
> L'___interfaccia___ di un'oggetto specifica l'insieme dei messaggi a cui esso può rispondere.
> 
> L'___identità___ di un oggetto è una caratteristica che viene associata ad un oggetto alla sua creazione e che non può cambiare. Oggetti diversi hanno identità diverse. 


#### Tipo oggetto
	In UML è la classe

> [!NOTE] Tipo oggetto
> Un tipo oggetto definisce i possibili valori e le operazioni ad essi applicabili.
> Riguarda la struttura delle entità omogenee.
> 
> Ogni oggetto è un valore di un tipo. Ad ogni tipo sono associati degli operatori per costruire oggetti di quel tipo (costruttori) e l'interfaccia dell'oggetto stesso.
> 
> L'interfaccia di tipo oggetto specifica i componenti dello stato che sono accessibili dall'esterno ed il loro tipo

> Esempio di rappresentazione di tipo oggetto:
> ![[Pasted image 20240213114828.png]]

Per i tipi si usano quelli primitivi (int, real, bool, date e string) e non, come:
- _tipo record_, etichetta valore $[A_1:T_1; ... ; A_n:T_n]$
- _tipo enumerazione_ 
- _tipo sequenza_

#### Classe


> [!NOTE] Classe
> Una ___classe___ è un insieme di oggetti dello stesso tipo, modificabile con operatori per includere o estrarre elementi dall'insieme, al quale sono associabili [[Conoscenza astratta|vincoli d'integrità]].
	Non c'è una rappresentazione specifica e si assume che gli unici oggetti che si modellano fanno parte di classi ed il nome del TIPO OGGETTO sia il solito della classe

Una classe modella una [[Conoscenza concreta|collezione]].

###### Rappresentazione delle associazioni
- Associazioni binarie senza proprietà
	Un’associazione fra due collezioni $C_1$ e $C _2$ è una relazione binaria fra $C _1$ e $C_2$ 
	![[Pasted image 20240213134524.png]] 
- Associazione binaria con proprietà
	![[Pasted image 20240213134739.png]]
	Può essere modellata rendendo la proprietà un entità facendola così diventare una binaria 
	![[Pasted image 20240213134846.png]]
- Associazione ricorsiva
	Le associazioni ricorsive sono relazioni binarie fra gli elementi di una stessa collezione
	![[Pasted image 20240213135010.png]]
- Associazioni n-arie
	Associazioni che riguardano più entità
	![[Pasted image 20240213135116.png]]

[[Esempi associazioni]]
## Gerarchie

La relazione di sottotipo è una relazione di ordinamento parziale sull’insieme dei tipi tale che un valore che appartiene al sottotipo può essere utilizzato in tutti i contesti in cui è previsto un valore del supertipo.

Due importanti caratteristiche delle gerarchie:

- [[#^21e488|Ereditarietà]] delle proprietà
- Gli elementi di una sottoclasse sono un sottoinsieme degli elementi della superclasse.

#### Gerarchia tra tipi oggetto

Fra i tipi oggetto è definita una relazione di sottotipo, con le seguenti proprietà:

- È asimmetrica, riflessiva e transitiva (relazione di ordine parziale).
- E $T$ è sottotipo di $T'$, allora gli elementi di $T$ possono essere usati in ogni contesto in cui possano apparire valori di tipo $T'$ (sostitutività). In particolare:
    - Gli elementi di $T$ hanno tutte le proprietà degli elementi di $T'$
    - Per ogni proprietà $p$ in $T'$, il suo tipo in $T$ è un sottotipo del suo tipo in $T'$.
- La gerarchia può essere semplice (unico super tipo) o multipla (più super tipi)

#### Ereditarietà
^21e488

L’ereditarietà permette di definire:
- un tipo di oggetto a partire da un altro
- l’implementazione di un tipo oggetto a partire da un’altra implementazione

Normalmente l’ereditarietà tra tipi si usa solo per definire sottotipi, e l’ereditarietà tra implementazioni per definire implementazioni di sottotipi (ereditarietà stretta) in questo caso:
- gli attributi possono essere solo aggiunti
- gli attributi possono essere ridefiniti solo specializzandone il tipo
![[11_ereditarietà.png]]

#### Gerarchia fra classi
Fra le classi può essere definita una relazione di sottoclasse, detta anche **sottoinsieme**, con le seguenti proprietà:

- È asimmetrica, riflessiva, transitiva
- Se $C$ è sottoclasse di $C'$ allora il tipo degli elementi di $C$ è sottotipo del tipo degli elementi di $C'$ (**vincolo intensionale**)
- Se $C$ è sottoclasse di $C'$, allora gli elementi di $C$ sono un sottoinsieme degli elementi di $C'$ (**vincolo estensionale**)

Si hanno 5 tipi di gerarchia tra classi:

- _inclusione_
![[12-0_ereditarietà.png]]
- _disgiunzione_ : ogni coppia di sottoclassi in questo insieme è disgiunta, ovvero è priva di elementi comuni (sottoclassi disgiunte).
![[12-1_ereditarietà.png]]

- _copertura_ : l'unione degli elementi delle sottoclassi coincide con l’insieme degli elementi della superclasse (sottoclassi copertura).
![[12-2_ereditarietà.png]]
- _partizione_ : Unione e disgiunzione contemporaneamente
 

- _scorrelate_ : Le sottoclassi scorrelate non richiedono né il vincolo di copertura né quello di disgiunzione, si possono rappresentare anche nel seguente modo:![[12-4_ereditarietà.png]]

#### Ereditarietà multipla
Un tipo può essere definito per ereditarietà a partire da un unico supertipo (ereditarietà singola) o da più supertipi (ereditarietà multipla).

L’ereditarietà multipla è molto utile ma può creare problemi quando lo stesso attributo viene ereditato, con tipi diversi da più tipi di antenato.


## Rappresentazione [[Conoscenza astratta|conoscenza astratta]]

Si devono modellare anche i vincoli d'integrità. Questi possono essere descritti in modo dichiarativo, con formule del calcolo dei predicati o mediate controlli da eseguire sulle operazioni.

![[14_vintegrità.png]]

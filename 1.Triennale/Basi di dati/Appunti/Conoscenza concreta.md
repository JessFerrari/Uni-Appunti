---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Aspetto ontologico]]"
tags:
  - BD
Creation: 2024-02-10
---
La conoscenza concreta riguarda i fatti che si vogliono rappresentare.
La realtà è composta da ___entità___ che hanno ___tipo___ e ___proprietà___. 
Le entità sono classificabili all'interno di ___collezioni di entità omogenee___ ed esistono delle ___istanze di associazioni___ tra queste entità.

La __struttura della conoscenza concreta__ riguarda la conoscenza dell'esistenza di collezioni di entità e l'esistenza di associazioni tra le collezioni.
Riguarda _quali entità esistono_, il _tipo_ di queste entità e le loro _proprietà_, quali _entità_ appartengono ad ogni specifica _collezione_ (__estensione della collezione__) e quali istanze appartengono ad una specifica associazione (__estensione dell'associazione__)

La conoscenza concreta è considerata lo _stato_ dell'universo del discorso che si evolve nel tempo.

> [!note] Entità
> Un'entità è un qualcosa di concreto o astratto di cui interessa rappresentare alcuni fatti.

^6bed08

	Sono ad esempio oggetti, sia concreti che astratti, ed eventi. Ad esempio una persona, una descrizione bibliografica,  un prestito
 Delle entità interessano la _proprietà_


> [!NOTE] Proprietà
> Una proprietà è una fatto che descrive una qualità di un'entità.
> Non coincide con l'insieme dei valori che può assumere
	Esempi di proprietà sono il nome di una persona
I  valori di una proprietà cambiano nel tempo e due entità possono avere le stesse proprietà con gli stessi valori pur rimanendo due entità distinte.
Il concetto di proprietà è collegato al concetto di _tipo_
Ad ogni proprietà è associato un ___dominio___ di valore che può assumere.

Una ___proprietà___ può essere: 
- atomica o strutturata, 
- univoca o multivalore 
- obbligatoria o opzionale
- costante o variabile
- calcolata o non calcolata


> [!NOTE] Tipo
> Un tipo è una descrizione astratta di ciò che accomuna un insieme di entità omogenee, esistenti o possibili
	Esempio : Persona è il tipo di Mario
I tipi possono essere visti come collezioni infinite di possibili entità. Ai tipi sono associate le proprietà che interessano le entità che appartengono a tele tipo e le caratteristiche di tali proprietà



> [!NOTE] Collezione
> Una collezione è un'insieme di entità omogenee variabili nel tempo, interessanti nell'universo del discorso
> L'insieme degli elementi di una collezione in un determinato momento è detto ___estensione della collezione___
> 
> Tra le collezioni si modellano ___GERARCHIE DI SPECIALIZZAZIONE___ o ___DI GENERALIZZAZIONE___ 
> Se una collezione $C_{sub}$ è una specializzazione della gerarchia $C_{sup}$, allora $C_{sub}$ è sottoinsieme di $C_{sup}$
^244f59



> [!NOTE] Istanza di associazione
> Un’istanza di associazione è un fatto che correla due o più entità, stabilendo un legame logico fra di loro.
	Esempio: lo studente x ha preso in prestito il libro y
Un'istanza di associazione può avere delle proprietà che non caratterizzano nessuna delle due entità in gioco



> [!NOTE] Associazione
> Un’associazione tra le collezioni C 1 , . . . , C n è un insieme di istanze di associazione tra elementi di C 1 , . . . , C n , che varia in generale nel tempo. 
> Il prodotto cartesiano delle estensioni di C 1 , . . . , C n è detto il dominio dell’associazione
Il dominio è un insieme finito che dipende dallo stato dell'universo del discorso e varia nel tempo
^2ab461



> [!NOTE] Molteplicità
> La molteplicità di un’associazione fra due entità X ed Y riguarda il numero massimo di elementi di Y che possono trovarsi in relazione con un elemento di X e viceversa. 
> Si dice che l’associazione è _univoca_ da X ad Y se ogni elemento di X può essere in relazione con al più un elemento di Y. 
> Se non esiste tale vincolo si dice che l’associazione è _multivalore_ da X ad Y. 
> Allo stesso modo si definisce il vincolo di univocità da Y ad X



> [!NOTE] Cardinalità
> La cardinalità di un’[[#^2ab461|associazione]] fra X ed Y descrive contemporaneamente la __molteplicità dell’associazione e della sua inversa__. 
> Si dice che la cardinalità è  uno a molti (1 : N) se l’associazione è multivalore da X ad Y ed univoca da Y ad X. 
> La cardinalità è molti ad uno (N : 1) se l’associazione è univoca da X ad Y e multivalore da Y ad X. 
> La cardinalità è molti a molti (N : M) se l’associazione è multivalore in entrambe le direzioni, ed è uno ad uno (1 : 1) se l’associazione è univoca in entrambe le direzioni




> [!NOTE] Totalità
> L a totalità di un'[[#^2ab461|associazione]] fra due [[#^244f59|collezioni]] X e Y riguarda il numero minimo di elementi di Y che sono associati ad ogni elemento di X.
> Se almeno un'[[#^6bed08|entità]] di Y deve essere associata ad ogni entità di X si dice che l'associazione è _totale_ su X. Viceversa sostituendo X e Y.
> Quando tale vincolo non esiste si dice che è _parziale_


![[10_associazioni 1.png]]


Ad ogni entità del dominio corrisponde un _**oggetto**_ del modello ossia un’entità software con stato, comportamento e identità che modella un’entità dell’universo.

Lo _**stato**_ è modellato da un insieme di costanti o variabili con valori di qualsiasi complessità.

Il _**comportamento**_ è un insieme di procedure locali chiamate metodi, che modellano le operazioni di base che riguardano l’oggetto e le proprietà derivabili da altre.

Un oggetto può rispondere a dei messaggi, restituendo valori memorizzati nello stato o calcolati con una procedura locale.


[[Esempi associazioni]]
---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello relazionale]]"
Esempi: "[[Esempi traduzione]]"
Esercizi: "[[Esercizi traduzione]]"
tags:
  - BD
Creation: 2024-02-17
---
Trasformare uno schema vuol dire “tradurre” lo [[Progettazione - progettazione concettuale|schema concettuale]] in uno schema logico relazionale che rappresenti gli stessi dati in maniera corretta ed efficiente.

La trasformazione di uno schema ad oggetti in uno schema relaziona le avviene eseguendo i seguenti passi:

1. Rappresentazioni delle associazioni uno ad uno ed uno a molti
2. Rappresentazione delle associazioni molti a molti o non binarie
3. Rappresentazione delle gerarchie di inclusione
4. Identificazione delle chiavi primarie
5. Rappresentazione degli attributi multivalore
6. Appiattimento degli attributi composti.

L'obiettivo è quello di rappresentare le stesse informazioni _minimizzando la ridondanza_.
Lo schema prodotto si vuole sia comprensibile per facilitare la scrittura e la manutenzione delle applicazioni

Non si tratta di una pura traduzione in quanto alcuni costrutti non sono traducibili e bisogna tenere conto delle prestazioni.

# Associazioni uno a molti
Le associazioni uno a molti si rappresentano aggiungendo agli attributi della relazione rispetto a cui l'associazione è univoca una [[Modello relazionale - chiave|chiave esterna]] che riferisce l'altra relazione

# Associazioni uno a uno
Le associazioni uno a uno si rappresentano aggiungendo la chiave esterna ad una qualunque delle due relazioni che riferisce l'altra relazione preferendo, se esiste, quella con il vincolo di totalità.


Se un'associazione ha degli attributi questi li metto nella relazione con la chiave esterna.

La direzione dell'associazione rappresentata dalla [[Modello relazionale - chiave|chiave esterna]] è detta ___la diretta___ dell'associazione 

##### Vincoli sulle associazione uno a molti e uno a uno
- univocità della diretta
- totalità della diretta, che si rappresenta imponendo un vincolo $not \ null$ sulla chiave esterna
- univocità dell'inversa che si rappresenta con un vincolo di chiave sulla chiave esterna
![[Pasted image 20240218225118.png]]
---
## Associazioni molti a molti

Un'associazione molti a molti si rappresenta aggiungendo allo schema una nuova relazione che contiene due chiavi esterne che si riferiscono alle due relazioni coinvolte.
La chiave primaria di questa relazione è costituita dall'insieme di tutti i suoi attributi
![[Pasted image 20240218225215.png]]

---
## Rappresentazione delle gerarchie

Il modello relazionale non può rappresentare direttamente le gerarchie, bisogna eliminarle sostituendole con classi e relazioni:

- ___Accorpamento delle figlie della gerarchia nel genitore (relazione unica)___
	Se $A_0$ è la classe genitore di $A_1$ ed $A_2$, le classi $A_1$ e $A_2$ vengono eliminate ed accorpate ad $A_0$.
	Ad $A_0$ viene aggiunto un attributo (**discriminatore**) che indica da quale delle due classi figlie deriva una certa istanza, e gli attributi di $A_1$ ed $A_2$ vengono assorbiti nella classe genitore, e assumono valore nullo sulle istanze provenienti dall’altra classe.
	Infine, una relazione relativa a solo una delle classi figlie viene acquisita dalla classe genitore e avrà comunque cardinalità minima uguale a 0, in quanto gli elementi dell’altra classe non contribuiscono alla relazione.
	![[Pasted image 20240219024047.png]]
	Ad esempio:
	![[Pasted image 20240219023946.png]]
	Quando non è conveniente:
	- quando le figlie hanno tanti attributi
	- quando per le operazioni non bisogna distinguere tra le sottoclassi
	- per le associazioni tradotte con le chiavi esterne bisogna fare controlli a livello del destinatario.

- ___Accorpamento del genitore della gerarchia nelle figlie (partizione orizzontale)___
	La classe genitore $A_0$ viene eliminata e le classi figlie $A_1$ ed $A_2$ ereditano le proprietà (attributi, identificatore e relazioni) dalla classe genitore.
	Il partizionamento orizzontale.
	![[Pasted image 20240219025424.png]]
	La chiave primaria delle due relazioni è la stessa ed è quella che avrebbe avuto la relazione del padre.
	**Problemi:**
	Se la gerarchia non è una copertura sconveniente per le operazioni.
	Se la gerarchia non è disgiunta si ha ridondanza dei dati, perché i dati vanno copiati in entrambe le tabelle e si hanno problemi anche con le associazioni del padre perché non posso essere rappresentate.
	
	Conveniente se le operazioni riguardano solo le figlie e non il padre
 
- ___Sostituzione della gerarchia con relazioni (partizionamento verticale)___
	La gerarchia si trasforma in tre relazioni, due che rappresentano le classi figlie e una che rappresenta la classe padre.
	In questo caso non si ha un trasferimento di attributi o di associazioni e le classi figlie $A_1$ ed $A_2$ sono identificate esternamente dalla classe genitore $A_0$.
	Nello schema ottenuto vanno però aggiunti dei vincoli: ogni occorrenza di $A_0$
	non può partecipare contemporaneamente alle due associazioni, e se la gerarchia è totale, deve partecipare ad almeno una delle due.
	![[Pasted image 20240219030440.png]]
	
	Esempio:
	![[Pasted image 20240219030413.png]]
	Ottimale per le chiavi esterne,  per le gerarchie che non sono copertura
---
## Attributi multivalore

Gli attributi multivalore sono quelli per cui possiamo avere uno o più valori allo stesso attributo (tecnicamente attributi diversi).

Per rappresentare questo possiamo creare una nuova classe che conterrà la lista dei valori degli attributi.
![[Pasted image 20240219030736.png]]![[Pasted image 20240219031105.png]]
---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello ad oggetti]]"
tags:
  - BD
  - esempio
  - "#todo"
Creation: 2024-02-13
---

> [!Example] Biblioteca universitaria
> Di una biblioteca universitaria si vogliano rappresentare i seguenti fatti: 
> 
> 1. Le Descrizioni Bibliografiche dei libri a volume unico, sia già disponibili che quelli ordinati ma non ancora consegnati alla biblioteca. Delle descrizioni bibliografiche interessano: Codice ISBN (International Standard Book Number) che le identifica, titolo del libro, autori, editore, anno di pubblicazione e termini che le descrivono.
> 
> 2. I termini sono una rappresentazione di un thesaurus, o parole chiave, usati per descrivere (indicizzare) le descrizioni bibliografiche. Fra i termini interessano due particolari associazioni, fra le diverse possibili: 
> 	1. Preferenza ( E'SinonimoDi), che associa a termini non-standard il termine standard che viene usato da esperti del settore. Ad esempio: 
> 		* Calcolatore Standard Computer; 
> 		* Computer Sinonimi Calcolatore, Workstation, Server; 
> 	2. Gerarchia (Specializza), per sottolineare le relazioni di specificità o generalità fra due termini. Ad esempio:
> 		* Felino TerminiPiùSpecifici Gatto, Leone, Tigre; 
> 		* Gatto TerminePiùGenerale Felino; 
> 		
> 3. I libri, disponibili in una o più copie ognuna identificata da un Codice, una stringa con la loro collocazione e numero. 
> 
> 4. Gli autori dei libri, dei quali interessano: Codice Fiscale, che li identifica, nome e cognome, nazionalità e anno di nascita. 
> 
> 5. Gli utenti della biblioteca. Quando un utente prende in prestito un libro, interessano le seguenti informazioni (se non già presenti): Codice Fiscale, nome e cognome, indirizzo e numeri dei telefoni. Un utente può avere più libri in prestito. 
> 
> 6. I prestiti dei libri, dei quali interessano, fino a quando il libro non è restituito, le date del prestito e della restituzione prevista
> 
> si definiscono le seguenti sottoclassi partizione: 
> - della classe Utenti le sottoclassi Studenti, dei quali interessa anche la matricola, e Docenti, dei quali interessa anche il numero del telefono dell’ufficio; 
> - della classe Libri le sottoclassi Prestabili e Consultabili che possono essere presi in prestito per un numero prefissato di giorni solo dagli utenti che sono docenti; 
> - della classe Prestiti le sottoclassi Regolari, dei prestiti di libri prestabili, e InConsultazione dei prestiti di libri consultabili 

![[Pasted image 20240213135953.png]]


![[Pasted image 20240215024329.png]]

### con diagramma [[Modello entità-relazione|entità relazione]]
![[Pasted image 20240215031551.png]]
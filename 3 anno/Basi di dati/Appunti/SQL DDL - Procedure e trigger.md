---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[SQL]]"
tags:
  - BD
Creation: 2024-02-23
---
![[Pasted image 20240224025226.png]]
Un trigger definisce un’azione che il database deve attivare automaticamente quando si verifica (nel database) un determinato evento

Possono essere utilizzati: 
- per migliorare l’integrità referenziale dichiarativa 
- per imporre regole complesse legate all’attività del database
- per effettuare revisioni sulle modifiche dei dati

L’esecuzione dei trigger è quindi trasparente all’utente. 
I trigger vengono eseguiti automaticamente dal database quando specifici tipi di comandi (Eventi) di manipolazione dei dati vengono eseguiti su specifiche tabelle.

Tali comandi comprendono i comandi DML insert, update e delete, ma gli ultimi DBMS prevedono anche trigger su istruzioni DDL come Create View ecc. 

Anche gli aggiornamenti di specifiche colonne possono essere utilizzati come trigger di eventi.

## trigger livello di riga

I trigger a livello di riga vengono eseguiti una volta per ciascuna riga modificata in una transazione; vengono spesso utilizzati in applicazioni di revisione dei dati e si rivelano utili per operazioni di audit dei dati e per mantenere sincronizzati i dati distribuiti. 
Per creare un trigger a livello di riga occorre specificare la clausola FOR EACH ROW nell’istruzione create trigger.

## trigger a livello di istruzione

I trigger a livello di istruzione vengono eseguiti una sola volta per ciascuna transazione, indipendentemente dal numero di righe che vengono modificate (quindi anche se, ad esempio, in una tabella vengono inserite 100 righe, il trigger verrà eseguito solo una volta). 
Vengono pertanto utilizzati per attività correlate ai dati;  vengono utilizzati di solito per imporre misure aggiuntive di sicurezza sui tipi di transazione che possono essere eseguiti su una tabella. 
E’ il tipo di trigger predefinito nel comando create trigger (ossia non occorre specificare che è un trigger al livello di istruzione).

### Struttura

I trigger si basano sul paradigma evento-condizione-azione (ECA). 

1. L’istruzione `Create Trigger` seguita dal nome assegnato al trigger 
2. Tipo di trigger, Before/After 
3. Evento che scatena il trigger Insert/Delete/Update 
4. `[For each row],` se si vuole specificare trigger al livello di riga (altrimenti nulla per trigger al livello di istruzione) 
5. Specificare a quale tabella si applica 
6. Condizione che si deve verificare perché il trigger sia eseguito 
7. Azione, definita dal codice da eseguire se si verifica la condizione
![[Pasted image 20240224025757.png]]

	![[Pasted image 20240224025812.png]]

## Tipi di trigger

BEFORE e AFTER: i trigger possono essere eseguiti prima o dopo l’utilizzo dei comandi insert, update e delete.
All’interno del trigger è possibile fare riferimento ai vecchi e nuovi valori coinvolti nella transazione. 

Occorre utilizzare la clausola `BEFORE/AFTER <tipo di evento> (insert, delete, update)` 

Se si tratta di un trigger BEFORE UPDATE per valori vecchi si intendono i valori che sono nella tabella e che si vogliono modificare e per nuovi quelli che si vogliono inserire al posto dei vecchi. 

Se si tratta di un trigger AFTER UPDATE per vecchi si intendono quelli che c’erano prima dell’update e per nuovi quelli presenti nella tabella alla fine della modifica

 Un trigger è attivo quando, in corrispondenza di certi eventi, modifica lo stato della base di dati. 
 
 Un trigger è passivo se serve a provocare il fallimento della transazione corrente sotto certe condizioni.
### `instead of`

INSTEAD OF si usa per specificare che cosa fare invece di eseguire le azioni che hanno attivato il trigger. 
Ad esempio, è possibile utilizzare un trigger INSTEAD OF per reindirizzare le INSERT in una tabella verso una tabella differente o per aggiornare con update più tabelle che siano parte di una vista. 
I trigger instead-of possono essere definiti su viste (relazionali od oggetto) e sono solo a livello di riga.

## Proprietà
La proprietà essenziale dei trigger è la terminazione 

## Utilità
- Trattare vincoli non esprimibili nello schema 
- Attivare automaticamente azioni sulla base di dati quando si verificano certe condizioni
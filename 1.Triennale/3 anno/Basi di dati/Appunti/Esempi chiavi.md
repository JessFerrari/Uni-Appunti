---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello relazionale - chiave]]"
tags:
  - BD
  - esempio
Creation: 2024-02-18
---
# Esempio 1

![[Pasted image 20240219002613.png]]
In questa tabella se si prendono gli attributi _Nome_, _Cognome_ e _Nascita_, si sta prendendo un'insieme di attributi che rappresentano una chiave se si imponesse il vincolo che nella base di dati non possono esistere persone con il solito nome e cognome e nati lo stesso giorno.
Imposto questo vincolo, questo insieme è superchiave e pure minimale in quanto sono necessari tutti e tre gli attributi per individuare la ennupla.

Se non imponessi il vincolo allora non sarebbe nemmeno superchiave in quanto possono esiste due ennuple in cui Nome, Cognome e Nascita hanno gli stessi valori.

Una superchiave che non è chiave, in quanto non minimale, può essere l'insieme di attributi Nome, Cognome e Matricola.
Questo perché le ennuple contengono per forza tutte una Matricola diversa e quindi contiene al suo interno un'altra superchiave.
Quindi se prendo solo l'attributo Matricola questo rappresenta una superchiave formata da un solo elemento e quindi anche minimale.

Nell'esempio, si ha che l'insieme di attributi {Cognome, Corso} formano una chiave, in quanto non ci sono ennuple uguali su tali attributi, ma non è sempre vero come vincolo.


# Esempio vincolo d'integrità referenziale
![[Screenshot 2024-02-19 005016.png]]
In questo modo sto legando le tabelle, come se stessi mettendo un puntatore tra esse.
Nella tabella Studenti si ha {Matricola} come chiave primaria che verrà utilizzata come chiave esterna nella tabella Esami con l'attributo {Candidato}.
Si ha il vincolo di integrità referenziale tra Candidato e Matricola in quanto ogni valore che può assumere si riferisce a quella chiave.
Nella seconda tabella si ha come chiave primaria {Materia, Candidato} in quanto un candidato può verbalizzare esami di diverse materie. 

![[Pasted image 20240219004854.png]]L'esempio si può estendere a 3 tabelle, mettendo 2 puntatori nella tabella esami, uno che punta a studenti e l'altro a corsi.

Nella tabella studenti Matricola è la chive primaria e come prima in Esami c'è un vincolo referenziale che prende come chiave esterna Studente che  punta a Matricola.
In Corsi la chiave primaria è Codice e viene puntato dalla chiave esterna di Esami Corso.

In Esami la chiave primaria c'è, la prof non l'ha messa, ed è {Studente, Corso}.
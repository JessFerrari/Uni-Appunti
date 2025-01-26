---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello relazionale -  Traduzione di schemi]]"
tags:
  - esempio
  - BD
Creation: 2024-02-19
---
Schema concettuale:
![[Pasted image 20240219015128.png]]
Un'esame è sostenuto da un solo studente e uno studente sostiene da 0 a più esami
Manca la matricola in esami in quanto è data dall'associazione tra esami e studenti. Mettercela sarebbe stata un'errore.


Schema logico:
![[Pasted image 20240219015520.png]]
Aggiungo l'attributo Candidato in esami in modo da poterlo usare come chiave esterna.
Se metessi la materia in Studenti lo studente potrebbe sostenere un solo esame.
![[Pasted image 20240219015736.png]]

Questa soluzione NON buona perché c'è ridondanza in quanto ogni volta che uno studente sostiene un esame si aggiunge una ennupla relativa ad esso e se questo cambia degli attributi bisogna cambiarla in ogni ennupla.
![[Pasted image 20240219020323.png]]


Questa è molto simile alla prima ma è più dispendiosa sia a livello di spazio e di tempo per recuperare tutti gli esami fatti da uno studente bisogna percorrere 3 tabelle.
![[Pasted image 20240219020108.png]] Si crea una terza tabella in cui si mettono 2 chiavi esterne che puntano una alla tabella studenti e l'altra alla tabella esami.
Nell'ultima tabella Esame è la chiave primaria in quanto rappresenta il numero identificativo di una verbalizzazione. La coppia {Esame, Candidato} è una superchiave e non una chiave



#### Esempio molti a molti
![[Pasted image 20240219023048.png]]![[Pasted image 20240219023105.png]]![[Pasted image 20240219023121.png]]



### Esempio associazione
![[Pasted image 20240219023211.png]]


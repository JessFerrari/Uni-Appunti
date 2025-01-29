---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello relazionale - Algebra relazionale]]"
tags:
  - esempio
  - BD
Creation: 2024-02-21
---
# Esempio raggruppamento
Per ogni candidato: numero degli esami, voto minimo, massimo e medio:
$_{ \{Candidato \} }\gamma_{ \{ count(*), min(voto), max(voto), avg(voto) \} } (Esami)​$
![[Pasted image 20240220201911.png]]
Vengono partizionati i candidati sull'attributo Candidato e poi vengono calcolati gli attributi raggruppati della nuova relazione.


### Posso raggruppare per voto ?
- Si, posso raggruppare per voto e se faccio l'operazione min(Voto) viene 20
- non capisco me deve essere 
- ![[Pasted image 20240221020955.png]]

# Posso raggruppare su chiave primaria ? cosa succede?
![[Pasted image 20240221021147.png]]
Succede che per ogni matricola $Count(*)$ è 1.



# Raggruppamento su più attributi
![[Pasted image 20240221021027.png]]


# Per ogni studente visualizzare matricola, nome, cognome e numero di esami sostenuti
![[Pasted image 20240221021602.png]]
---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBS - Ordinamento]]"
tags:
  - BD
Creation: 2024-03-04
---
# Proiezione : SELECT
![[Pasted image 20240304233504.png]]
Si legge R e si scrive T che contiene solo gli attributi della select
Si ordina E su tutti gli attributi e si eliminano i duplicati

# Restrizione con condizione semplice : WHERE
Se utilizzo gli indici devo scorrere tutte le pagine della tabella e costa il costo per l'accesso agli indici più il costo di accesso ai dati.
![[Pasted image 20240304233808.png]]


# Aggregazione e raggruppamento 

Si visitano i dati e si calcolano le funzioni di aggregazioni es. count( * )

Se invece si ha un raggruppamento (Group by) si possono ordinare i dati sugli attributi del GROUP BY, poi si visitano i dati e si calcolano le funzioni di aggregazione per ogni gruppo.


# Join
Fare il prodotto R x S è grande; pertanto, R x S non seguito da una restrizione è inefficiente.
di solito nella restrizione si usa la relazione chiave esterna chiave primaria
Anche se logicamente il Join sia commutativo, dal punto di vista fisico vi è una chiara distinzione, che influenza anche le prestazioni, tra operando sinistro (o “esterno”, “outer”) e operando destro (o “interno”, “inner”)

![[Pasted image 20240304234256.png]]
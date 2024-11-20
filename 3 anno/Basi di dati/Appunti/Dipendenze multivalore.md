---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Dipendenze funzionali]]"
tags:
  - BD
Creation: 2024-02-27
---
# Dipendenze multivalore

Nella [[Normalizzazione di schemi]] oltre le anomalie di _[[Dipendenze funzionali|dipendenza funzionali]]_ ce n'è di un altro tipo che riguarda i casi in cui ci sono _proprietà multi valore indipendenti_.

Per risolvere questo problema va estesa la teoria della normalizzazione con
1. una nuova dipendenza tra i dati, _dipendenza multi valore_
2. estendere la _[[Dipendenze funzionali derivate|dipendenza derivata]]_ alla dipendenza multi valore
3. nuove [[Regole di inferenza|regole di inferenza]] _corrette e complete_ per la derivazione
4. esiste la nozione di [[Decomposizione dei schemi|decomposizione]] che preserva _dati e dipendenze_
5. è stata definita una nuova forma normale detta _[[Forme normali - Quarta forma normale|quarta forma normale]]_ (4NF) che generalizza la forma [[Forme Normali - Boyce-Codd|BCNF]]
6. Algoritmo di normalizzazione per la _quarta forma normale_ con stesse proprietà del algoritmo per BCNF
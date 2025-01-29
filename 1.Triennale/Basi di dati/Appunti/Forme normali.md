---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Normalizzazione di schemi]]"
tags:
  - BD
Creation: 2024-02-24
Esempi: "[[Esempi forme normali]]"
---
 Dalla _teoria di normalizzazione_ deriva il processo di __*normalizzazione degli schemi relazionali*__ che trasforma una _rappresentazione esistente_ in una rappresentazione in _forma normale_.

Una _forma normale_ di una schema relazionale è una forma _equivalente_ al originaria che assicura le buone qualità di un [[Base di dati|database]], ovvero è migliore secondo la _teoria della normalizzazione_.


> [!NOTE] ### Forme normali
> Una _forma normale_ è una proprietà di una base di dati relazionale che ne garantisce la “qualità”, cioè l’assenza di determinati difetti.
> 
> Quando una relazione _non_ è normalizzata essa presenta ridondanze e si presta a comportamenti poco desiderabili durante gli aggiornamenti.
> 

### Forme normali
Le _forme normali_ sono un criterio di valutazione su ciò controllare i _schemi relazionali_ esistenti in modo da trasformarli in schemi che rispettano i criteri

#### Prima e seconda forma normale
le prime de _forme normali_ sono elencante per motivi storici siccome sono vere implicitamente con i sistemi moderni usati
1. _prima forma normale_: ogni valori dei domini di una relazione sono _atomici_
2. _seconda forma normale_: tutti gli attributi dipendono dalla [[Modello relazionale - chiave#Chiave primaria|chiave primaria completa]]
3. [[Forme Normali - Terza forma|Terza forma normale]]
4. [[Forme Normali - Boyce-Codd|Forma normale Boyce-Codd]]
5. [[Forme normali - Quarta forma normale|Quarta forma normale]]

Ognuna di questa _implica la precedente_
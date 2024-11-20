---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Dipendenze funzionali derivate]]"
tags:
  - BD
Creation: 2024-02-25
---

# Schema relazionale - Assiomi di Armstrong
---
#### Assiomi di Armstrong (Definizione)
gli _assiomi di Armstrong_ sono un insieme di [[Regole di inferenza|regole di inferenza]] per la [[Dipendenze funzionali derivate|derivazione]] di [[Dipendenze funzionali|Dipendenze funzionali]] _corretto_ e _completo_.

- ___Riflessività___: se $Y \subseteq X$ allora $X \rightarrow Y$
- ___Arricchimento___: se $X \rightarrow Y$ e $W \subseteq T$ allora $XW \rightarrow YW$
- ___Transitività___: se $X \rightarrow Y$ e $Y \rightarrow Z$ allora $X \rightarrow Z$

##### Regole derivate
Dagli assiomi base si possono dimostrare le seguenti formule:
- ___Identità___ $\{ \} \vdash X \rightarrow X$
- ___Decomposizione___: $\{ X \rightarrow YZ \} \vdash X \rightarrow Y,X \rightarrow Z$
- ___Unione___: $\{ X \rightarrow Y,X \rightarrow Z \} \vdash X \rightarrow YZ$
- ___Indebolimento___: $\{ X \rightarrow Y \} \vdash XZ \rightarrow Y$

> [!NOTE] ## Teorema
> Gli _assiomi di Armstrong_ sono __corretti__ e __completi__

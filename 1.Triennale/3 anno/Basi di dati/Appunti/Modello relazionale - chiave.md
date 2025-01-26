---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Modello relazionale]]"
Esempi: "[[Esempi chiavi]]"
Esercizi: "[[Esercizi chiavi]]"
tags:
  - BD
Creation: 2024-02-17
---
**Informalmente** : una chiave è un insieme di attributi che indentificano le ennuple di una relazione in modo univoco.
Gli attributi scelti per le chiavi non devono essere mutabili nel tempo.

Formalmente:
#### Superchiave
> [!NOTE] Superchiave
> Un insieme $K$ di attributi è **superchiave** per $r$ se $r$ _non_ contiene due ennuple (distinte) $t_1$ e $t_2$ con $t_1[K] = t_2[K]$. 

#### Chiave
> [!NOTE] Chiave
> $K$ è **chiave** per $r$ se è una _superchiave minimale_ per $r$, cioè non contiene un’altra superchiave.


Una [[Modello relazionale#Relazione|relazione]] non può contenere ennuple distinte ma con valori uguali (una relazione è un sottoinsieme del prodotto cartesiano).

___Una superchiave di tutte le relazioni è l’insieme di tutti gli attributi su cui è definita e quindi ogni relazione ha (almeno) una chiave___. 

L'esistenza delle chiave garantisce l'accessibilità a ciascun elemento della base di dati.

Le chiavi permettono di correlare i dati in relazioni diverse.

Non possono esserci valori nulli tra i valori di una chiave in quanto questo non permette di identificare le ennuple e di realizzare facilmente i riferimenti da altre relazioni.

### Chiave primaria
> [!NOTE] Chiave primaria
> Una **chiave primaria** è una chiave su cui non sono ammessi i valori nulli
> 
> 	L’attributo viene generalmente sottolineato per denotare lo stato di chiave primaria.
In generale una chiave può avere dei valori Null.
In una tabella deve essere SEMPRE definita una chiave primaria

Nel [[Modello relazionale|modello relazionale]] le informazioni in relazioni diverse sono correlate attraverso valori comuni, in particolare vengono presi in considerazione i valori delle chiavi (primarie), le correlazioni devono però essere “coerenti”.

### Chiave esterna
Grazie alle chiavi si può definire il [[Modello relazionale - vincoli d'integrità|vincolo di integrità referenziale]] con il quale si parla di ___chiave esterna___.

Una chiave esterna punta alla chiave primaria di un'altra tabella e può essere formata da più elementi. 
![[Pasted image 20240219004704.png]]

---
---
---

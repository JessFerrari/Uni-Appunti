---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Normalizzazione di schemi]]"
tags:
  - BD
Creation: 2024-02-24
---

# Schemi relazionali - Dipendenze derivate
---
Le _dipende derivate_ in uno _[[Modello relazionale|schema relazionale]] $R \langle T,F\rangle$_ sono tutte le [[Dipendenze funzionali|dipendenze funzionali]] _derivabili_ da quelle presenti in $F$.
Un'[[Dipendenze funzionali#^3d8c8a|istanza valida]] oltre le dipendenze in $F$ deve sodisfare anche tutte _quelle derivate_.

> [!NOTE] Dipendenza Derivata (Definizione)
> _Sia_ $R \langle T,F\rangle$ un _[[Modello relazionale|schema relazionale]]_
> _Allora_ una _dipendenza derivata_ indicata con 
> $F \models X \rightarrow Y$ ($F$ _Implica logicamente_ $X \rightarrow Y$)
> è tale _se_ ogni istanza $r$ di $R(T)$ che soddisfa $F$ soddisfa anche $X \rightarrow Y$


Da questa definizione vale immediatamente che 
- $\{ X \rightarrow Y,X \rightarrow Z \}\models X \rightarrow YZ$, [[Dipendenze funzionali#Dipendenze funzionali atomiche|DF atomiche]]
- $\{  \} \models X \rightarrow X$ , implicate da vuoto


#### Ricerca Delle dipendenze derivate
Per cercare tutte le _dipendenze derivate_ partendo da un insieme $F$ di [[Dipendenze funzionali|dipendenze funzionali]] c'è bisogno di un _insieme di regole_ che permettono di costruire un [[Algoritmi|algoritmo]]. 
Si utilizzano le [[Regole di inferenza|regole di inferenza]] in questo contesto detti “assiomi”

##### Definizione
_sia_
- $F$ un insieme di _[[Dipendenze funzionali|dipendenze funzionali]]_
- $RI$ un [[Insiemi|insieme]] di [[Regole di inferenza|regole di inferenza]] per $F$
_allora_  si indica con $F \vdash X \rightarrow Y$ la derivabilità di $X \rightarrow Y$ usando $RI$ e
- L insieme $RI$ è _corretto_ se: $F \vdash X \rightarrow Y \implies F \models X \rightarrow Y$
- L Insieme $RI$ è _completo_ se $F \models X \rightarrow Y \implies F \vdash X \rightarrow Y$

> [!tip]
> L'insieme corretto e completo più famoso sono gli [[Schema relazionale - Assiomi di Armstrong|assiomi di Armstrong]]


> [!NOTE] DERIVAZIONE
> Sia F un insieme di dipendenze funzionai
> Si deice che X -> Y sia derivabile da F ($F\vdash X\rightarrow Y$)
> se X->Y può essere inferito da F usando gli [[Schema relazionale - Assiomi di Armstrong|assiomi di Amstrong]]

### Regole derivate

**UNIONE U** : {X->Y, X->Z}  $\vdash$  X->YZ
	Dimostrazione
		X->Y per ipotesi
		X->XY per arricchimento
		X->Z per ipotesi
		X->XZ per arricchimento
		X->YZ per transitività
**DECOMPOSIZIONE D** : Z$\subseteq$Y {X->Y} $\vdash$ X->Z



> [!NOTE]Derivazione di una dipendenza (Definizione)
> Una _derivazione_ di $f$ da $F$ è una sequenza finita $f_{1},\dots f_{m}$ di _dipendenze_ dove 
> - $f_{m}=f$ 
> - ogni $f_{i}$ o è un _elemento_ di $F$ oppure è stato _derivato da_ $F$ con delle _[[Regole di inferenza|regole di inferenza]]_  
> 
> vale che ogni _sotto sequenza_ $f_{1},\dots,f_{k}$ è una _derivazione_ e quindi che $$F \vdash f_{k} \ \ \forall k\leq m$$
---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Statistical Learning Theory - Vapnik]]"
tags:
  - ML
  - STAT
Creation: 2025-02-06
---
# Shattering (frammentazione)
---
Dati:
- $X$ : input space
- $N$ : numero delle istanze di $X$ (distinte)
- $H$ : spazio delle ipotesi

Con un problema di classificazione si hanno $2^N$ possibili dicotomie.
Una dicotomia è uno dei vari modi di assegnare alle istanze di $N$i valori +1/-1 
Una dicotomia è rappresentata da $H$ se esiste $h \in H$ che realizza tale dicotomia.

*Def.*
$H$ frammenta $X$ se e solo se $H$ può rappresentare tutte le possibili dicotomie di $X$.

Ciò vuol dire che in $H$ esiste una funzione $h$ in rado di separare $X$ in tutti i modi possibili.
Per ogni dicotomia esiste inoltre un'ipotesi $h \in H$ consistente con X.

# VC - dimension
La VC dimension è una misura della complessità dello spazio delle ipotesi $H$.
Per complessità di $H$ non si intende la numerosità dell'insieme ma il numero di istanze distinte che si possono determinar utilizzando $H$.
#### [[Neural Networks#Potere espressivo|VC-dimension for NN]]
- se i pesi sono a 0 si ha la minima VC-dimension
- se i pesi sono piccoli -> piccola VC-dim e si è nella parte lineare della funzione di attivazione 
- se i pesi sono alti il modello diventa più complesso


Con il  concetto di shattering si definisce come:
	Dato un insieme di funzioni $H$ 
	La VC dimension è il massimo numero di punti ($N$) che può essere frammentato da H
	
Se la $VC(H)=p$ allora $H$ non può frammentare più di $p$ punti.
Non tutte le configurazioni di $p$ punti possono essere frammentate da un $H$ con $VC(H)=p$ ma ne basta trovare una.

La VC dimension di una classe di iperpiani lineari (piani di separazione) in $n$ dimensioni è pari ad $n+1$
- Funzioni lineari : $VC(H)=3$


La VC dimension non dipende necessariamente dal numero di parametri  liberi (ad esempio i pesi e il bias nelle reti neurali).
Per esempio il k-nn ha un solo parametro libero ma $VC \to \infty$

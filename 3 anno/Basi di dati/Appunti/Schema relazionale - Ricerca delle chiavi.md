---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Dipendenze funzionali derivate]]"
tags:
  - BD
Creation: 2024-02-25
---
# Chiave candidata e attributo primo

> [!NOTE] Definizione : Chiave candidata e attributo primo
> Dato lo [[Modello relazionale|schema relazionale]] $R<T, F>$, 
> si dice che un insieme di attributi $W \subseteq T$ è una chiave candidata di $R$, se
> - $W → T \in F^+$ ( ossia se $W$ superchiave) 
> o
> - $\forall V \subset W,\ V → T \notin F^+$ (se V appartiene a W, V non è superchiave)
> 
> **Attributo primo** : un attributo primo è un attributo che appartiene ad almeno una chiave

Per capire se W è chiave o superchiave bisogna applicare la chiusura di $W^+$
	Se applico la [[Schema relazionale - Chiusura|chiusura]] a W mi fermo quando non posso più aggiungere attributi e se alla fine ci sono tutti allora è superchiave (o chiave)

![[Pasted image 20240225060712.png]]
![[Pasted image 20240225060846.png]]

Dato che D non è determinabile in nessun modo si dirà che D si deve mettere nella chiave. Stesso discorso per A. 

Si può sospettare la presenza di una chiave prendendo gli attributi che sono a sinistra e non a destra ma non va sempre bene
# Ricerca delle chiavi

***[[Complessità|Complessità]]*** : Il problema di trovare tutte le chiavi di una relazione richiede un algoritmo di [[Complessità|complessità]] esponenziale nel caso peggiore.
Il problema di controllare se un attributo è primo è NP-completo

**Proprietà per trovare tutte le chiavi** : 
1. Se un attributo A di T non appare a destra di alcuna dipendenza funzionale allora A appartiene ad ogni chiave di R
2. Se un attributo A di T appare a destra di qualche dipendenza in F ma non a sinistra di alcuna dipendenza non banale allora A non appartiene a nessuna chiave

# Algoritmo per trovare tutte le chiavi 
##### Esempio:
![[Pasted image 20240225064032.png]]
- Se solo a sinistra lo metto, se solo a destra nono lo metto
- Se sta da entrambe le parti bisogna valutare se è superfluo o no

Devo fissare un insieme X di attributi che appaiono solo a sinistra fare la chiusura e tentare tutte le chiavi. Quando trovo un attributo che potrei inserire guardo dove si trova:
- se si trova solo a destra non lo metto e non è una chiave
- se si trova da entrambi i lati lo metto e guardo se riesco ad ottenerla

--- 
##### Algoritmo Lineare nelle chiusure
Sfruttando le due osservazioni viste si può trovare __una__ sola chiave in modo lineare

Si parte dalla [[Modello relazionale - chiave|superchiave]] banale, ovvero quella composta da tutti gli attributi e si escludono mano gli elementi finche quello che resta e’ una chiave 

per saltare dei passaggi si possono escludere direttamente gli attributi che non appaiono mai a sinistra

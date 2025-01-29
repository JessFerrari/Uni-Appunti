---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Dipendenze funzionali derivate]]"
tags:
  - BD
Creation: 2024-02-25
Esempi: "[[Esempi copertura]]"
---
# Funzioni equivalenti
> [!NOTE] Dipendenze funzionali equivalenti
> Due insiemi di dipendenze funzionali, F e G, sullo schema R sono equivalenti, $$F \equiv G ,\ sse\ F^+ = G^+$$
> Se $F \equiv G$, allora F è una copertura di G (e G una copertura di F).


# Attributo estraneo
> [!NOTE] Attributo estraneo
> Sia F un insieme di dipendenze funzionali:
> 
> Data una dipendenza funzionale $X\to Y \in F$ si diche che X contiene un attributo estraneo $A_i$ SSE esiste una dipendenza funzionale equivalente a F in cui se tolgo $A_i$ si deriva la stessa dipendenza funzionale
> $$A_i = attributo\ estraneo\ \iff (X-\{A_i\})\to Y\in F^+$$
> ossia:
> $$F\vdash(X-\{A_i\})\to Y$$

Per verificare se A è estraneo in una dipendenza funzionale del tipo AX->B si calcola $X^+$ e si verifica se include B, ovvero se basta X a determinare B.

L'attributo estraneo serve a calcolare la copertura canonica che serve per calcolare la [[Forme normali|forma normale]].

Grazie alla definizione di attributo estraneo si può calcolare se una superchiave è minimane ovvero se un'attributi che si ha è minimale cercando di eliminare tutti gli attributi estranei se ci sono. ^778bbb

# Dipendenza ridondante
> [!NOTE] Dipendenza ridondante
> Sia F un insieme di dipendenze funzionali,
> X->Y è una dipendenza ridondante SSE la chiusura di F meno la dipendenza funzionale sia equivalente a F 
> 
> $$X-\to Y =dipendenza\ ridondante\ \iff  (F-\{X\to Y\})^+\equiv F^+$$
> ossia:
> $$F-\{X\to Y\}\vdash X\to Y$$

Per stabilire che una DF del tipo X->A è ridondante si elimina da F, si calcola $X^+$ e si verifica se include A, ovvero se con le DF che restano si riesce ancora a dimostrare che X->A


# Copertura canonica

> [!NOTE] Copertura canonica
> F è detta copertura canonica SSE:
> - la parte destra di ogni DF in F è un attributo
> - non esistono attributi estranei
> - nessuna DF in F è ridondante

## Teorema : esistenza della copertura canonica

_Per ogni insieme di dipendenza F esiste una copertura canonica_

## Algoritmo per calcolare la copertura canonica

1. Trasformare le dipendenze nella forma $X\to A$, ossia si sostituisce l'insieme dato con quello che ha i membri di destra costituiti da singoli attributi ([[Dipendenze funzionali#Dipendenze funzionali atomiche|dipendenze atomiche]])
2. Eliminare gli attributi estranei, ossia per ogni DF si verifica se esistono attributi eliminabili dal primo membro
3. Eliminare le dipendenze ridondanti
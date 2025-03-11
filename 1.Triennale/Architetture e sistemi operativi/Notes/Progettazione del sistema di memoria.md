---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Cache]]"
tags:
  - AESO
  - memories
Creation: 2025-02-24
---
La miss penalty può essere ridotta aumentando il traffico di dati tra la DRAM e la cache.

Si possono avere tre tipi di organizzazioni di memoria :

1. Semplice : viene letta solo una parola per volta dalla memoria
2. Wide-memory : vengono lette N parole
3. Interlacciata : k banchi di memoria indipendente possono rispondere a k richieste contemporanee
4. ![[Pasted image 20250223185837.png]]

Si suppone di avere un singolo modulo di memoria. I tempi di servizio della memoria e della cache sono rispettivamente $t_M$ e $t_{cache}$.

La grandezza di banda possibile è $B_M =\frac1 {t_M}$ e $b=1$.

Se la linea di cache contiene b>1 il costo di trasferimento dell'intero blocco in caso di cache miss è :

$t_{miss}=2t_{trf}+(m+1)t_{cache}+bt_M\simeq bt_M$

Usando una memoria modulare interlacciata a m moduli si può aumentare la banda di un fattore di m : $B_M=\frac m {t_M}$ In questo caso si avrà che il tempo di servizio in caso di miss è uguale a:

$t_{miss}=2t_{trf}+(m+1)t_{cache}+\frac b m t_M$

E nel caso in cui mettessimo che il numero di moduli della DRAM è uguale al numero di parole in un blocco di cache , ossia m=b, si avrà $t_{miss}\simeq t_M$

![[Pasted image 20250223185921.png]]


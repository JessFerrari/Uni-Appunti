---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
tags:
  - AESO
Creation: 2025-02-24
---
## Sistemi di input o di output o input/output

Posso essere uomo-macchina o macchina-macchina, sono molto eterogenei anche per la velocità.

La prima distinzione è input output rispetto al processore. 
Ad esempio le schede di rete sono sia di input che di output.

Nei sistemi I/O per l'eterogeneità dell'utilizzo e velocità sono classificabili anche per i protocolli e l'affidabilità ossia che si rompono e si possono sostituire o sistemare.

## Prestazioni

Si vuole misurare l'impatto del tempo di accesso sull'intera elaborazione, ad esempio 1/10 e quindi il tempo totale è 11/10, se io miglioro la CPU di 10 volte lasciando inalterato il sistema i/o viene 1/5 di prestazione (SPEED UP).

Si ha un fattore di incremento e ho perso dell'efficienza in quanto non ho ottimizzato il sistema di I/O.

#### AMDAHL LAW
Permette di capire lo speedup ottenibile se si migliora solo una parte . Lo speedup massimo è impattata comunque dalla parte del programma che non viene ottimizzata, mi da comunque un limite.

Sono molto importanti quindi i miglioramenti dei sistemi di I/O

### Affidabilità

Metrica : MEAN TIME TO FAILURE (Tempo prima che si abbia un guasto)

### Disponibilità

Metrica : MEAN TIME TO REPAIR


### Com'è fatto un sistema di I/O?

Ha due porte logiche:
- Controllo:
	- Filo 1 inviare comandi
	- Filo 2 stato
- Dati

Il controllo ha funzionalità di timing , comunicazioni con il device, fa un po' di buffering, controllare l'affidabilità (esempio nei sistemi raid quando un disco si rompe il controllore lo dice e fa continuare a lavorare gli altri).

### PASSI LOGICI

La CPU controlla se il dispositivo è in uno stato valido e il controllore risponde e dice se è occupato o no.
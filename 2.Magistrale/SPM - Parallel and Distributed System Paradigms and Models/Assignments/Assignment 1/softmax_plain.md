---
Subject: "[[Indice - Parallel and Distributed System|SPM]]"
Super Topic: "[[SPM - Assignment 1]]"
tags:
  - Assignment
  - SPM
Creation: 2025-03-11
---
## **Riassunto del funzionamento**

1. **Trova il massimo dell'input**
    - Questo evita problemi numerici legati agli esponenziali molto grandi.
2. **Calcola la funzione softmax**
    - Usa `std::exp(input[i] - max_val)` per evitare overflow.
    - Somma tutti i valori esponenziati.
3. **Normalizza i valori**
    - Divide ogni elemento per la somma totale, ottenendo così una distribuzione di probabilità.
4. **Main function**
    - Prende un parametro `K` dalla linea di comando per definire la dimensione dell'input.
    - Genera un array casuale di numeri in **[-1,1]**.
    - Misura il tempo di esecuzione con **TIMERSTART** e **TIMERSTOP**.
    - Se richiesto, stampa i risultati.
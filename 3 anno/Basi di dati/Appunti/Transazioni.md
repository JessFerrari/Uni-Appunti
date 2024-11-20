---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Base di dati]]"
tags:
  - BD
Creation: 2024-02-08
---
Le operazioni nelle [[Base di dati|basi di dati]] si chiamano transazioni.

Una **transazione** è una sequenza di azioni di lettura e scrittura in memoria permanente e di elaborazioni di dati in memoria temporanea, con le seguenti proprietà:

- _**Atomicità**_: Le transazioni che terminano prematuramente (aborted transactions) sono trattate dal sistema come se non fossero mai iniziate; pertanto eventuali loro effetti sulla base di dati sono annullati.
- _**Persistenza**_: Le modifiche sulla base di dati di una transazione terminata normalmente sono permanenti, cioè non sono alterabili da eventuali malfunzionamenti.
- _**Serializzabilità:**_ Nel caso di esecuzioni concorrenti di più transazioni, l’effetto complessivo è quello di una esecuzione seriale
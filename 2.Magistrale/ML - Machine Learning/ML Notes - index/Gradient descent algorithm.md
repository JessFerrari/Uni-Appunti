---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks]]"
tags:
  - ML
Creation: 2025-02-05
---
L'algoritmo **gradient descent** si basa sul calcolo del gradiente dell'errore rispetto ai pesi della rete, aggiornandoli per diminuire progressivamente per diminuire il valore della [[Loss Function|funzione di errore]].
Il calcolo del gradiente viene fatto con la [[Back Propagation|back propagation]].

In base a come vengono gestiti gli input nella rete esistono diverse varianti:
- ***Batch gradient descent***: che utilizza tutto il batch di dati del training e vengono aggiornati i pesi dopo un epoca intera. La stima è precisa ma necessita molto tempo per essere eseguito.
- ***Online***: che aggiorna i pesi dopo ogni esempio. Ciò rende la convergenza più rapida ma l'allenamento molto instabile, può trovare una buona soluzione anche prima di completare un'epoca ma può rimanere su minimi locali sub-ottimali
- ***Mini-batch***: combina la precisione del batch con la velocità dell'online aggiornando i pesi dopo un gruppo di dati
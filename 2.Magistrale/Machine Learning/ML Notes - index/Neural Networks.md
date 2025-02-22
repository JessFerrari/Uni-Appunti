---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
  - "#totranslate"
Creation: 2025-01-31
---
# Neural Network
---
Le reti neurali comprendono un grande insieme di reti per questo motivo si può considerare un paradigma.

Le NN possono imparare da esempi e gestire dati continui o discreti sia per problemi di classificazione che di regressione.

Sono degli [[Universal approximation|approssimatori universali]] e utili anche per la rappresentazione di funzioni non lineari.



# Unit
---

Una rete neurale è composta da nodi detti unità o neuroni artificiali.
Ogni neurone è composto da due parti :
- $net_{i}(\mathbf{x})=\sum_{j}w_{ij}x\mathbf{x}_{j}$ , ossia la somma pesata degli input 
- $o_{i}=f_{i}(net_{i}(\mathbf{x}))$, ossia l'output del neurone calcolato attraverso la [[Activation functions|funzione di attivazione]] del neurone

# Architecture
---
Nelle reti neurali, per poter rappresentare più funzioni si utilizzano gli hidden layers, in modo da facilitare il lavoro all'ultimo layer (quello di output).
In questo modo la rete può imparare feature interne e relazioni di dai
# Learning methods
---
Per i metodi learning si distinguono storicamente:
- ***Adaline (Adaptive Linear Neuron)***: in cui vengono utilizzate delle unità lineari e come algoritmi di training si applica direttamente la ***LMS*** con ***Gradient Descent***. Si usa sia per la regressione che per la classificazione e si generalizza per ottenere un approccio utilizzabile com le MLP
- ***[[Perceptron]]***: utilizza un unità non lineare con un forte limite al threshold ed è utile solo per la classificazione


# Neural networks as LBE
---
Le reti neurali possono essere viste come un metodo per fare [[Linear Basis Expansion - LBE|espansione di base LBE]]. 
Infatti, ricordiamo che per la LBE si otteneva:
- classificazione : $h(\mathbf{x})=f\left( \sum_{j}w_{j}\phi_{j}(\mathbf{x}) \right)$ 
- regressione : $h(\mathbf{x})=\sum_{j}w_{j}\phi_{j}(\mathbf{x})$

Data una rete neurale della forma : $h(\mathbf{x})=f_{k}\left( \sum_{j} w_{jk}f_{j}\left( \sum_{i}w_{ij}x_{i} \right)\right)$
Se si pone $\phi_{j}(\mathbf{x,w})=f_{j}\left( \sum_{i} w_{ji}x_{i}\right)$
Si ottiene una rete della forma : $h(\mathbf{x})=f_{k}\left( \sum_{j}w_{j}\phi_{j(\mathbf{x,w})} \right)$

In questo caso $\phi$ non dipende solo dai dati ma anche dai pesi.

## Differenze:
- LBE è un'espansione di base fissa e selezionata in precedenza
- le NN sono adattive e quindi flessibili. Dato che $\phi$ dipende anche dai pesi e questi sono in evoluzione nel processo di training allora anche $\phi$ cambierà nel metre
	- Ogni hidden unit si può vedere come una LBE indipendente che impara una feature non lineare in modo adattivo.


# Potere espressivo
---
Il potere espressivo di una rete neurale dipende da principalmente da:
- il numero di neuroni utilizzati, [[VC-Dimension]] del modello
- l'architettura della rete stessa


# Inductive Bias
---
Ricerca : algoritmo di back propagation
Linguaggio : Le funzioni che si possono esprimere con l'architettura scelta


# Loading problem
---
Data una rete neurale ed un set di esempi di training, dire se c'è un insieme di pesi per cui la rete è consistente con gli esempi è un problema *NP-completo*
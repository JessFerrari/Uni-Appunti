---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Neural Networks|NN]]"
tags:
  - ML
  - NN
Creation: 2025-03-09
---
Una __[[Neural Networks|rete neurale]] Feed Forward__ è un tipo di __[[Parametric Machine Learning Models|modello parametrico]]__ di [[Machine Learning|machine learning]]  e viene solitamente allenato con [[Supervised Learning|algoritmi supervisionati]].


__Le unità sono connesse tramite collegamenti pesi__ e organizzate in _layers_ con la seguente struttura:
- __Input Layer__: Copia i pattern esterni $x$ sugli ingressi (non calcola $\text{net}$ né $f$).
- __Hidden Layer__: Il livello nascosto proietta sul livello di output (o su un altro livello nascosto).
- __Output Layer__ : ultimo layer del modello che ne calcola l output 

Ogni neurone è un __unità__ definito in modo molto simile al [[Perceptron|percettrone]] ma se ne cambia la [[Activation functions|funzione di attivazione]].

![[Pasted image 20250309021718.png]]

Una __Feed Forward__ può anche essere vista come come un __ipotesi flessibile__ $h$. 
Per questa $h$ vale che a ogni input è associato un solo output e quindi è una [[Funzioni|funzione]].

Considerando un __input layer__, un __hidden layer__ e un __output layer__, l'ipotesi che rappresenta la rete e definita con la seguente funzione: $$h_\mathbf{W}(\mathbf{x})=f_k\left(\sum_jw_{kj}f_j\left(\sum_iw_{ji}x_i\right)\right)$$Dove
- $\mathbf{W}$ è la matrice dei __parametri__ ovvero i pesi 
- $\mathbf{x}$ il vettore di __input__.

#Sbagliato
Se $f$ è una funzione lineare allora $h$ è funzione NON è lineare nei parametri $W$.
Nel caso in cui questa invece sia lineare allora l'ipotesi diventa uguale ad avere un solo layer e si ritorna ad un [[Linear models|modello lineare]].

Con $h$ non lineare si ha che il problema di ottimizzazione per imparare i parametri diventa un problema non lineare.



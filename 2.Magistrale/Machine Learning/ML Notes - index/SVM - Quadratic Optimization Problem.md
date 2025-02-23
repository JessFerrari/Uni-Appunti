---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[SVM]]"
tags:
  - ML
  - "#SVM"
  - CMDLA
Creation: 2025-02-07
---
Trovare l'iperpiano ottimale per le SVM è un [[Convex optimization problems|problema di ottimizzazione convesso]], e si sviluppa in 4 passi principali:
1. Problema primale vincolato per trovare l'iperpiano ottimale 
2. Costruzione delle funzioni Lagrangiane
3. Derivazione delle condizioni di ottimalità
4. Risoluzione del problema in forma duale con i moltiplicatori Lagrangiani


# Hard margin
## 1. Problema primale - problema di ottimizzazione vincolato
---

*DEF. problema primale
	Dati gli esempi di training $\{(\mathbf{x}_{i},d_{})\}^N_{i=1}$ , trovare i valori ottimi del vettore dei pesi $\mathbf{w}$ e del bias $b$ in modo tale che soddisfino i vincoli, senza errori di classificazione:
	$$d_{i}(\mathbf{w}^T\mathbf{x}_{i}+b)\geq 1 \text{  for } i =1\dots N$$
	E che minimizzano la funzione di costo :$$\Phi(\mathbf{w})=\frac{1}{2}\mathbf{w}^T\mathbf{w} \text{ , ossia che minimizza } ||\mathbf{w}||$$

- La funzione obiettivo $\Phi$ è quadratica e convessa in $\mathbf{w}$
- I vincoli sono lineari in  $\mathbf{w}$

Il costo computazionale di risolvere il problema primale scala con la dimensione dell'input space.


## 2. Costruzione della funzione Lagrangiana
---

Per risolvere il problema primale bisogna usare il metodo dei [[Lagrangian multipliers|moltiplicatori di Lagrange]].

Si costruisce quindi una funzione Lagrangiana corrispondente al problema primale:
$$J(\mathbf{w},b,\alpha)=\frac{1}{2}\mathbf{w}^T\mathbf{w}-\sum_{i=1}^N\alpha_{i}(d_{i}(\mathbf{w}^T\mathbf{x}_{i}+b)-1)$$

> [!NOTE] Forma funzione di Lagrange:
> $L(x, \alpha)=f(x)+\sum_{i=1}^m\alpha_{i}g_{i}(x)$
> 
> dove $f(x)$ è la funzione da minimizzare, $g_{i}(x)$ sono i vincoli da rispettare e $\alpha_{i}\geq 0$ sono i moltiplicatori di Lagrange 

La soluzione del problema di ottimizzazione vincolato è determinato dai [[Punti di sella|punti di sella]] della funzione Lagrangiana $J(\mathbf{w},b,\alpha)$, usando il teorema dei [[saddlepoints.pdf|saddle point]].


> [!NOTE] Punti di sella di una funzione Lagrangiana
> Un punto di sella di una funzione Lagrangiana è un punto in cui le radici  (ossia gli autovalori della matrice Hessiana) sono reali ma del segno opposto

Questi punt di sella devono essere minimizzati rispetto a $\mathbf{w}$ e $b$ e massimizzati rispetto ad $\alpha$.

## 3. Condizioni di ottimalità - Kuhn-Tucker conditions
---

Differenziando $J(\mathbf{w},b, \alpha )$ rispetto a $\mathbf{w}$ e $b$ e ponendo il risultato uguale a zero si ottengono le seguenti condizioni di ottimalità:

1. $$\frac{\partial J(\mathbf{w},b,\alpha)}{\partial \mathbf{w}}=0$$
2. $$\frac{\partial J(\mathbf{w},b,\alpha)}{\partial b}=0$$
Applicando la condizione 1 si ottiene:$$\mathbf{w}=\sum_{i=1}^N\alpha_{i}d_{i}\mathbf{x}_{i}$$ ed in particolare per l'iperpiano ottimale si ottiene :$$\mathbf{w}_{o}=\sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x}_{i}$$ considerando solo i moltiplicatori che esprimono l'iperpiano ottimale.

L'iperpiano ottimale si può quindi esprimere come:$$\mathbf{w}_{o}^T\mathbf{x}+b=0 \iff \left( \sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x}_{i}\right)^T\mathbf{x}+b_{o}=0$$
La soluzione di $\mathbf{w}_{o}$ è *ottima* e *unica* per le proprietà delle funzioni Lagrangiane.

Non lo sono invece i moltiplicatori Lagrangiani $\alpha_{i}$.

Si considerano le ***[[Kuhn - Tucker Conditions]]*** segue che nei saddle point di $J(\mathbf{w},b,\alpha)$ si ha:$$\alpha_{i}(d_{i}(\mathbf{w}^T\mathbf{x}_{i}+b)-1)=0 \quad \forall i=1,\dots,N$$
- se $a_{i}>0$ allora $d_{i}(\mathbf{w}^T\mathbf{x}_{i}+b)=1$ e quindi $\mathbf{x_{i}}$ è un support vector
- se $x_{i}$ non è un support vector allora $\alpha=0$
	- non può essere che $\alpha=0$ e $\mathbf{x}_{i}$ support vector per le proprietà delle KKT conditions (se il vincolo è attivo allora $\alpha>0$)

-> [Karush-Kuhn-Tucker (KKT) conditions: motivation and theorem](https://youtu.be/K3L7UYnZuZ4?si=QfOg6Mw4mZbKIIir)

*Ciò vuol dire che l'iperpiano dipende SOLO dai support vectors*


## 4. Problema duale
---
Per ottenere i moltiplicatori di Lagrange $\{a_{i} \}_{i=1}^N$ si deve risolve il problema in forma duale o con approcci più recenti e più efficienti come le [[Self Organizing Map (SOM)]].

*Problema duale:*
	Dati gli esempi di training $T=\{(x_{i},d_{i})\}^N_{i=1}$ trovare i valori ottimi dei moltiplicatori Lagrangiani $\{(\alpha_{i})\}$
	che soddisfano i vincoli:
	-  $\alpha_{i}\geq 0 \quad \forall i=1,\dots,N$
	- $\sum_{i=1}^N \alpha_{i}d_{i}=0$
	che massimizzano :$$Q(\alpha)=\sum^N_{i=1}\alpha_{i}-\frac{1}{2}\sum_{i=1}^N\sum_{j=1}^N\alpha_{i}\alpha_{j}d_{i}d_{j}\mathbf{x}^T_{i}\mathbf{x}_{j}$$


## Come ottenere l'iperpiano

Dopo aver ricavato i moltiplicatori si passa alla ricerca dell'iperpiano ottimale.
- $\mathbf{w}_{o}=\sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x_{i}}$
- $b_{o}=1-\mathbf{w}_{o}^T\mathbf{x}^{(s)} \to b_{o}=1-\sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x}_{i}$

In realtà non serve calcolare il vettore $w_{o}$ in modo esplicito in quanto, solamente con i moltiplicatori Lagrangiani, ottenuti risolvendo il problema duale.

Infatti, dato che $\mathbf{w}_{o}=\sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x}_{i}$, la superficie di divisione si può esprimere come : $$\mathbf{w}_{o}^T\mathbf{x}+b_{o}=0\iff \sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x}_{i}^T\mathbf{x}+b_{o}=0$$
Quindi, dato un pattern $\mathbf{x}$ si calcola $g(\mathbf{x})=\sum_{i=1}^N\alpha_{o,i}d_{i}\mathbf{x}_{i}^T\mathbf{x}+b_{o}$ e poi si classifica $\mathbf{x}$ in base al segno di $g(\mathbf{x})$.

# Soft margin
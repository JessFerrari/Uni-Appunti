---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[SVM]]"
tags:
  - ML
Creation: 2025-02-14
---
# What's a Kernel?
Un *Kernel* è una funzione matematica che serve per organizzare i dati e rendere più semplice la loro classificazione.

In molti scenari reali, i dati non sono linearmente separabili nell'input space originario, e seguendo il [[Cover's Theorem - Separability of patterns|teorema di Cover]] si sa che dati non linearmente separabili in uno spazio $m_{0}$ lo possono diventare portandoli in uno spazio $m_{1}$ con dimensionalità più alta, detto feature space.![[Pasted image 20250214152752.png]]
Per farlo ci si serve di una funzione $\phi(\mathbf{x}):\mathbb{R}^{m_{0}}\to \mathbb{R}^{m_{1}}$ ma fare questa operazione è un problema difficile.

La formulazione del problema resta la stessa ma :
- i dati di training assumono la seguente forma: $T=\{(\phi(\mathbf{x}_{i}),d_{i})\}^N_{i=1}$
- L'iperpiano si esprime come $\mathbf{w}^T\phi(\mathbf{x})+b=0$
-> se si incorpora $b$ in $\mathbf{w}$ si ha $\mathbf{w}^T\phi(\mathbf{x})=0$ come nella [[Linear Basis Expansion - LBE]].
Il vettore dei pesi $\mathbf{w}$ è una combinazione lineare del *feature vector*: $\mathbf{w}=\sum_{i=1}^N\alpha_{i}d_{i}\phi(\mathbf{x}_{i})$
E quindi l'iperpiano di separazione si esprime come: $\sum_{i=1}^N\alpha_{i}d_{i}\phi^T(\mathbf{x}_{i})\phi(\mathbf{x})=0$, dove $\phi^T(\mathbf{x}_{i})\phi(\mathbf{x})$ è un dot product.
Valutare $\phi(\mathbf{x})$ è un problema intrattabile.


I Kernels aiutano a mappare implicitamente i dati dall'input space originario al nuovo feature space dove i dati sono più facilmente separabili.
Quando le SVMs usufruiscono dei kernel si parla di *Kernel trick*.

Una funzione Kernel calcola la similarità di due dati in uno spazio con una dimensionalità più alta senza passarci davvero. infatti $k(\mathbf{x}_{1},\mathbf{x}_{2}):\mathbb{R}^{m_{0}} \times \mathbb{R}^{m_{0}}\to \mathbb{R}$

I kernel sono funzioni simmetriche quindi $k(\mathbf{x}_{i},\mathbf{x})=k(\mathbf{x},\mathbf{x}_{i})$, quindi la matrice della funzione di kernel è simmetrica, e servono per astrarre l'inner product tra $\phi^T(\mathbf{x}_{i})\phi(\mathbf{x})$.
Infatti si  può dire che :
$$k(\mathbf{x}_{i},\mathbf{x})=\phi^T(\mathbf{x}_{i})\phi(\mathbf{x})$$

## Problema duale con i kernel

Riprendendo il [[SVM - Quadratic Optimization Problem#4. Problema duale|Problema Duale]] e usando  i nuovi dati di input si avrebbe che:

Dati i dati di training $T=\{(\phi(\mathbf{x}_{i}),d_{i})\}_{i=1}^N$ trovare i valori ottimi di $\{ \alpha_{i}\}^N_{i=1}$ che massimizzano la funzione obiettivo :$$Q(\alpha)=\sum_{i
=1}^N \alpha_{i}-\frac{1}{2}\sum_{i,j=1}^N \alpha_{i}\alpha_{j}d_{i}d_{j}\phi^T(\mathbf{x}_{i})\phi(\mathbf{x}_{j})=$$$$=\sum_{i
=1}^N \alpha_{i}-\frac{1}{2}\sum_{i,j=1}^N \alpha_{i}\alpha_{j}d_{i}d_{j}k(\mathbf{x}_{i},\mathbf{x}_{j})=\sum_{i
=1}^N \alpha_{i}-\frac{1}{2}\sum_{i,j=1}^N \alpha_{i}\alpha_{j}d_{i}d_{j}k_{i,j}$$  
E che soddisfino i vincoli :
- $\sum_{i=1}^N \alpha_{i}d_{i}=0$
- $0\leq \alpha_{i}\leq C \quad \forall i=1,\dots,N$
## Pros of using kernels:
1. **SVMs possono gestire problemi non linearmente separabili**: con l'ausilio dei kernel si cambia lo spazio in cui si trovano i dati senza eseguire operazioni computazionalmente costose.
2. ***Flessibilità***: Esistono diversi kernel da usare in diverse situazioni, in base alla natura dei dati e del problema, e in questo modo le SVMs possono gestire tasks diversi.
# Proprietà dei kernel
Dati due Kernel $k_{1}$ e $k_{2}$ entrambi definiti su $\mathbb{R}^{m_{0}} \times \mathbb{R}^{m_{0}}$ allora anche i seguenti sono kernel:
- *somma*:$k_{1}(\mathbf{x},\mathbf{y})+k_{2}(\mathbf{x},\mathbf{y})$ 
- *moltiplicazione per scalare* : $\alpha k_{1}(\mathbf{x}),\mathbf{y} \quad \forall \alpha in \mathbb{R}_{+}$
- *moltiplicazione dei kernels*: $k_{1}(\mathbf{x},\mathbf{y})k_{2}(\mathbf{x},\mathbf{y})$

# Tipi di Kernels
---
- **Lineare**: $k(\mathbf{x},\mathbf{x}_{i})=\mathbf{x} \cdot \mathbf{x_{i}}$
- **Polinomiale**: $k(\mathbf{x},\mathbf{x}_{i})=(\mathbf{x}^T\mathbf{x}_{i}+1)^p$ , dove $p$ è un parametro specificato dall'utente 
- **Radial Basis Function (o gaussiano)**: $k(\mathbf{x},\mathbf{x}_{i})=e^{(-\frac{1}{2\sigma^2}||\mathbf{x}-\mathbf{x}_{i}||^2)}$, dove $\sigma^2$ è un parametro specificato dell'utente
- **Two-layer perceptron**: $k(\mathbf{x},\mathbf{x}_{i})=\text{TanH}(\beta_{0}\mathbf{x}^T\mathbf{x}_{i}+\beta_{1})$, dove $\beta_{0}>0$ e $\beta_{1}<0$ sono parametri specificati dall'utente.

Per il lineare, polinomiale e il RBF si ha sempre l'inner-product kernel, metre per il two-layer perceptron dipende dalla scelta di $\beta_{0}$ e $\beta_{1}$.
Inoltre, il RBF porta ad un feature space con un numero infinito di dimensioni.
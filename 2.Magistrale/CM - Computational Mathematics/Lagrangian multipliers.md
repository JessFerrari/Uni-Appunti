---
Subject: "[[Indice - Computational Mathematics for learning and data analysis|CM]]"
tags:
  - CMDLA
  - ML
Creation: 2025-02-07
---
Il **metodo dei moltiplicatori di Lagrange** è uno strumento utilizzato per risolvere problemi di **ottimizzazione vincolata**.

## **1. Problema generale di ottimizzazione vincolata**

Supponiamo di voler:

- **Minimizzare** una funzione obiettivo $f(\mathbf{x})$ Soggetta a uno o più **vincoli**:
$$g_i(\mathbf{x}) = 0 \quad \text{per } i = 1, \dots, m$$


### **Idea principale**

Quando ottimizziamo $f(\mathbf{x})$ con vincoli, cerchiamo soluzioni che rispettino due condizioni:

1. La funzione $f(\mathbf{x})$ deve essere **stazionaria** nella direzione della variazione permessa dai vincoli.
2. I vincoli devono essere soddisfatti.

Per combinare $f(\mathbf{x})$ e i vincoli in un unico problema, introduciamo una nuova funzione chiamata **funzione Lagrangiana**:

$$\mathcal{L}(\mathbf{x}, \boldsymbol{\lambda}) = f(\mathbf{x}) - \sum_{i=1}^{m} \lambda_i g_i(\mathbf{x})$$

dove:

- $\boldsymbol{\lambda} = [\lambda_1, \dots, \lambda_m]$ sono i **moltiplicatori di Lagrange**, coefficienti che misurano quanto i vincoli influenzano la soluzione ottimale.
- $f(\mathbf{x})$ è la funzione obiettivo.
- $g_i(\mathbf{x})$ sono i vincoli.


### **Condizioni di ottimalità (KKT Conditions)**

Per trovare il punto ottimale, si risolve il sistema di equazioni derivato dalle seguenti condizioni:

1. **Condizione di stazionarietà**: $\nabla_{\mathbf{x}} \mathcal{L}(\mathbf{x}, \boldsymbol{\lambda}) = \nabla f(\mathbf{x}) + \sum_{i=1}^m \lambda_i \nabla g_i(\mathbf{x}) = 0$, che assicura che il gradiente della funzione obiettivo e dei vincoli siano bilanciati

2. **Soddisfacimento dei vincoli**: $g_i(\mathbf{x}) = 0, \quad \forall i$

3. **Condizioni di non negatività** (per vincoli di disuguaglianza, come nel caso degli [[SVM - Quadratic Optimization Problem|SVM]]): $\lambda_i \geq 0 \quad \text{e} \quad \lambda_i g_i(\mathbf{x}) = 0$


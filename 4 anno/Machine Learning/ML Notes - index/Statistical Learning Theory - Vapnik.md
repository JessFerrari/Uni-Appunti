---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning]]"
tags:
  - ML
Creation: 2025-01-09
---
#### Purpose
--- 
Investigate on ***generalization capability*** of a model, measured as a *risk* or *test error*, with respect to the *training error* and analyzing overfitting and underfitting zones.
Including also the role of ***model complexity*** and the role of ***number of  data***.


## Formal setting

#### **Goal in Machine Learning**
- Approximate an **unknown function** $f(\mathbf{x)}$:
    - $f(\mathbf{x})$: The true function we aim to learn.
    - $d$: The target value, which is derived as $d = f + \text{noise}$
- **Objective**: Minimize the **risk function** $R$ over all data, which measures the true error : $R = \int L(d, h(x)) dP(x, d)$ 
	- $L$ is the [[Machine learning#Loss|Loss function]]
	- $P(x, d)$ is the **probability distribution** of data points $(x, d)$.
	**True Error $R$** : Represents how well $h(\mathbf{x})$ (the model hypothesis) matches the true function $f(\mathbf{x})$ over all possible data.

---
#### **Search for the Best Hypothesis**

- **Goal**: Find $h \in H$ (a hypothesis in the hypothesis space) that minimizes $R$.

- **Challenge**:
    - The true risk $R$ depends on the **entire data distribution** $P(x, d)$ which is unknown
    - We only have access to a **finite dataset** $TR = \{(x_p, d_p)\}_{p=1}^l$​ , where $l$ is the number of samples

---

#### **Empirical Risk Minimization (ERM)**

- Instead of minimizing the true risk $R$, minimize the **empirical risk** $R_\text{emp}$​, which is an approximation based on the training data $TR$.
    
- **Empirical Risk**:
    $R_\text{emp}(h, TR) = \frac{1}{l} \sum_{p=1}^l (d_p - h(x_p))^2$
    This is the **training error** $E$, calculated as the average loss over the finite dataset.

---

#### **Key Concept: ERM Inductive Principle**

- **Why Use ERM?**
    - We cannot compute the true risk $R$ directly since $P(x,d)$ is unknown.
    - By minimizing $R_\text{emp}$​, we attempt to approximate $R$, assuming the training dataset is representative of the true distribution.



# Statistical Learning Theory 

- ***Given***:
	- The *VC-dimension* (VC), a measure of the complexity of $H$, that means the flexibility to fit data
- We define ***VC-bound*** in the form :
$$R\leq R_{\text{emp}}+\epsilon\left( \frac{1}{l}, VC, \frac{1}{\delta} \right) $$

Where :
- $\epsilon$ , the VC confidence, is a function that grows with the $VC$ dimension and decreases with higher $l$ and $\delta$ 
- $R_{\text{emp}}$ decreases using complex models, that means with high $VC$
- $\delta$ is the confidence, that rules the probability that the bound holds -> the bound holds with probability $1-\delta$

Intuitions :
- higher $l$ means low VC -> low $\epsilon$ -> bound close to $R$ (it's limited)
- fixing $l$, a too simple model (low $VC$) -> Training Error could be high because the model cannot explain patterns in data -> high $R_{\text{emp}}$ -> **underfitting**
- fixing $l$, high $VC$ -> lower $R_{emp}$ -> $\epsilon$ could grow a lot -> not well bounds -> ***overfitting***

![[Pasted image 20250109154253.png]]



> [!NOTE] Simplifying
> We can make a good approximation of $f$ from examples, provided a good number of data and the complexity of the model is suitable for the task 
> 
> Fit the data as much as possible to avoid underfitting but not too much to avoid overfitting.



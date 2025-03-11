---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
Creation: 2024-12-23
---
***Machine Learning*** (ML), is an area of research combining the aims of creating *computer that could learn* [[Indice - Artificial Intelligence Fundamentals|AI]] and *adaptive/[[Indice - Statistica|statistical]] tools*.
We want machine that learn by themself for analyzing a huge datasets of empirical data to have a *data driven* paradigm.

Machines learn by **training experience** by a long phase of training on a set of data.


> [!NOTE] Definition : Learn
> A computer program is said to ***learn*** from experience $E$ with respect to some class of tasks $T$ and performance measure $P$, if its performance at task in $T$, as measured by $P$, improves with experience $E$.

To design a learning system it's needed a performance measure that's right for that specif problem, a well-representative training set, the target function

Machine learning could have different point of view:
- AI methodology
- Statistical learning
- Computer science method



> [!NOTE] Computational Framework
> Principles, methods and algorithms for learning and prediction:
> - Learning by the system of experience (known data) to approach a defined computational task
> - Build a model (or [[Hypothesis space|Hypothesis]]) to be used for predictions
>   
>   The most common specific framework:
>   
>   Infer a model / function from a set of examples which allows the ***[[Machine learning#Generalization|Generalization]]*** (the capability to provide accurate response on new data)

It's used to solve real-world problem that are difficult to be treated with traditional techniques, for example when data are too difficult to be formalized hand-made, when there's not enough human knowledge or when it's required a personalized behaviour.


Usually we have an input and a task to resolve, but data are noisy and ambiguous to formalize but easy to labeled.

A ML system is able to fit to the known examples and is able to [[Machine learning#Generalization|generalize]] to new data with reasonable accuracy.


![[ML system.png]]



# Formal settings
---
#### **Goal in Machine Learning**
- Approximate an **unknown function** $f(\mathbf{x)}$:
    - $f(\mathbf{x})$: The true function we aim to learn.
    - $d$: The target value, which is derived as $d = f + \text{noise}$
- **Objective**: Minimize the **risk function** $R$ over all data, which measures the true error : $R = \int L(d, h(x)) dP(x, d)$ 
	- $L$ is the [[Machine learning#Loss|Loss function]]
	- $P(x, d)$ is the **probability distribution** of data points $(x, d)$.
	**True Error $R$** : Represents how well $h(\mathbf{x})$ (the model hypothesis) matches the true function $f(\mathbf{x})$ over all possible data.

#### **Search for the Best Hypothesis**

- **Goal**: Find $h \in H$ (a hypothesis in the hypothesis space) that minimizes $R$.

- **Challenge**:
    - The true risk $R$ depends on the **entire data distribution** $P(x, d)$ which is unknown
    - We only have access to a **finite dataset** $TR = \{(x_p, d_p)\}_{p=1}^l$​ , where $l$ is the number of samples
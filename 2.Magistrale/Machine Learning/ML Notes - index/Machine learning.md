---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
Creation: 2024-12-23
---
***Machine Learning*** (ML), is an area of research combining the aims of creating *computer that could learn* [[Indice - Artificial intelligence Fundamentals|AI]] and *adaptive/[[Indice - Statistica|statistical]] tools*.
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


![[Pasted image 20241223101953.png]]


## Data

Data can be *Flat* or *Structured*. 
- Flat as numerical or as the 1-of-k or the 1-hot encoding
- Structured such as lists, trees, graphs, tables

Data have 
- *Noise*, addition information from external factors
- *Outliers*, data values that are not consistent with most observations

To have an optimal input representation for a learning problem we can do the **Feature selection**. With that are selected a small number of informative feature of the data.


## Task

The task defines the purpose of the application, such as the knowledge we want to achieve, understand the helpful nature of the result and the available information.

The task could be:
- ***Predictive***, that approximate a function (Regression and Classification)
- ***Descriptive***, that find subsets or groups of unclassified data (Cluster analysis and Association rules)

Task are of two categories : supervised and unsupervised.

***Supervised learning***: The training examples are labeled data $<\mathbf{x},d>$ for an unknown function $f$. The problem is to find a good approximation of $f$, an *hypothesis* $h$, that can *[[Machine learning#Generalization|Generalize]]*.
	![[Pasted image 20241223103738.png]] ^af8e9d
- ***Unsupervised learning***: the training set is a set of unlabeled data $<\mathbf{x}>$ and the task consists in find natural grouping  in a set of data.
	Examples are: clustering, dimensionality reduction, visualization, preprocessing and modeling the data density
	![[Pasted image 20241223111343.png]]

### Classification task

^ceaf9d

It returns discrete value output.
$f(\mathbf{x})\to \text{class of } \mathbf{x}$

If the number of classes is 2 $f(\mathbf{x})$ is a boolean function and we can say that the problem is a binary classification (*concept learning*), otherwise, if it's greater than 2 is a *multiclass problem*.

It could be view as the allocation of the input in the right decision region.

The possible hypothesis are:
$$h(\mathbf{x})=\begin{cases}
1 \text{  if  } \mathbf{w}^T\mathbf{x}+w_{0} \geq {0} \\
0 \text{        otherwise}
\end{cases}$$
$$h(\mathbf{x})=\text{sign}(\mathbf{w}^T\mathbf{x}+w_{0})$$
these functions are indicators functions of [[Linear models - classification|LTU]]
The LTU allows us to indicate an hyperplane that induces sets of [[Statistical Learning Theory - Vapnik|dichotomies]], that correspond to the number of possible hypothesis $h$ in the *Hypothesis space* $H$.


### Regression task
It returns continuous value output.

The task aim is to estimate a real-value function on the basis of finite set of noisy samples


### Semi-supervised learning
Combines both label and unlabeled examples to generate an appropriate function or classifier

### Reinforcement learning
It's about the adaptation in autonomous systems, in which the algorithm learns a policy of how to act given an observation of the world. Every action has some impact in the environment, and the environment provides feedback that guide the [[Machine learning#Learning Algoritm|learning algorithm]].
That not include step by step examples and it's toward decision making aims.

It's useful in modern AI.

## Model

A model aim is to capture and describe the relationship among the data by a language. The language is related to the representation used to get knowledge.

The model defines the class of functions that the learning machine can implement, *the***Hypothesis space** $H$, that include all the set of function $h(\mathbf{x},\mathbf{w})$, where $\mathbf{w}$ is the abstract parameter.

The principal characteristics of a model are:
- Training examples 
- Target function
- Hypothesis
- Hypothesis space $H$

Exist different types of models such as:
- [[Linear models]]
- [[Symbolic rules]]
- [[Probabilistic models]]
- [[K nearest neighbor regression]]

An other example of model are the [[Neural networks]], capable of approximating complex non-linear relationships between inputs and outputs.


## Learning Algoritm

The learning algorithm is based on *data*, **task** and **model**.

The heuristic is search through the hypothesis space $H$ of the best hypothesis.8
![[Pasted image 20241223130012.png]]


## Inductive Bias
The [[Bias-Variance|Bias]] is a stet of assumptions made in order to set up a model and a learning algorithm. They are the "preferences" that helps tho choose in a restrict space.
It's necessary to:
- define constraints in the model that limit the hypothesis space,***language bias*** (not that you set a limit inside the $H$ but the limit of $H$ itself in the function space)
- define constraint or preferences in learning algorithm/search strategy, ***search bias***
These assumption are strictly need to obtain an useful model with generalization capabilities.

#### Example in discrete hypothesis space
For boolean function, so in the discrete hypothesis space of rules, we ca write down all the possible function with a lookup table.
But the number of them will grow up with the number of input. We cannot figure out what is the right one until we have see every possible input pair. there are a lot of possible function and it's difficult to generalize. We will have $|H|=(2^{2})^{n}$ because we don't have any bias.

If we restrict the type of function, for example considering only the conjunctive function we reduce the dimension of hypothesis space, using a *language bias*.
In fact it becomes: $|H|=3^n$

### Version space
> [!NOTE] Definition : *Consistent hypothesis* 
> A hypothesis $h$ is **consistent** with the training set if $h(\mathbf{x})=d(\mathbf{x})$ for each training example $<\mathbf{x},d(\mathbf{x})>$ in training set.

It's possible to perform a complete search:
- Listing all the possible hypothesis with [[List then eliminate algorithm]], applicable only if $H$ is finite (unrealistic)
- in an efficient way int the biased space with cleverer algorithms for example the [[Candidate Elimination algorithm]].


These algorithms finds the ***Version Space*** $VS_{H,TR}$, that is the the subset of *hypotheses* $h$ that are consistent with all training examples of the training set. 
The version space boundaries are represented by :
- upper bound **G**, the most general hypotheses consistent with the data (low constraints)
- lower bound **S**, the most specific hypotheses consistent with the data

The version space will converge toward the hypothesis that correctly describes the target concept if only if:
1. there're not errors in training examples
2. there some hypotheses $h\in H$ that correct describes the target concept.
If vs converge to an hypothesis means that G and S converge both to the same hypothesis.
If there'are some errors in training examples the VS will be empty.

### Theorem : Unbiased learner
___ 
An unbiased learner is unable to generalize on new instances.

Proof: 
Each unobserved instance will be classified 1 by half of $h \in VS$ and 0 by the other half.

Indeed:
$\forall h$ consistent with $x_{i}$ (test), $\exists h'$ identical to $h$ except $h'(x_{i})<>h(x_{i})$ because if $h\in VS$ then $h'\in VS$
## Loss

The ***Loss*** is how we can measure how good a model generalize. In other words with the loss we can measure the quality of the approximation.

The *Error* or *Risk* or *Loss* is an expected value of a *loss function* above of all examples.
- loss function : $L(h_{\mathbf{w}}(\mathbf{x}),d)$ for a pattern $\mathbf{x}$
- Loss : $\text{Loss}(h_{\mathbf{w}})=E(\mathbf{w})=\frac{1}{l}\sum_{p=1}^l{L(h_{\mathbf{w}}(\mathbf{x}_{p}), d_{p})}$
We use a different loss function $L$ for different tasks.


### Loss for Regression
---

For the regression we use the loss function *Squared error*: $$L(h_{\mathbf{w}}(\mathbf{x}_{p}), d_{p})=(d_{p}-h_{\mathbf{w}}(\mathbf{x}_{p}))^2$$
If we do the mean over the dataset than we obtain the ***MSE***.

![[Pasted image 20241223150518.png]]
![[Pasted image 20241223150534.png]]


### Loss for Classification
---

For the classification we use a loss that measure the classification error into discrete classes:

$$L(h_{\mathbf{w}}(\mathbf{x}_{p}),d_{p})=\begin{cases} 
0 \text{ if } h_{\mathbf{w}}(\mathbf{x}_{p})={d_{p}}\\
 1 \text{     otherwise}
\end{cases} $$

Def.
	The mean over the data set provide the percentage of misclassified patterns.
	E.g. 20 out 100 are misclassified -> 20% error and 80% accuracy 


### Loss for Clustering and Vector quantization
---

For the clustering and the vector quantization we use the *square error distortion* that find the proximity of the pattern to the centroid of  it's cluster.

$$L(h(\mathbf{x}_{p})= (\mathbf{x}_{p}-h(\mathbf{x}_{p})) \cdot   (\mathbf{x}_{p}-h(\mathbf{x}_{p}))$$
where $\cdot$ is the inner product


### Loss for density estimation
---

For the density estimation we use $$L(h(\mathbf{x}_{p}))=-\ln(h(\mathbf{x}_{p}))$$related to maximizing the (log) likelihood function.



The Error is use to adjusting the weights, what we want is minimize $E$ finding the best weights and incrementally we refine them.
One example is the ***Least Mean Square*** ( [[Least Mean Square|LMS]] ) training rule.
## Generalization

Generalize mean give the right result with a model over new data.
We can't generalize if we haven't a bias.

We can see if our model is able to generalize using the ***test set***. (See the [[Statistical Learning Theory - Vapnik]])


### Overfitting
Overfitting is a phenomenon where a model learns to perform well on training data abut it's not capable to generalize on unseen data.
We can recognize overfitting when we have a high accuracy in training but a low one in test, when our model is too complex with a lot parameters relative to the number of data and when it's sensitive to small variation to the training data.

If a model is yo complex, in number coefficients (weights), it's possible that it could learn to complex pattern in the training set that are not useful to generalize.


> [!NOTE] Definition : OVERFITTING
> A learner overfit data if it outputs a hypothesis $h \in H$ having true/generalization error (risk) $R$ and empirical (training) error $E$, but there's an another $h' \in H$ having $E'>E$ and $R'<R$
> 
> So $h'$ is better then $h$ despite a worst fitting



Technique which are used to control overfitting are:
- [[Regularization]]
- [[K-fold - cross validation|cross validation]]


## [[Curse of dimensionality]]

The number of input and output units depends by the dataset, the number of hidden layers and hidden units can bu adjust to generalize better.

---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning]]"
tags:
  - ML
Creation: 2025-01-01
---
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

  

A learner that doesn't make prior assumption regarding the identity of the target function has not the rational basis for classifying any unseen instance.

Bias is not only assumed for efficiency, but it's needed for  the [[Machine learning#Generalization|Generalization capability]]. However it doesn't quantify how good a model generalize.

It's important to characterize the bias in function of the type of the problem we are working on.

## Language and search bias
---

We can distinguish two type of biases: language and search bias. 

Language bias limits the Hypothesis Space $H$. It's done by defining constraints ore rules beforehand, that excluding some possibility.
If it's too restrictive it can happen to exclude the true target function 

Search bias limits the search of the right hypothesis inside the Hypothesis Space $H$. Search bias uses an incomplete search strategy to explore $H$. It relies on strategy like [[Optimization Algorithms]] to find good solution within a vast hypothesis space. 


### Conclusions
---

A learner that doesn't make prior assumption regarding the identity of the target function has not the rational basis for classifying any unseen instance.

Bias is not only assumed for efficiency, but it's needed for  the [[Machine learning#Generalization|Generalization capability]]. However it doesn't quantify how good a model generalize.

It's important to characterize the bias in function of the type of the problem we are working on.
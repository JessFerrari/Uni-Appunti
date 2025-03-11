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



A learner that doesn't make prior assumption regarding the identity of the target function has not the rational basis for classifying any unseen instance.

Bias is not only assumed for efficiency, but it's needed for  the [[Machine learning#Generalization|Generalization capability]]. However it doesn't quantify how good a model generalize.

It's important to characterize the bias in function of the type of the problem we are working on.
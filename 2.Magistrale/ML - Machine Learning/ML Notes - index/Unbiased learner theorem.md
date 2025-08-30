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

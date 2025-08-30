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

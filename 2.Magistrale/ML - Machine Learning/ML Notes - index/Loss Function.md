
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

![[Regression task.png]]
![[MSE.png]]


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
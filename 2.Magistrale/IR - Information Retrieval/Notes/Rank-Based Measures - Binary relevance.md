---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Evaluation]]"
tags:
  - IR
Creation: 2024-10-27
---

To evaluate IR system considering the position of retrieval documents we use rank-based metrics.
These are useful because in some situation we don't need only the document retrieval but also its position.
# MAP
MAP, Mean average precision, measure the average precision on all the relevance document for a query.
To calculate the MAP we have to calculate the Average Precision (AP) for all queries and the do the mean.
It weights each query equally.

$$AP=\frac{1}{R}\sum_{k=1}^NP(k)*\text{relevance}(k)$$
![[Pasted image 20241027165822.png]]
$$AP_{\text{R\#1}}=\frac{1.0+0.67+0.75+0.8+0.83+0.6}{6}=0.78$$
$$AP_{\text{R\#2}}=\frac{0.5+0.4+0.5+0.57+0.56+0.6}{6}=0.52$$
$$MAP=\frac{0.78+0.52}{2}=1.3$$

# Precision@K and Recall@K
We use Precision@k when we don't know the number of relevant documents.

To compute P@k, we need to:
- set a rank threshold $K$, 
- compute the % relevant in top $K$, 
- Ignores documents ranked lower than $K$

$$P@K=\sum \frac{\text{relevant docs in top-K}}{K}$$

In a similar fashion is possible to compute Recall@K but we use the total $N$ retrieval documents as denominator:
$$R@K=\sum \frac{\text{relevant docs in top-K}}{N}$$


These measure don't average well over a set of queries. The total number of relevant documents for a query has a strong influence on $AP@K$ per query.

# MAP@K
It's an evaluating metrics that consider only the first k retrieval documents for each query.
$AP@K$ and $MAP@K$ are largely used for Web Search and Recommender Systems.

$$AP@K(q_{i})=\frac{1}{K_{i}}\sum_{k=1}^KP@K(q_{i})*rel(q_{i},k)$$

Where: 
- $K_{i=\sum_{k=i}}^Krel(q_{i},k)$, number of relevant docs for that query
- $rel(q_{i},k)=\begin{cases} 1 \ \ \text{if item at the }k_{th}\text{ rank is relevant}  \\ 0 \ \ \text{otherwise} \end{cases}$

$$MAP@K(Q)=\frac{1}{|Q|}\sum_{q_{i}\in Q}AP@K(q_{i})$$
MAP@K evaluate both the position and the precision pf retrieval documents on top k elements. High values mean that the system is able to put most relevant documents in higher positions, improving the user experience.
# Mean Reciprocal Rank
This metrics measure how high is the first relevant document in the retrieved list.
It is based on the *Reciprocal Rank* (RR) that is the inverse of the first relevant result's position for a query. If it's in the i's position RR is: $\text{RR}=\frac{1}{i}$.
So : $\text{RR}=\frac{1}{\text{rank}_{i}}$

To calculate the MRR we do the mean RR across multiple queries:
$$\text{MRR}=\frac{1}{|Q|} \sum_{i=1}^{|Q|}{\frac{1}{\text{rank}_{i}}}$$

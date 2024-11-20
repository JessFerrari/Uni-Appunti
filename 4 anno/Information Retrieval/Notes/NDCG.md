---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Evaluation]]"
tags:
  - IR
Creation: 2024-10-07
---
NDCG is a Rank-based metric that consider graduated relevance. That means that the assessments are not binary but is graduated (for example in a scale from 0 to 3).

# CG : Cumulative Gain
First of all is necessary to define a metrics to compute the total relevance of relevant documents given a query. 
To compute that we simply sum the relevances.

$$CG=\sum_{i=1}^n rel_{i}$$
Where $i$ is the position of the document. 
This metric does not considers the position in the ranking list

# DCG : Discounted Cumulative Gain
It's a metric that consider both relevance and position in the list of results.

It is based on 2 assumption:
- the higher relevance documents are more influent than margin relevance documents 
- the low ranked documents are less useful for the user

The discounted cumulative gain give a discount by the position.
Documents that are highly relevant has a greater cost than others.

The typical discount is $\frac{1}{\log_{2}(\text{rank})}$ , that means that with base 2 at rank 4 discount is 1/2 and at rank 8 is 1/3.

The DCG at a level p of ranking is:
$$DCG_{p}=rel_{1}+\sum_{i=2}^p \frac{rel_{i}}{\log_{2}(i)}$$
To give more emphasis to the firsts relevant documents is use this alternative:
$$DCG=\sum_{i=1}^p \frac{2^{rel_{i}}-1}{\log_{2}(i+1)}$$
# NDCG : Normalized Discounted Cumulative Gain
Because the DCG depends by the relevance level of documents is useful normalize the DCG in order to compare performance on different queries.
To normalize we use the IDCG (Ideal Discounted Cumulative Gain), that sorts the ranking list over the relevance assessment and compute its DCG.

$$NDCG=\frac{DCG}{IDCG}$$

The NDCG is $\leq 1$ at any rank position.

## Examples

$q_{1}: (d_{1},2), (d_{2},3), (d_{3},1), (d_{4},2), (d_{5},1), (d_{6},0), (d_{7},1)$
$q_{2}: (d_{1},3), (d_{2},2), (d_{3},2), (d_{4},1), (d_{5},2), (d_{6},1), (d_{7},0), (d_{8},0), (d_{9},1)$
### CG

$CG_{1}=2+3+1+2+1+0+1=10$

$CG_{2}=3+2+2+1+2+1+1=12$

### DCG

- Regular

$DCG_{1}=2 + \frac{3}{\log_{2}2}+\frac{1}{\log_{2}3}+\frac{2}{\log_{2}4}+\frac{1}{\log_{2}5}+\frac{0}{\log_{2}6}+\frac{1}{\log_{2}7} =7.42$

$DCG_{2}=3 + \frac{2}{\log_{2}2}+\frac{2}{\log_{2}3}+\frac{1}{\log_{2}4}+\frac{2}{\log_{2}5}+\frac{1}{\log_{2}6}+\frac{0}{\log_{2}7} +\frac{0}{\log_{2}8}+\frac{1}{\log_{2}9}=8.32$

- Alternative

$DCG_{1}=\frac{2^2-1} {\log_{2}2}+ \frac{2^3-1}{\log_{2}3}+\frac{2^1-1}{\log_{2}4}+\frac{2^2-1}{\log_{2}5}+\frac{2^1-1}{\log_{2}6}+\frac{2^0-1}{\log_{2}7}+\frac{2^1-1}{\log_{2}8} = 9.93$

$DCG_{2}=\frac{2^3-1}{\log_{2}2}+\frac{2^2-1}{\log_{2}3}+\frac{2^2-1}{\log_{2}4}+\frac{2^1-1}{\log_{2}5}+\frac{2^2-1}{\log_{2}6}+\frac{2^1-1}{\log_{2}7}+\frac{2^0-1}{\log_{2}8} +\frac{2^0-1}{\log_{2}9}+\frac{2^1}{\log_{2}10}=13.11$


### NDCG

$sort_{1}= (d_{1},3), (d_{2},2), (d_{3},2), (d_{4},1), (d_{5},1), (d_{6},1), (d_{7},0)$
$sort_{2}= (d_{1},3), (d_{2},2), (d_{3},2), (d_{4},2), (d_{5},1), (d_{6},1), (d_{7},1), (d_{8},0), (d_{9},0)$

- Regular

$IDCG_{1}=3+\frac{2}{\log_{2}2}+\frac{2}{\log_{2}3}+\frac{1}{\log_{2}4}+\frac{1}{\log_{2}5}+\frac{1}{\log_{2}6}+\frac{0}{\log_{2}7}=7.58$

$IDCG_{2}=3+\frac{2}{\log_{2}2}+\frac{2}{\log_{2}3}+\frac{2}{\log_{2}4}+\frac{1}{\log_{2}5}+\frac{1}{\log_{2}6}+\frac{1}{\log_{2}7}+\frac{0}{\log_{2}8}+\frac{0}{\log_{2}9}=8.43$


$NDCG_{1}=\frac{DCG_{1}}{IDCG_{1}}=\frac{7.42}{7.58}=0.989$

$NDCG_{2}=\frac{DCG_{2}}{IDCG_{2}}=\frac{8.32}{8.43}=0.987$

- Alternative

$IDCG_{1}=\frac{2^3-1}{\log_{2}2}+\frac{2^2-1}{\log_{2}3}+\frac{2^2-1}{\log_{2}4}+\frac{2^1-1}{\log_{2}5}+\frac{2^1-1}{\log_{2}6}+\frac{2^1-1}{\log_{2}7}+\frac{2^0-1}{\log_{2}8}=11.57$
$IDCG_{2}=\frac{2^3-1}{\log_{2}2}+\frac{2^2-1}{\log_{2}3}+\frac{2^2-1}{\log_{2}4}+\frac{2^2-1}{\log_{2}5}+\frac{2^1-1}{\log_{2}6}+\frac{2^1-1}{\log_{2}7}+\frac{2^1-1}{\log_{2}8}+\frac{0}{\log_{2}9}+\frac{0}{\log_{2}10}=14.96$
$NDCG_{1}=\frac{9.93}{11.57}=0.858$
$NDCG_{2}=\frac{DCG_{2}}{IDCG_{2}}=\frac{8.43}{14.96}=0.563$

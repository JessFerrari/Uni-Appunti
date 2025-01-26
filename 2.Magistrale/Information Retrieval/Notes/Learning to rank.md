---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
  - ML
Creation: 2024-11-11
---
Reference: [Efficient and Effective Tree/based and Neural Learning to Rank](https://arxiv.org/pdf/2305.08680)

[[4 anno/Machine Learning/Machine Learning]] transformed how we approach to [[Document Ranking Problem]], from [[Statistical retrieval]] to Learning to Rank (LTR).

### Motivation
Statistical retrieval separate the representation of queries, documents and representation of mixed query and documents (such in [[BM25 (Best Matching 25)|BM25]]). With LtR we want to create an aggregation function $f$ that can be used to rank.
To do thar we need a strutturate framework that links together all the parts.

This framework comprises of two distinct algorithms:
- [[Top-k Retrieval]], which finds a subset of $k$ documents that are the the most relevant to a query
- [[Ranking models]],which order the documents in the top-k set.

In LtR the ranking phase uses an often expensive function that was trained using [[4 anno/Machine Learning/Machine Learning#^af8e9d|supervised learning]] or [[Online learning|online learning]] methods.
While, the retrieval algorithm solves a form of the [[Maximum inner product search problem|maximum inner product search problem]] (MIPS). 

In dense retrieval, retrieval is often an approximate [[Nearest Neighbor]] search while ranking is the identity function or a complex learnt functions such as [[Decision forest]] or [[Deep learning]] methods.

![[Pasted image 20241111120523.png]]


## [[Efficiency]] in LtR

The question of efficiency gained increasing significance with the LtR whose require large amount od computational power.
The training of such models is expensive because we want we must often learn groups of hundred ti thousands off deep decision trees sequentially with gradient boosting, which each node in every tree requiring q search in the feature space. To become accurate these models need to be trained on vast amount of data, often represented as complex features that are in turn costly to compute. Also inference is computationally intensive because estimating the relevance of a single document to a query requires the traversal of paths, from roots to leaves, of every decision tree in the model.

## Ranking algorithm

A ranking algorithm it's a function of a set of documents and a query. It's simplicity or complexity is determinate by how we represent documents and queries.

Important to ranking algorithm is the way how query and documents are ranked. We know that queries and document could be [[Natural Language|natural language]] texts and that they can be ranked considering them such vectors in the [[Vector space model]]. So the can be represented in the [[Bag of Words model|bag of words model]] and we can using techniques such as the [[TF-IDF (Term Frequency-Inverse Document Frequency)|TF-IDF]] and [[BM25 (Best Matching 25)|BM25]], that considers term occurrences. 

Also the structure of the documents can be important, in particular in web search context, in which we consider hyperlinks between pages and fields, such as the title and sections, that can give as information about the document itself.

As the size and complexity of query and document representations grows is impractical to hand-craft a ranking function and ineffective to use basic similarity measures.
It is rather more practical to view the ranking problem as [[4 anno/Machine Learning/Machine Learning#^af8e9d|supervised learning]] task. 
![[Pasted image 20241111170320.png]]

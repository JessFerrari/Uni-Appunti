---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Weighting Models]]"
tags: 
Creation:
---
## What is ?
---
---
--- 

In the vector space we can measure the relevance of a document to a query using a similarity measure between query and document vectors, such as [[Cosine similarity]] or inner product.
Alternatively, because each vector is a distribution over a vocabulary, we may use a probabilistic approach based on language models to measure query-documents similarity.

In either case, the ranking function computes the similarity scores for pairs of query and documents vectors and sorts the document in decreasing order of similarity.  ([[TF-IDF (Term Frequency-Inverse Document Frequency)|TF-IDF]],[[Weighting Models]],[[Weighting models-Ranking and relevance]], [[BM25 (Best Matching 25)|BM25]])


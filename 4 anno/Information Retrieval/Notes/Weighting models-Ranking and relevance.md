---
Subject: "[[Indice - Information Retrieval|IR]]"
tags: 
Creation: 
Chapter: 
Papers: 
Slide:
---
[[Boolean Model|Boolean queries]] often result in too few (AND query) or too many (OR query) results.
Rather than a set of documents satisfying a query expression, in *ranked retrieval*, the system reorders the top documents in the collection for a given query. The query in not an expression of boolean operator but is free text, compose by a single word or multiple words in natural language.
In this model large results set are not a problem and we just show the top-k elements to the user.

The goal is return in order the documents. A first approach could be assign a score, say in [0, 1], to each document given a query. But we need a technique to assign the score.


## Jaccard coefficient
A first technique is the Jaccard coefficient that is commonly used measure of overlap of two set A and B.
We have three cases:
1. $\text{jaccard}(A,B)=|A\cap{B}| / |A\cup B|$
2. $\text{jaccard}(A,A)=1$
3. $\text{jaccard}(A,B)=0 \ \text{ if } A\cap{B} =0$

This method assign always a number between 0 and 1.

Example:

-> Query  : ides of march
-> doc1    : Cesar died in march
-> doc2   : the long march


$J1 = 1/(3+4-1)=\frac{1}{6}$
$J_{2}={1} / {3+3-1}=\frac{1}{5}$


## Term frequency
The problem of this approach is that doesn't consider the *Term frequency*, that is how many times a term occurs in a document.
In a ideal model the more frequent should have the higher score and rare terms are more informative than frequent terms.
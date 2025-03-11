---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: 
tags:
  - IR
Creation: 2024-10-14
---
There're different types of queries: *Conjunctive (AND)*, *Disjunctive (OR)*, *Negative (NOT)*.
Maybe we are searching a precisely, so we need the *phrase search*.
In this way we can simplify the user query.

The [[Search Engine|search engine]] can add some words like synonymous or similar words without accent and in this way the user receives the wrong result. 

We use two techniques to scan the posting list: ***TAAT*** e ***DAAT***

# TAAT
That means : Term At A Time 

That consists in processing the posting list one query at a time.
It maintains an accumulator for each result document with a value/score.
The score of each document is update with the current term.

We scan each list separately.

E.g.
	![[Pasted image 20241014010801.png]]
	we scan the first list and write the accumulators for each term. The we scan the second one and update every terms of accumulators.
	![[Pasted image 20241014010935.png]]

The accumulators can be a [[Tabella ad accesso diretto|direct access table]] or an [[Hash table|hash table]].
If we need every document that has a specific term we do the AND, we take the term that has the accumulator like the number of document. For have at least one document with a specific term we do the OR, and we chose the one who has at least one in the accumulator.
When we touch a document we don't know if is the final score, because maybe the term occurs in an another document.

For NOT query we can increase the score only if the term is not contains in a document.

PROS:
	- Easy to implement (just use $next_{t}()$) 
CONS:
	- A lot of cache misses because many accumulators (jumps in memory) (A LOT OF ACCUMOLATORS)
	- no possibility of skipping docIds for selective queries
	- random position of results


If we use [[BM25 (Best Matching 25)|BM25]] we don't store a counter but the partial contribution. Than if we sort them we can obtain the top one.
# DAAT
That means : Document At A Time

That consists in scan the posting list of all the query terms in parallel.
It computes score when the same documents is seen in one or more posting list.

The advantage is that many posting list are scan simultaneously and it maintains a sorted list of results.
	E.G. OR query
	![[Pasted image 20241014011707.png]]
	OR query is expensive because we touch al the posting.

This algorithm is like the *Merge* of [[Mergesort|mergesort]] to find the union of the document.
When two number are the same we can continue together, otherwise go before the small one.

E.g. AND query
	![[Pasted image 20241014011926.png]]
	The AND query with this algorithm is also expensive because we touch all the posting lists. We are storing only te documents that contains both of terms.

To advance in AND, to have better performance we can advance of some position grater than one. One method is find the same number with a [[Binary search|binary search]].
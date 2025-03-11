---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
Creation: 2024-09-18
Slide: "[[01-Evaluation.pdf]]"
---
Evaluate a [[Search Engine|search engine]] means that we can say how effective is an IR technique in a specific application, based on how fast it index a collection, how fast does it search and how good are the information that it retrieved.

It is necessary to demonstrate the performance of a technique over another.

With evaluation we want to say how happy is a user with search engine experience.
We can say that if :
- the search results are clicked a lot
- the user buys after using the search engine 
- a user return after a period of time 
- for the dwell time, that is the amount of time in which the user spent on the result after clicking on it

## Measuring relevance 

To measure the effectiveness of results we need three elements:
1. A document collection
2. A test suite of queries
3. A set of relevance judgements

***Relevance judgements*** are binary assessment of either *relevant* or *non-relevant* for each pair query-document. 
That is the simplest way to doing this but it has some issues such as to many judgments.
E.g. 
	5M docs, 50K queries
	$50Milion*50K=2.5*10^{11}=0.25*10^{12}=\frac{1}{4}$trillions judgments 
	if a judgment took 2.5sec for a human we need $6.25*10^{11}$seconds for all judgements, $\sim 170Mh / person$
For using this way we have to limit the numbers of documents.


Relevance is assessed relative to an information need, not a query.


For standardize the way to evaluate search engines exist the [[TREC]], a conference which has this aim.
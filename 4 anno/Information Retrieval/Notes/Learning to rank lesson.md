---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
  - ML
  - "#lecture"
Creation: 2024-10-30
Chapter: 
Papers:
---

title, text, body and hyperlinks. are use anchors for linked pages with hyperlinks.
If I have multiple doc that point to my doc i can use them to describe my document.
Additional information can be used such as click, page rank, ecc.
For queries is important also consider user information such as the user habits ore profile information.

We need to build a representation of doc and query to compute the rank.
From ML comes solutions for learning a function $f$ to rank.


### [[4 anno/Machine Learning/Machine Learning]]
--> qui ha iniziato a spiegare in modo generale il ML non scrivo
--> ha fatto pure una discussione sulla terminologia riguardate classificazione (mapping in classes) e regressione (mapping to real number)
--> ha parlato della fase di training a di test. fa esempi alla lavagna del tipo :
	Data -> ML alg. -> Model. Dopo: Nuovi esempi -> model
	Training offline, Test online
-->Parlato di cosa vuol dire learning

## Learning to Rank (LtR)

Is a different problem from [[4 anno/Machine Learning/Machine Learning#Classification task|classification]] and [[4 anno/Machine Learning/Machine Learning#Regression task|regression]].
The instance are query and documents. We ant do a representation of our task. So we use features from our instance.
We want also supervision, that is the risultato aspettato, che nel nostro caso è il rank ossia la rilevanza del documento.

$$\forall q\in Q:\{d_{1},\dots,d_{n} \} \text{ assesment of doc for a query} 
\ \forall d \text{ is given a rank} $$
OUR supervision is (q,d)={0,1} or (q,d)={0, ..., 4} that said if a document is good or not.

So a query instance could be $(q, d, rel)$ ->basic way.
I can use $(q, d_{1}, d_{2})$ and we want see where the model put $d_{1}$ wrt $d_{2}$ , given 2 documents, $d_{2}$ negative and $d_{1}$ positive there's more information than before and i want that the positive is before of the negative in the list

I can give also the complete list of relevance $(q, d_{1}, \dots, d_{m})$, i exploiting all the knowledge
3 different methods: 1 doc, a pair , all the list as a label of data.
To give the problem to ML algorithm i need a representation of my knowledge.
I have three possible representation:
- doc rep
- query rep
- mixed query-doc rep : means something that unisce entrambi, as TF-IDF and BM25. thy are signal of relevance that links together and produce some more sophisticated thing.

A document vector , inside numbers from different representations (BM25, cosine, tf-idf,...)->so $v$ is the representation of (q,d)
Il vettore è composto da tutti i diversi tipi di rappresentazione e tipo ad un certo indice c'è la bm25
L'input quindi è essenzialmente composto da:
- for 1 ex. : $(v, \text{rel})$ 


(proximity signal??)

Input = feature vector which contains representation of q, d and $(q,d)$. 
Label = human assessors (explicit feedback) and login information (implicit feedback)

We can't use the ML methods on inverted index because is very expensive. from id we appy bm5 or tfide to give a set of doc and then apply the ML f(q,d)

The ml function works on the vector representation  so we need to build a v representation on the the set of doc. some information about doc can be compute offline and stored in disk, and the algorithm just fetch these info for create the vector. from query build the q rep. and from doc set and q. we build the q,d.
It's all about the budget.

(is cascading of modules working on a set of doc.)

A training corpus is a triplet $(q,d,r)$ , where $r$ is the relevance that could be for ex. binary.

$\omega$ is used lo capture the locality of words in query representation, proximity inf. (how query is spread in the doc.)
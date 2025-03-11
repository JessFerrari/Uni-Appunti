---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Indexing a document]]"
tags:
  - IR
Creation: 2024-10-07
---
We use the *inverted index* to improve space efficiency: see what position of the first non zero entry and write down the index of it for each row. In this way we can transform a sparse matrix in a list.


The inverted index is an index that stores a mapping between terms and the documents they appear in.

It's a fundamental data structure in typical search engine indexing algorithm.

The goal is to *optimize the speed of the query* in the work of find the documents where a set of words occur.

Basically we have lists of indices.


These are three documents for the example of inverted index.
![[Pasted image 20241009170648.png]]

In this picture is represented the inverted index for a [[Boolean Model|boolean retrieval]], the model in which there's no a score for documents.
From the 3 document we can produce a dictionary with terms from all the documents. 
Every term of the dictionary is connected to a list with the numbers of document in which is in.
in this case the **posting list** is a list that contains the document identifier that contains that term.

![[Pasted image 20241007161343.png]]

Here is the inverted index for [[BM25 (Best Matching 25)|BM25]]. In this model we use a ranking and what we need is store also the frequency of terms. In the dictionary, the orange number is the $df_{t}$, the number of documents containing one or more occurrences of the term $t$ and the green number is $F_{t}$ , the number of occurrences of term $t$ in the collection.

In *Posting list* we are storing the frequency of term $t$ in the document $d$ (is simple to store the frequency and not the score because its simply calculable from frequency and the frequency is more easy to represented.)
![[Pasted image 20241009170126.png]]
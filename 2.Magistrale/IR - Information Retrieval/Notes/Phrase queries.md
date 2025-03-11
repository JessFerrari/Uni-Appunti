---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Indexing a document]]"
tags:
  - IR
Creation: 2024-10-22
---
A phrase query is a specific type of query in which is important the position of the terms. For example we want to find "Information retrieval" and we want information before retrieval.
In the posting list we do another list for each document inside in which we store the position of the term occurrences.
![[Pasted image 20241022114958.png]]
In this way we search before the document that contains both and then, in the sublist of each of these document, we looking for an occurrence of the term information at the position $p$ and one of retrieval at the position $p+1$.
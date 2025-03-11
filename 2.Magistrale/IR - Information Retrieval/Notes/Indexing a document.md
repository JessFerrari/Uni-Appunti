---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
Creation: 2024-10-09
Chapter: 
Papers: 
Slide:
---
RECAP:

The documents collection has been tokenized an it can be represented as a matrix in which rows are terms and columns are documents.
Every element of the matrix says if a term is present on the document with a score. This score can be proportional to the number of the term in the document and the frequency of the term in the collection ([[TF-IDF (Term Frequency-Inverse Document Frequency)|TF-IDF]]).

The number of columns is in the order of million and the number of rows is in the order hundred million.

When a query arrive we transform it in the form of a column of the matrix.
Answer at the query means compare the query vector with the documents vectors and say haw good is a document for a query. For doing that we use the dot product between vectors, that is the product between non zero element in both vectors and then do the sum. But the most of elements are zero.

 With this approach we have two principal issues: it's **Space Inefficient** because is a very sparse matrix, and also is **Time Inefficient** because need to process *ONLINE* the whole collection.
 
![[Pasted image 20241021110121.png]]

We want indexing the document to build [[Inverted Index|inverted index]] to [[Query processing|processing a query]]. 


- Space efficient : see what position of the first non zero entry and write down the index of it for each row -> [[Inverted Index]]
---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
Creation: 2024-09-20
---
Information retrieval (IR) is the process of obtaining relevant information from a large repository of unstructured data, such as documents, web pages, or multimedia content, base on a users's query.
It involves *searching* and *indexing* data to find the most relevant pieces of information. 
It's a fundamental component of technology like [[Search Engine|search engine]], recommendation systems and digital assistant.


The key components of IR are:
- [[Document representation]] : IR system process and represent data in a structured way to make search *efficient*. It typically involves tokenization, parsing and indexing.
- [[Query processing]] : When a user inputs a query the system interprets it. For doing it, the query is breaking into keywords or semantic element to match it with indexed data
- [[Weighting models-Ranking and relevance]] : The core of IR is determining which documents are relevant for the user's query. It involves ranking algorithms that score the relevance of each result based on factors like keywords frequency, semantic matching or use behavior.
- [[Evaluation|Evaluation metrics]] : Common metrics to assess IR system performance include *precision*, how relevant te result are, and *recall* (how many relevant document the system was able to retrive).


IR systems have two principal goals: *Effectiveness* and *Efficiency*

The Effectiveness refers to how well the IR system retrieves relevant documents in response to a query. It's measure with metrics like precision and recall ([[Evaluation|evaluation metrics]]) and user satisfaction.
The focus is on retrieving high-quality, accurate results that meet the user's information needs.


The Efficiency involves the system's ability to retrive result *quickly* and handle *large-scale data processing* in a tamely manner. It's concerned with response time, resource usage (e.g. CPU, Memory, ...) and scalability, ensuring that the user receive their result without long delays, even as the amount of data grows.


### Language
Language in IR is complex because it includes element like synonyms, homonyms, syntax and semantic. These properties influences how well a system can retrieve relevant documents.

Language properties can either help or hinder retrieval. For example, if a system can handle synonyms (e.g., "car" and "automobile"), it improves the chance of retrieving relevant documents. Misunderstanding these properties can lead to irrelevant results.

### Retrieve a piece of text
Retrieving a piece of text means identifying and returning documents or passages that match the user's query, based on the relevance of their content to the query terms.

### Document rapresentation
Documents can be represented in different ways for retrieval, such as using [[Bag of words|bag-of-words]] models (where documents are treated as a collection of words without considering order), [[Term frequency vectors|term frequency vectors]], or more advanced embeddings. 
The way documents are represented influences how well an IR system can match them to queries.

### Retrieval models

These models define how the system retrieves and ranks documents based on a query:

- **[[Boolean Model]]**:  
    This model uses strict binary logic (AND, OR, NOT) to match documents to a query. A document either matches or it doesn't—there’s no ranking based on relevance.
    
- **[[TF-IDF (Term Frequency-Inverse Document Frequency)]]**:  
    A statistical measure used to evaluate the importance of a word in a document relative to a collection (corpus). Words that appear frequently in a document but rarely across the corpus are given higher weights, helping the system retrieve more relevant documents.
    
- **[[BM25 (Best Matching 25)]]**:  
    BM25 is a more sophisticated ranking function that builds on TF-IDF, adjusting for document length and term saturation. It uses parameters to fine-tune how term frequency and document frequency affect the ranking of documents.
$$
	scored(q,d)=\sum_{i=0}^{|q|} idf(q_{i})*\frac{tf(q_{i},d)*(k_{1}+1)}{tf(q_{i,d})+k
	*(1-b+b*\frac{|d|}{a v g d l})}
$$

---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
Creation: 2024-09-20
---
An ***SEARCH ENGINE*** is a software system that *indexes* and *retrieves* information from the web or other data sources in response to user queries.
It ranks result based on relevance, using algorithms and ranking models to present the most useful content.

This is the architecture of a search engine:

![[Pasted image 20241007155946.png]]

1. **Query**: This is the user's input in the form of a search query. This define the terms to search.
2. **Expanded Query**: The query may be expanded with synonyms or other related terms to improve the search results.
3. **Query Processing**: The search engine processes the query, which may include tasks such as tokenization, spell correction, and other linguistic analyses.
4. **[[Inverted Index]]**: An index of all the documents (or web pages) in the search engine's database, mapping terms to the documents in which they appear.
5. **Feature Lookup and Computation**: The system extracts features of the documents that match the query. Features could include relevance signals like term frequency, page rank, etc.
6. **Learned Ranking Function**: This is the core ranking mechanism, often powered by a machine learning model, which ranks the search results based on the computed features.
7. **Learning-to-Rank Model**: A model trained on data that helps the search engine learn which documents should appear higher in the search results.
8. **Document Features Repository**: A storage system for various features and metadata of documents, which are retrieved during the search process.
9. **Training**: A process where the search engine learns from past data (user interactions, relevance feedback) to improve ranking.
10. **Document Collection**: The database of documents (web pages, files, etc.) that the search engine indexes.
11. **Indexing**: The process of creating and updating the inverted index with new or modified documents.
12. **Feature Processor**: Extracts and processes the features from documents to make them usable for ranking.

The architecture integrates both offline and online processes:

- **Offline**: Indexing, feature processing, training the ranking model.
- **Online**: Query processing, feature lookup, and ranking the results in real-time.

The ranked results are displayed to the user on the search engine results page (SERP).
---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
  - ML
Creation: 2024-11-20
---
With [[learning to rank]] it's possible to create a [[machine learning]] model which ranks documents using a [[Ranking models|ranking method]], i.e. [[BM25 (Best Matching 25)|BM25]], to sort them, trying to maximize a [[ranking metrics]], such as the [[NDCG]].

Starting from a dataset, which is composed by queries, documents and features, te objective is **training** the model (off-line process) and **ranking** the documents (inference, online process).


We use [[gradient boosting forest decision tree]] for the learning to rank model.

At the end of training time we produce a forest and at the end of each inference time we go thought the whole forest.
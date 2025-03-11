---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Evaluation]]"
tags: 
Creation: 2024-10-27
---
The users need must be translated in a query and the relevance is assessed with respect to the user need and not the query. 
With *binary assessment* we refer to a binary way to evaluate the relevance of documents. The system evaluate as relevant or non-relevant a document for a query.

The principal metrics are *precision* and *recall*.

![[Pasted image 20241027155623.png]]
# Precision
Precision is the fraction of retrieved documents that are relevant: $P(\text{relevant retrieved}|\text{retrieved})$:
$$P=\frac{tp}{tp+fp}$$
# RECALL
Recall is the fraction of relevant document that are retrieved: $P(\text{relevant retrieved}|\text{relevant})$:
$$R=\frac{tp}{tp+fn}$$
# F-Measure or F-score
The F-measure is the [[Media armonica|harmonic mean]] of precision and recall:
$$F=\frac{1}{0.5 \frac{1}{P} +0.5 \frac{1}{R} }=2\frac{PR}{P+R}$$
The harmonic mean is always less than or equal to the [[Media aritmetica|arithmetic mean]] and the [[Media geometrica|geometry mean]].
With the F-measure we can compute a trade off between them because when precision and recall are very different numbers, F-measure is closer to the minimum.


We can have a weighted F-measure if use weight instead of 0.5 in the formula.
if we use $\alpha$ to $P$ and $(\alpha-1)$ to $R$, with $\alpha =\frac{1}{(1+\beta^2)}$, we obtain:
$$F_{\beta}=\frac{1}{\alpha\frac{1}{P}+(\alpha-1)\frac{1}{R}}=(\beta^2+1)\frac{PR}{\beta^2P+R}$$
With $\beta>1$ emphasize recall and with $\beta<1$ emphasize precision
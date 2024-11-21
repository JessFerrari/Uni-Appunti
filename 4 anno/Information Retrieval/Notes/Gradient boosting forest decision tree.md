---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Learning to rank]]"
tags:
  - IR
  - PEA
  - ML
Creation: 2024-11-21
---
We use [[Ensemble]], in particular the [[Gradient Boosting Machine]] with [[Decision trees]]  forest. The score of a document is made by the sum of the partial score of each tree.

The number of decision trees is thousand up to 20 thousands, and each tree is a small model that have from 16 to 512 leaves.
The number of features involved depends on the ask but usually is about 100 up to 2000.
![[Pasted image 20241121155135.png]]

Here the [[decision trees]] are small trees in which each node has a threshold and a feature. A document is associated a score of a feature and from the root we arrive at leaves.
Potentially every node have much than a feature, it depends on the training phase.
![[Pasted image 20241121162108.png]]
We stop when we arrive at one leaf and we have a score for a document.

If the feature score is greater than the threshold we go to the right if is less than it we go to left. 
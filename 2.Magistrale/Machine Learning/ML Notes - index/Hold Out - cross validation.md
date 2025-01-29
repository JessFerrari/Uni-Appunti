---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Validation]]"
tags:
  - ML
  - dataset
Creation: 2025-01-09
---
For the basic setting, we can simply divide the dataset $D$ in three sets: Training $TR$, Validation $VL$ and test $TS$, and use $TR$ for training, $VL$ for model selection and $TS$ for model assessment.

We can call te union of $TR$ and $VL$ *Development/design set*.

![[Pasted image 20250109160508.png]]


Usually we don't have too many data to to that, and for this we use [[K-fold - cross validation]].


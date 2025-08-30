---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Machine learning]]"
tags:
  - ML
Creation: 2025-03-04
---
## Data in machine learning

Data can be *Flat* or *Structured*. 
- Flat as numerical or as the 1-of-k or the 1-hot encoding
- Structured such as lists, trees, graphs, tables

Data have 
- *Noise*, addition information from external factors
- *Outliers*, data values that are not consistent with most observations

To have an optimal input representation for a learning problem we can do the **Feature selection**. With that are selected a small number of informative feature of the data.

## Concept representation
---

There are two ways to represent data:
1. *Symbolic representation*: which use *one-hot encoding*, that is a sparse vector with a single position set at 1, and all the others at 0. 
   Each vector is equidistant from others of $\sqrt{2 }$ and it's not possible to define relationships between them.
2. *Distributed representation*: that use dense encoding where all vector's elements can assume a continuous value, allowing a more flexible representation.
   The distance between vectors depends by the representation and it's possible to capture similarities.

The distributed representation is more efficient because needs less values to represent concepts. If with one-hot encoding we need *$n$* distinct values to represent a concept, with the distributed you just need one vector of k position o represent $k^n$
concepts.
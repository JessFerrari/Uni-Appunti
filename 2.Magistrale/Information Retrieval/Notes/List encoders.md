---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Data compression]]"
tags:
  - IR
Creation: 2024-10-27
---
The problem is that we want to compress a strictly increasing list of integers $L=[x_{1},\dots,x_{n}]$ where $x_{1}>0$, $x_{i}<x_{i+1}$ and $x_{n}\leq U$. The value $U$ is called the *universe size*.
Some compressor compress $L$ directly and others need to transform $L$ into a list of d-gaps.

For *compression* we mean that we can exploit regularities within the entire list. for example, runs very small values because same domain contains the same terms.
![[Pasted image 20241027024331.png]]
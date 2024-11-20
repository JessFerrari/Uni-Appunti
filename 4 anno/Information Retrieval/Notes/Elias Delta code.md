---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Encoding, representation and decodability]]"
tags:
  - IR
  - inverted_index
  - compression
  - encoding
Creation: 2024-10-27
---
The idea is make $bin(x)$ decodable by prepending a code for its length. we represent $|bin(x)|$ with Elias Gamma writing bin(x) without the most significant bit because are all 1. 
Is like Gamma but instead of using unary we use gamma for the length.

Gamma is better for small number but when numbers increase delta works better.
![[Pasted image 20241027122526.png]]
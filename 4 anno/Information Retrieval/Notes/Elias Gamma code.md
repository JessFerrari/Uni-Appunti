---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Encoding, representation and decodability]]"
tags:
  - IR
  - inverted_index
  - encoding
Creation: 2024-10-26
---
The idea is make $bin(x)$ decodable by prepending a code for its length and represent $|bin(x)|$ with unitary.

for $\gamma(5)$ we think:
- how 5 is represent in binary : 101
- take its length : 3 
- represent the length 3 in unitary code : 110
- then the first part of $\gamma(5)$ is 110 and then 101
since the significant bit of b(x) is 1 we leave it for every one, so $\gamma(5)=110 01$


esempio $\gamma(7)$
- 7 in b(x) = 111
- length = 3 -> 110
- 11011
- ![[Pasted image 20241027122553.png]]
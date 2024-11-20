---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Data compression]]"
tags:
  - IR
Creation: 2024-10-26
---
# Encoding Integer

In our task we have integer, for example for index, frequency, TF ecc..

Problem : Given an integer $x>0$ we want to design an algorithm that represents $x$ as few as possible bits.

The bit-string representing $x$ according to the chosen code is called the *codeword* of $x$ and indicated with $C(x)$.

A sequence  $S=x_{1},\dots,x_{n}$ consisting of $n$ integers will be coded as the concatenation of the codewords assigned to $x_{1},\dots,x_{n}$, i.e.: $C(x_{1}),\dots,C(x_{n})$

The codes that always assign the same codeword $C(x)$ to $x$ are called *static*, regardless the sequence $S$to be coded.

![[Pasted image 20241026185323.png]]
This is the representation of *delta encoding*, or *d-gap encoding*. Instead of storing each integer directly, delta encoding stores the difference between each consecutive pair of numbers.
We use this type of compression because the different between numbers is often smaller than original numbers, so it occupy less space. Delta encoding is useful in scenarios like storing [[Inverted Index|inverted index]].

# Binary representation

$k$ bits are sufficient to represent any number $x$ in $0\leq x\leq 2^k$.
$\text{bin}(x)$ is the binary representation of $x$ and $|\text{bin}(x)|$ is the number of bits necessary to represent $x$, i.e. $\lceil \log_2(x + 1) \rceil$.

When compressing data, especially when dealing with binary codes, each number $x$ is mapped to a binary codeword. For $x>0$, the binary codeword $B(x)$ is defined as $bin(x-1)$. This shift the mapping by one, effectively creating a more compact binary encoding.

![[Pasted image 20241026195002.png]]
In the example in the table for $x=3$ we have that $B(x)=\text{bin}(x-1)=bin(2)=10$
The length of a codeword $C(x)$ for $x>0$ is bounded below by $\lceil \log_2(x ) \rceil$. This bounds implies that you cannot have a shorter representation than the standard binary representation length, which is consistent with the codeword $B(x)$ length for each $x$value.
$|C(x)| > ⌈log2(x)⌉ = |bin(x − 1)| = |B(x)|$

When we store the information with d-gap encoding we store it in binary but there will be different ways to decode it. this is an example:
![[Pasted image 20241026222251.png]]

# Unique Decodability
![[Pasted image 20241027121729.png]]
We use the **Unique decodability** for disambiguate the decoding. A way is to have prefix-free code. A code $C$ is said to be prefix-free when there are no $C(x)$ and $C(y)$, with $C(y)>C(x)$ for which $C(x)=C(y)[1:C(x)]$.

If a code is not prefix-free the codeword of a number could be the prefix of another codeword. 
So we can decode: $011101$ in different ways such as 1432, 1812, ... 
If we decide a prefix-free code it couldn't happen because codewords are unique. In this case $011101$ is meaning 26.
![[Pasted image 20241026223226.png]]
This is not the only way and this is the worst in term of space.
The goal is design an unique decodable code with space close to $|B(k)|$.


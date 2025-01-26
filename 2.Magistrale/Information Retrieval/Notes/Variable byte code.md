---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Encoding, representation and decodability]]"
tags:
  - IR
  - encoding
  - compression
Creation: 2024-10-27
---
The ideas is the codewords are byte-aligned rather than bit-aligned. 
Reading bits is expensive and in this way we can reduce the shift operations.
Byte-aligned codewords favor implementation simplicity and encoding/decoding speed.

$bin(x-1)$ is split into a suitable number of bytes: for each byte, 7 bits are allocated for the representation of $x$ itself (data bits), and 1 bit (the control bit) is used to signal continuation or the end of the stream of bytes.

![[Pasted image 20241027022616.png]]

The control byte is 0 if is the last, 1 otherwise:
![[Pasted image 20241027023317.png]]
---
Subject: "[[Indice - Parallel and Distributed System|SPM]]"
Super Topic: "[[Parallel computing]]"
tags:
  - SPM
Creation: 2025-02-25
---
Parallel architectures helps us to solve problem in scientific and engineering application, assicurando:
- *Scalability*: to enable scale-out by adding more nodes to the system
- *Fault tollerance*: to ensure *reliability*. If one node fail, other nodes can still be used.

Parallelism is applied at level of system design (in the part where you choose microarchitecture, memory systems, ecc.)

# How to classify parallel architectures

To classify parallel architectures we take in consideration two main aspect that characterize parallel architectures:
1. The system architecture of the single node 
2. The interconnection network connecting multiple nodes forming the parallel system

But there's no a sigle classification because there are too many feature and is difficult to choose a main criteria. The most famous are:
- *Flynn's taxonomy* : nowadays not so representative
- *Memory organization*: shared memory, distributed memory or hybrid system
- *Core count & processing model*
- *Interconnection network*

## Flynn's Taxonomy (1966)
---
It's an old Classification based on the number of *instruction* and *data stream*.

1. SISD : Single Instruction Single Data. Not parallel but only sequential
2. [[SIMD]] : Data parallelism because the parallelism depend by the granularity of the data. PEs works independently relays with how GPUs works  
3. MISD :
4. MIMD : 


## Classification based on the memory systems organization
---
24:00 lezione 3 non sono riuscita a seguirlo

1. Shared Memory (SHM)
2. Distributed Memory

33:00 pure non riesco a seguire stamani
36:00 NUMA MULTIORE EXAMPLE


## Classifications based on the cores count
---

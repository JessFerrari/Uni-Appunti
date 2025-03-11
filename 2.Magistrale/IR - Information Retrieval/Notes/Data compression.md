---
Subject: "[[Indice - Information Retrieval|IR]]"
tags:
  - IR
  - inverted_index
Creation: 2024-10-26
Chapter: 
Papers: 
Slide:
---
The objective is compress the [[Inverted Index|inverted index]] in order to reduce its size to enable better storage efficiency and faster query processing. 
It's essential to :
- *Reducing storage requirement*
- *Faster disk I/O operations and query processing*
- *Better cache utilization*
- *Efficient list processing for query execution*
- *Lower network bandwidth* 
- *Minimizing redundancy*

# Motivation for data compression

When we store big dimension data collections we need a lot of space to store the index. To store it we use datacenters with a lot of machines using sharding.

Sharding is a technique used in [[Indice - Basi di dati|database systems]] and [[Search Engine|search engine]] to *distribute data* across multiple physical node of a [[Datacenter|datacenter]]. It's essential for handling massive document collections and improving query performance without using disk.
A large collection (dataset) can be handle by splitting a massive index in smaller and more manageable pieces, called *shards*, and the query is also process in shards.
Typically each shard is stored and processed on a separate node which distributes the workload across a cluster of machines.


Sharding is good for:
- **Scalability** (distributed data and scale horizontally) : as the document collection grows, a single machine can't handle the load. Sharding distributes the data, allowing the search engine to scale horizontally by adding more nodes.
- **Performances** (Parallel query processing) : By distributing the data across multiple nodes, sharding can significantly reduce the load on any single server, resulting in faster query execution and improved overall system performance.
- **Fault tolerance** (Replicas on different nodes) : Sharding with replicas enhance fault tolerance. If one node fails. the data is still available on other replicas.

![[Pasted image 20241027121228.png]]
![[Pasted image 20241026153100.png]]
In this picture is represent a *sharded* and *replicated* architecture, which processes queries over a distributed set of index servers.

The full [[Inverted Index|inverted index]] is divided into smaller parts called *shards*. Each of them represents a subset of the full data, containing only a portion of the documents. Each *shard* is duplicated across multiple servers called *replicas*, that improve the fault tolerance.

The *Broker* is responsible for routing the query to multiple index servers that each contains shards of the full index. 
It acts as an intermediary, ensuring that the query is processed by the appropriate part of index.

If the index is very large we have more shards and if there is a lot traffic increase the number of replicas. in both cases, increase the number of machines, but datacenter are very expensive and we want to minimize the number of shards.

# Basic model of data compression 

![[Pasted image 20241026173115.png]]

We have a input bit string that we pass to a program, the *compressor*, and we obtain an output bit string. We can have an another program, the *decompressor*, that return the original bit-string.


The compression ratio is define as: $CR=\frac{|B|}{|C(B)|}$. If $CR=r$ then the size of the compressed output $|C(B)|$ is $r$ times smaller then the input size $|B|$.

To evaluate a compressor we have to consider for sure the compression rate, but we don't want only the reduction of space but also of time.

Is not only important how long the compressor takes to compress data but also how long it takes to decompress, because we don't want to slow down in the query processing.

We want to be able to compute directly on compressed data.
---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Indexing a document]]"
tags:
  - IR
  - PEA
Creation: 2024-10-14
---
We have a pointer in posting list and we define operations to move it.

- $\text{first}_{t}()$ : places the point to the begin of the list
- $\text{next}_{t}()$ : goes ahead on the list to the next position
- $\text{nextGEQ}_{t}(d)$ : moves the pointer to the first docID in the list which is greater or equal to $d$
- $\text{docID}_{t}()$ : returns the current docID
- $\text{position}_{t}()$ : returns the position of the pointer, this could be important because frequency is often store in another array at the same position.

We don't store pairs of document frequency because we have to compress them and to do that we need homogeneous data, so we split them.

Examples:

1. $\text{first}_{t}()$
	![[Pasted image 20241022103135.png]]
2. $\text{docId}_{t}()$
	![[Pasted image 20241022103315.png]]
3. $\text{position}_{t}()$
	![[Pasted image 20241022103403.png]]
4. $\text{next}_{t}()$
	![[Pasted image 20241022103420.png]]
5. $\text{nextGEQ}_{t}(d)$
	![[Pasted image 20241022103431.png]]


## Implementations of NextGEQ

There are different ways to implements this operator.
One of them is with [[Binary search|binary search]] or some variants such as [[Exponential search|exponential search]], that is better because frequently the solution of NextGEQ is closer and this variant first search in the closest position.

In Exponential search we proceed with powers of 2. so we analyze the position distance one, distance 2, distance 4 and so on. 
In the case of example if we are ate the position 1 and we want to calculate $\text{nextGEQ}_{t}(12)$, the algorithm will analyze before the distance 1 position (d=5), then distance 2 (d=8), then distance 4 (d=13) and stop here.

This implementation has some issues:
- is not really efficient in time,  $\Theta (\log ( \frac{n}{t} ))$
- the skips are usually very small
- We want to compress the posting list but this implementation isn't usale with most compressors because it not possible todo random access.

In practice we use a better strategy named *Skip pointers*. It consist in skip an amount of elements (k elements, k is a constant.)
This approach work well with [[Elias-Fano compression]].
K depends on the dimension of posting list, usually is in the order of hundreds, but it depends.

## DAAT : AND query with nextGEQ

![[Pasted image 20241022112651.png]]

In the while after have compute the minimum, we want to jump with that points to the NextGEQ with the values of the other.
In this way we don't have to touch every document of the posting list.
If we have many document we have to calculate also the maximum and do the NextGEQ for all document using this value.

## TAAT : AND query with nextGEQ

TAAT is not able to skip, but with this operator we can intersect the posting list from shorter to longest. 
Reduce the number of comparisons and produce an order set of results.
It's better then approach with accumulators and is still a document at time.
Intersecting before the two shorter we obtain a smaller list, and if we intersect this we a larger one we can do more skips. 

![[Pasted image 20241022113325.png]]

![[Pasted image 20241022113338.png]]
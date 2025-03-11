---
Subject: "[[Indice - Parallel and Distributed System|SPM]]"
Super Topic: "[[Parallel computing]]"
tags:
  - SPM
Creation: 2025-02-24
---
Data streams is a key concept in many parallel applications.

A Data Stream is a sequence of data element of the same type made available over time.

A stream is a flow and sometimes we have natively these streams, such in the case of a network for the streams of packets, and sometimes we don't have streams but we have to rethink these cases in forms of streams to obtain a parallel solutions. (for example the operations between matrixes).

Data streams are:
1. *Continuous* : Data arrives constantly , or the stream length is sufficiently long
2. *Dynamic* : The *volume*, *velocity* and *variety* of data may change over time
3. *Time sensitive* : Processing must occur with minimal delay


We can think a problem like a streams of activities to solve and create a *pipeline pattern* (catena di montaggio) with new elements that work in parallel for different task.
So we can overlap the cost of different phases but we introduce a little overhead for moving items through workers.

[[Example of bikes]]
[[Example of map-based translation of books]]
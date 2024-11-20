---
Subject: "[[Algorithm Engineering - indice]]"
tags:
  - AE
Creation: 2024-09-17
---
# What is an algorithm ?


> [!NOTE] Formal definition 
> A finite, definitive, effective procedure that takes some inputs and return an output. 
> The output is the answer to the problem we want to solve.
> - Knuts

- finite -> the algorithm must terminate
- definite -> the steps are defined in an unambiguous way; the same way every time, well defined.
- effective -> every step is basic, namely atomic step that are execute in a small time (constant time) 

Take input and return an output must be correct and cannot be an error inside.
There are some [[Algoritmi randominci|randomized algorithm]], that possibly depend on an randomization and possibly have an error but this is can mathematical bounded by advanced data structures.

When we analyse algorithms we have to take in mind CPU and MEMORY. when you write an algorithm it is executed by the CPU and stay in the memory. Every operation has a constant time.
This model of computation is named RAM -> random access machine, because in this simple computer we are assuming that the CPU can read any item in the memory in a constant time

If u consider an array and you sum two elements of this u do it in a constant time.
This model doesn't represent the reality.

we have to find the correct balance for represent the reality and easy to use. that is more sophisticated than this primitive model but still easy to use



---
# What it means analyse an algorithm?

You have an algorithm idea is create a function $A\rightarrow T_A(n)$.  
$n$ is the input size, which is the number of item that the algorithm has to process.
The time complexity $T_{A}(n)$ is the number of steps that the algorithm needs to solve the problem. (It's not so correct)
For do the best thing we introduced the "worst case analysis" or the "average". 
This is worst for the number of steps to solve it.

This is not precise because in current machine there is a hierarchy of memory levels and every of them has different performances :
	CPU <-> Caches (L1, L2, L3) <-> Memory <-> Disk <-> Network
The speed of memory $10^{-9}$ and disk $10^{-3}$ so there's a gap of $10^{-6}$.
Also the size is different.

This model is called Two level memory, the first level includes caches and memory and the second the disk and the network

WE HAVE TO ORGANIZE THE DATA FOR HAVE THE BEST PERFORMANCE FROM THIS STRUCTURE. 


1. Asymptotic analysis in the worst case 
2. Step are constant but the constant is different in each level -> we don't use the number of steps but IO operation, we count the accesses to the memory , at the second level of memory


We have to consider :
- the spatial locality -> where the are located the items, where the algorithm work. Item that we use is better to be in the same block of memory
- the temporal locality -> keep the item that we use in a limited time near us and also be sparse. the dataset is small in this case. but the data is continuously used and are stored in the cache
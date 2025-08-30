---
Subject: "[[Indice - Parallel and Distributed System|SPM]]"
tags:
  - Assignment
Creation:
---
## Softmax vectorization 

The [[softmax function]] is a fundamental algorithm in machine learning, widely used in classification tasks and neural network output layers. 
It converts raw scores (logits) into a probability distribution, ensuring that the sum of the outputs equals one. 
Given its frequent use in large-scale models, optimizing the softmax operation is critical to improving overall performance in real-world applications. 

Its mathematical formulation is as follows: 
$$
 \sigma : \mathbb{R}^K\to\left\{ z \in \mathbb{R}^K | z_{i}>0, \sum_{i=1}^K z_{i}=1\right\} 
$$
$$\sigma(\mathbf{z})_{j}=\frac{e^{zj}}{\sum_{k=1}^Ke^{zk}} \quad j=1,\dots,K$$

---
1. Starting from a [[softmax_plain|scalar implementation of the softmax function in C++]] using FP32 arithmetic (provided by the teacher), optimize the softmax function by manually vectorizing the code using AVX intrinsics and FMA. 

2. Then modify the baseline code (if necessary) and apply appropriate compiler flags and pragmas to enable auto vectorization. 

3. Compare the resulting performance with your manually vectorized version. 

In the code provided by the teacher (softmax.zip) you can find the AVX implementation of the exponential function (exp256_ps) that you should use in your AVX version. 

4. Write a brief [[SMP-Ass1 report|report]] (max 3 pages) summarizing your findings, including:
	- A description of your implementation choices 
	- Performance evaluation and comparisons. 
	- Discussion of potential trade-offs between manual and auto-vectorization. 
	- Any challenges encountered and possible improvements for future work.

Send the teacher your code and report (both in a zip file with the name softmax_NameSurname.zip) by the deadline. 
Deadline: March 14 EOB. 

# Content of the softmax.zip file: 
- Makefile 
- softmax_plain.cpp : full scalar implementation 
- softmax_auto.cpp : partial implementation, the file contains the softmax_auto function you should implement for auto-vectorization
- softmax_avx.cpp : partial implementation, the file contains the softmax_avx function you should implement using AVX intrinsics 
- Include folder 
	- avx_mathfun.h : files containing some mathematical functions including exp256_ps 
	- hpc_helpers.hpp : helper functions for getting time measurements
	- README : a file with some notes related to the avx_mathfun software 

Your code should execute on the spmcluster.unipi.it machines.
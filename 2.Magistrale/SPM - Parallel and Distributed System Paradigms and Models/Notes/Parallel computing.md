---
Subject: "[[Indice - Parallel and Distributed System|SPM]]"
tags:
  - SPM
  - AESO
Creation: 2025-02-23
---
The *Parallel computing* is the practice of using multiple processors in parallel to solve problems more quickly than with a single processor.
Deals with performance assuming the correctness of the code.

It implies the capability of :
- identify and exposing parallelism in algorithms and software systems. We have to understand which part of the code has to be parallelised and the dependencies between different parts, such as [[Variabili condivise|shared variables]] and part of code protected with [[Lock|lock]].  
- understanding the costs, benefits and limitations of a chosen parallel approach. Some solutions could be better than others and it's important to know the limitations.


## Parallel machines

Parallel machines could be :
- a *computer clusters* made by multiple independent computers connected with one ore more high speed networks 
- *SMP (Symmetric Multi-Processor)*, that are multiple processor chips connected to a [[Shared memory]] hierarchy
- *CMP ( Chip Multi Processors, aka Multicore)*: multiple compute units called cores packed on a single chip.



The Parallelism is used to reduce power consumption:
$$\text{Power}_{\text{dynamic}} \approx \frac{1}{2}CV^2F$$
$$\text{Performances}=N\text{cores}\times F$$
Where : $C$ = capacitance, $V$ = voltage, $F$ = clock frequency

The $V \approx F$ therefore we have that : $\text{Power}_{\text{dynamic}} \approx CF^3$

If we double the number of cores , we double the Performance but also the Power, but if we double the number of cores and we halve $V$ and $F$ we have the same Performances but the power is reduced:
$$\frac{1}{2}(2C)\left( \frac{V}{2} \right)^2\left( \frac{F}{2} \right)=\frac{CF^3}{4}=\frac{\text{Power}_{\text{dynamics}}}{4}$$

> [!NOTE] Osservazione
> Se prima le performance aumentavano annualmente con lo sviluppo dei core, ora si è arrivati ad un punto in cui se si continua c'è troppo consumo di corrente e la densità del cip dovrebbe essere troppo alta. Quindi aumentando il numero dei chip si ha una macchina multi core in grado di avere le stesse performance con una riduzione del costo di corrente elettrica. 
> Per aumentare le performance non vanno aggiunti più chip ma il programmatore deve essere in grado di parallelizzare bene il programma.

![[Pasted image 20250224122014.png]]


## Supercomputers

A supercomputer is a highly advanced and powerful computing system designed to perform massive computations at high speeds. It is designed for raw performance.


## Software challeging

-> How we implement portability
# Approaches to Parallel Programming


## Unstructured
Offer the maximum freedom.  It's a low level approach to parallelism where developers manually control threads synchronization and data communication.

## Structured 


# Consideration
Parallelism boost performances, however its efficiency depends on the available resources, their utilization and the problem size.
In most cases a specific Parallel Pattern can be applied to solve a problem.
Parallelization is not free and introduce *overhead* that impact to the performance. The objective is reduce this overhead.
Parallelization requires *coordination* of activities and intermediate steps that introduce communication/synchronization.
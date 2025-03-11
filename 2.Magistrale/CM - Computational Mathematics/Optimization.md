---
Subject: "[[Indice - Computational Mathematics for learning and data analysis|CMLDA]]"
tags:
  - CMDLA
  - AM
  - RO
Creation: 2024-09-25
---
[[1-simple problems.pdf]]
Recall of definition as:
- [[Funzioni|functions]], con le relative informazioni sul grafico di una funzione, l'immagine 
- Level set at value v: $L(f,v)=\{ x \in \mathbb{R} : f(x)=v\} \subset \mathbb{R}$
![[Pasted image 20241107183003.png]]
# What is  an optimization problem

We consider an unconstrained optimization problem:

A mathematical optimization problem has the form :
$$
(P) \ \ f_{*}=\min\{f(x):x\in \mathbb{R}\}
$$
Where:
- $f$ is the objective function 
- $f_{*}=v(P)$ is the optimal value, that is unique if $\exists$ and it's the smaller element of $im(f)$ s.t. $L(f,v)\neq \emptyset$

So we can rewrite the problem as: 
$$
(P) \ \ x_{*}\in argmin\{ f(x):x\in \mathbb{R}\}
$$
where $x_{*}$ such that $f_{*}=f(x_{*})\leq f(x)$  $\forall x \in \mathbb{R}$ *optimal solution* if exists.


$f_{*}$ is a re-formulation of the original problem that it could be difficult.  


For a constraint optimization problem we want to:  
$$
\begin{equation}\begin{split}  
minimize \ f_{0}(x) \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \  \\
subject\ to\ f_{i}(x)<b_{i}, \ i=1\dots n
\end{split}\end{equation}
$$
The [[Vettori|vector]] $x=(x_{1},\dots,x_{n})$ is the *optimization variable* of the problem
The [[Simple problems#Function|function]] $f_{0}:\mathbf{R}^n\to\mathbf{R}$ is the *objective function* 
The functions $f_{i}:\mathbf{R}^n\to\mathbf{R},\ i=1,\dots,m$ are the *(inequality) constraint functions* 
The constants $b_{1},\dots,b_{m}$ are the *bounds* or *limits* for the constraints.


A vector $x^*$ is called *optimal* or *solution for the problem* if it has the smallest objective values among all vectors that satisfy the constraints : 
	for any $z$ with $f_{1}(z)\leq b_{1},\dots,f_{m}(z)\leq b_{m}$ we have $f_{0}(z)\geq f_{0}(x^*)$


### **Optimize the problem P**
The goal is to minimize the function $f_{0}$
The functions $f_{i}$ are the function that have to satisfied (in italiano sono i vincoli che bisogna rispettare, come in [[Ricerca operativa - indice|ricerca operativa]], e possono essere ad esempio le risorse disponibili o restrizioni fisiche)

The objective is to minimize a function $f(x)$, where $x \in \mathbb{R}$. 
This type of problem is represented as: $(P): f_* = \min \{ f(x) : x \in \mathbb{R}$
The goal is to find the value of $x$ that gives the smallest possible value of $f(x)$.

### **Optimal Value $f_{*}$:

The **optimal value** $f_*$​ is the minimum value of $f(x)$, denoted by $\nu(P)$.
It is **unique** if such a value $x$ **exists** (denoted by $\exists$), though it's not guaranteed that such a solution will always exist.


### **Smallest Element in the Image $f_{*}$:

$f_{*}$ is the **smallest element** of the image of $f$, meaning the smallest value $v$ such that the level set $L(f,v)≠∅$, meaning the level set at that value $v$ is not empty (i.e., there exists at least one $x$ such that $f(x)=v$.


![[Pasted image 20240926015234.png]]
![[Pasted image 20240926015350.png]]


### **Optimization Problem Restated**:

The optimization problem can also be described as finding the **argument that minimizes** $f(x)$: $x_∗ ∈ argmin \{ f ( x ) : x ∈ R \}$
$x_∗$​ is the **optimal solution** — the $x$-value that minimizes $f(x)$.
![[Pasted image 20240926015418.png]]

### **Optimal Solution Condition**:

$x_*$​ is the optimal solution if $f(x∗)≤f(x)$ for all $x∈\mathbb{R}$. 
This means the value $f(x_*)$ (the function's value at $x_*$​) is smaller than or equal to the value of $f(x)$ for any other $x$.

### **Non-uniqueness of $x_{*}$:**
The optimal solution $x_{*}$ may not be unique. There could be another $x'\neq x_{*}$ such that : $$f(x')=f(x)=f_{*}$$
In this case, the set of optimal solution $X_{*}$ is defined as all $x$ values where $f(x)=f_{*}$.
This can be expressed as:
$$L(f,f_{*})=X
_{*}$$
However, in most cases, we don't care about which specific optimal solution we choose because all optimal solution are considered equivalent in the "eyes of f". This means that every solution in $X_{*}$ yields the same minimum value for the function and an of them is an acceptable solution.
![[Pasted image 20240926015522.png]]
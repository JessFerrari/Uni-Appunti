---
Subject: "[[Indice - Statistica|STAT]]"
Super Topic: "[[Statistica descrittiva]]"
tags:
  - STAT
Creation: 2024-11-20
---
La media, sia empirica che campionaria, è per definizione la media aritmetica dei dati.
Si definisce come : $$\overline{x} = \frac{1}{n}\sum_{i=1}^nx_{i}=\frac{{x_{1}+x_{2}+\dots+x_{n}}}{n}$$
La media non dipende dalla distribuzione dei dati e non viene necessariamente assunta dai dai dati ma sicuramente si trova all'interno.

### Esempi

$x_{1}=(1,1,2,2,2,3,3,3,3,4,4,4,5,5)$  $n=14$  $\overline{x}_{1}=\frac{{1+1+2+2+2+3+3+3+3+4+4+4+5+5}}{14}=3$

$x_{2}=(1,1,1,2,2,2,2,3,3,3,5,5,6,6)$  $n=14$  $\overline{x}_{2}=\frac{{1+1+1+2+2+2+2+3+3+3+5+5+6+6}}{14}=3$ 

$x_{3}=(1,1,1,1,1,1,1,5,5,5,5,5,5,5)$  $n=14$  $\overline{x}_{2}=\frac{{1+1+1+1+1+1+1+5+5+5+5+5+5+5}}{14}=3$

### Osservazioni:
La media può essere intesa come un [[Centro di massa|centro di massa]], dove le masse dipendono dell'altezza dei rettangoli.


Considerando la funzione : $F(a)=\sum_{i=1}^n(x_{i-a})^2$ , fissato un valore $a$ e misurando la distanza al quadrato del dato $x_{i}$ da $a$, si vuole dimostrare che il minimo di questa funzione si trova esattamente nella media.

-> $min F(a) = F(\overline{x})$
	$F(a)$ è derivabile e ne calcolo la derivata per trovare il minimo
	$$F'(a)=2\sum_{i=1}^n(x_{i}-a)(-2)$$
	La derivata si annulla se e solo se :
	$$\sum_{i=1}^n(x_{i}-a)=0$$
	Da cui ricavo : $$\left( \sum_{i=1}^n x_{i} \right)-na= 0$$
	$$a=\overline{x}=\frac{1}{n}\sum_{i=1}^nx_{i}$$

# La media è un'operazione lineare
---
Se considero due campioni di dati $x=(x_{1},\dots,x_{n})$ e $y=(y_{1},\dots,y_{n})$ che sono legati tra loro con la relazione $y_{i}=bx_{i}+a$ $\forall b,a \in \mathbb{R}$  si osserva che:
$$\overline{y}=\frac{1}{n}\sum_{i=1}^ny_{i}=\frac{1}{n}\sum_{i=1}^nb_{x_{i}}+a=b\overline{x}+a$$
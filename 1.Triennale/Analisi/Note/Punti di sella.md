---
Subject: "[[Indice - Analisi Matematica]]"
tags:
  - AM
---
Un **punto di sella** è un punto in cui la funzione non ha né un minimo né un massimo locale, ma invece assume valori minori in alcune direzioni e valori maggiori in altre.

Considerando una funzione $f(x, y)$ in due variabili, un punto critico $(x_0, y_0)$ è un **punto di sella** se la matrice Hessiana ha **autovalori di segno opposto**. 

$$H = \begin{bmatrix} \frac{\partial^2 f}{\partial x^2} & \frac{\partial^2 f}{\partial x \partial y} \\ \frac{\partial^2 f}{\partial y \partial x} & \frac{\partial^2 f}{\partial y^2} \end{bmatrix}$$


Questo significa che la curvatura della funzione cambia segno in direzioni diverse: lungo una direzione la funzione ha concavità verso l'alto (minimo), mentre in un'altra ha concavità verso il basso (massimo).
![[Pasted image 20250208171829.png]]
---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
Creation: 2025-02-07
---
Tornare a slide 6:66 per confronto su [[Neural Networks#SVM as LBE|LBE]]

---
# Support Vector Machines (SVM)

Le Support Vector Machines (SVM) sono un insieme di reti feed forward del tipo *kernel-learning method*.

L'obiettivo principale è trovare un iperpiano che separi al meglio le classi nei dati.


*DEF.*
Dato un insieme di dati di training, una SVM costruisce un iperpiano (superficie di decisione) in cui si vuole *massimizzare* il *margine di separazione* tra la classe positiva e negativa.

Si assume che il problema dato sia linearmente separabile e che le classi in cui si possono dividere i dati siano $d=\pm 1$ .
Detto ciò, l'iperpiano di separazione si definisce come $$\mathbf{w}^T\mathbf{x}+b=0$$
Dove $\mathbf{x}$ è il vettore di input e $\mathbf{w}$ è il vettore dei pesi.

#### Margine di separazione e iperpiano ottimale
---
Per ogni vettore $\mathbf{w}$ la distanza tra l'iperpiano di separazione ed il data point più vicino si chiama **Margine di separazione** $\rho$.
![[margin svm.png]]


L'obiettivo di una SVM è quello di cercare l'**iperpiano ottimale**  per cui il margine di separazione è massimizzato.
L'**iperpiano ottimale** è dato da $\mathbf{w}_{o}$ e $b_{o}$ che sono i valori ottimali del vettore dei pesi e del bias, e si definisce come : $$\mathbf{w}_{o}^T\mathbf{x}+b_{o}=0$$
Esistono diversi iperpiani che possono risolvere il problema ma l'iperpiano ottimale è unico.
#### Funzione discriminante
---
La funzione discriminante $g(\mathbf{x})$ è la misura algebrica della distanza del vettore di input $\mathbf{x}$ dall'iperpiano ottimale e si definisce come:
$$g(\mathbf{x})=\mathbf{w}_{o}^T\mathbf{x}+b_{o}$$
Da questa funzione si può riesprimere il vettore $\mathbf{x}$ come:
$$\mathbf{x}=\mathbf{x}_{p}+r\frac{\mathbf{w}_{o}}{||\mathbf{w}_{o}||}$$
Dove $\mathbf{x}_{p}$ è la proiezione di $\mathbf{x}$ sull'iperpiano ottimale ed $r$ è la distanza di $\mathbf{x}$ dall'iperpiano ottimale.
$r$ è positiva se $\mathbf{x}$ si trova nel lato positivo dell'iperpiano,  negativa se si trova nella parte negativa, e uguale a 0 s e si trova sull'iperpiano. 

Quindi per definizione, dato che $\mathbf{x}_{p}$ appartiene all'iperpiano, si ha 
che $g(\mathbf{x}_{p})=0$. 
Da ciò:
$$g(\mathbf{x}_{p})=\mathbf{w}_{o}^T\mathbf{x}_{p}+b_{o}=\mathbf{w}_{o}^T\left( \mathbf{x}_{p}+r\frac{\mathbf{w}_{o}}{||\mathbf{w}_{o}||}\right)+b_{o}=g(\mathbf{x}_{p})+r\frac{||\mathbf{w}_{o}||^2}{||\mathbf{w}_{o}||}=r||\mathbf{w}_{o}||$$

Quindi : $r=\frac{g(\mathbf{x}_{p})}{||w_{o}||}$ , e ciò è valido in generale e si ha : $$r=\frac{g(\mathbf{x})}{||\mathbf{w}_{o}||}$$
In particolare la distanza dell'origine dall'iperpiano è $\frac{b_{o}}{||\mathbf{w}_{o}||}$ e se $b_{o }>0$ l'origine è nella parte positiva dell'iperpiano, se <0 nella parte negativa e se =0 allora e sull'iperpiano.

![[geometrical view SVM.png]]

Date le condizioni dell'iperpiano:
$$\begin{cases}
\mathbf{w}^T\mathbf{x}_{i}+b \geq 0 \text{ if } d_{i}=+1 \\
\mathbf{w}^T\mathbf{x}_{i}+b \leq 0 \text{ if } d_{i}=-1
\end{cases}$$
si possono riscalare i vettori $\mathbf{w}$ e $\mathbf{b}$ in modo che i punti più vicini all'iperpiano soddisfino : $|g(\mathbf{x}_{i})|=|\mathbf{w}^T\mathbf{x}_{i}+b|=1$

Le condizioni si possono così riscrivere come:
$$\begin{cases}
\mathbf{w}^T\mathbf{x}_{i}+b \geq +1 \text{ if } d_{i}=+1 \\
\mathbf{w}^T\mathbf{x}_{i}+b \leq -1 \text{ if } d_{i}=-1
\end{cases}$$
Ed in forma più compatta: $d_{i}(\mathbf{w}^T\mathbf{x}_{i}+b)\geq 1\ \forall \ i=1,\dots,N$

### Support vector
---
I **support vector** sono quei vettori che si trovano esattamente sul margine di separazione, e sono quindi quelli più vicini all'iperpiano.

I support vector $\mathbf{x}^{(s)}$ soddisfano esattamente l'equazione:
$$d^{(s)}(\mathbf{w}^T\mathbf{x}^{(s)}+b)=1$$

![[support vectors.png]]

Per i support vector la funzione discriminante vale $\pm {1}$ a seconda del valore di $d^{(s)}$ e quindi la distanza algebrica dei SV dall'iperpiano è data da:
$$r=\frac{g(\mathbf{x}^{(s)})}{||\mathbf{w}_{o}||}=\begin{cases}
\frac{1}{||\mathbf{w}_{o}||}\text{  if } d^{(s)}=+1 \\
-\frac{1}{||\mathbf{w}_{o}||}\text{  if } d^{(s)}=-1
\end{cases}$$
Detto ciò si definisce il margine di separazione $\rho=2r=\frac{2}{||\mathbf{w}_{o}||}$

*OBIETTIVO SVM* : Massimizzare $\rho$ $\leftrightarrow$ Minimizzare $||\mathbf{w}_{o}||$


# Miglioramento della generalizzazione
---

Con le SVM si fissa l'errore di training per problemi linearmente separabili. Minimizzare la norma di $\mathbf{w}$ è equivalente a minimizzare la VC-dimension e quindi minimizzare il termine $\epsilon$ (VC-confidence) nella [[Statistical Learning Theory - Vapnik|STL]].

*Teorema di Vapnik:*
	Sia $D$ il diametro della palla più piccola che si trova attorno agli esempi di training $\{\mathbf{x}_{i}\}_{i=1}^N$.
	Per la classe di iperpiani di separazione descritta da dall'equazione $\mathbf{w}^T\mathbf{x}+b=0$, il limite superiore della VC-dimension è : $$VC \leq \min \left( \left \lceil   \frac{D^2}{\rho^2} \right \rceil , m_o \right) + 1$$

Dove $\left \lceil   \frac{D^2}{\rho^2} \right \rceil= \text{Radios}^2||\mathbf{w}||^2$

![[Pasted image 20250210173926.png]]
 Non ho capito

## Approccio elegante
---
Per i dati linearmente separabili posso esserci molteplici soluzioni e l'approccio di Vapnik propone un *iperpiano di separazione ottimale* massimizzando il margine fornendo :
- Una soluzione unica con zero errori per il classificatore binario 
	- non vale per il algoritmo di learning iterativo  del percettrone e non per la LMS
- Un approccio automatizzato della SRM che minimizza la VC-confidence come parte del processo di training. senza iperparametri nel caso di dati linearmente separabili
- L'uso di un solver della classe dei problemi quadratici vincolati con una forma duale 
- Una soluzione incentrata sui dati di training selezionati (i support vector)
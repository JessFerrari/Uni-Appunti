---
Subject: "[[Indice - Machine Learning|ML]]"
Super Topic: "[[Linear models]]"
tags:
  - ML
Creation: 2025-03-09
---
Il **$K$-Nearest Neighbor (k-nn)** è un algoritmo di __[[Supervised Learning|learning supervisionato]]__ __[[Instance Based Machine Learning Models|instance-base]]__.  

Questo algoritmo si utilizza principalmente per la classificazione e si basa sul idea che i nuovi punti siano simili a quelli "vicini".

Per valutare quando due punti siano vicini si utilizzano delle metriche come ad esempio la __[[Distanza euclidea|distanza euclidea]]__.


L'algoritmo per la classificazione binaria è il seguente:
1. Si sceglie un valore $k \in \mathbb{N}$ arbitrario 
2. Si mantengono i dati di training  in memoria come lista di coppie $( \mathbf{x}_p, \mathbf{y}_p) \ \ P=1,\dots,l$ , dove $\mathbf{x}_i\in \mathbb{R}^n$ e $y_i\in [0,1]$, ossia una variabile binaria.
3. Dato in un input $\mathbf{x}\in \mathbb{R}^n$ sconosciuto e $d(\mathbf{x},\mathbf{x}_i)$ una __distanza__ trova $k$ vicini tale che  $$N_k(\mathbf{x})= \arg_p \min d(\mathbf{x} ,\mathbf{x}_p) = \{(\mathbf{x}_1,y_1)\dots(\mathbf{x}_k,y_k)\}$$ovvero i $k$  __dati di training__ più vicini al nuovo dati $\mathbf{x}$  
	![[Pasted image 20250309015127.png]]

4. Calcolare la classe media scelta. Questo rappresenta un voto di maggioranza  $$avr_k(\mathbf{x})= \frac{1}{k}\sum_{x_i\in N_k(\mathbf{x} )} y_i$$
5. Restituire la classe che vince il voto di maggioranza, ovvero:$$
\begin{cases}
1 & if & avg_k(\mathbf{x})>0.5 \\
0 & & \text{otherwise}
\end{cases}$$ 


## Diversi k
---

Con $K=1$ si ha un modello __molto flessibile__, non ha errori di classificazione su __training set__ e ha un decision boundary non lineare e molto irregolare e rumoroso e solitamente va in __[[Overfitting e Underfitting|overfitting]]__
	![[Pasted image 20250309015230.png]]

Con un $K$ più alto si ottiene un decision boundary comunque flessibile e non lineare ma un po' meno rumoroso. 
Solitamente un valore alto ma non troppo porta a dei buoni risultati.
	![[Pasted image 20250309015320.png]]

Con $K=\ell$ abbiamo che il modello è molto rigido è siamo in [[Overfitting e Underfitting|underfitting]].

Questo algoritmo utilizza implicitamente i [[Diagramma di Voronoi|diagrammi di Voronoi]].

# Classificazione multi classe
---

Per fare [[Classification|classificazione]] multi classe si utilizza lo stesso algoritmo cambiandone l'output e facendo restituire la classe più comune tra i suoi $K$ vicini:
$$h(\mathbf{x})= \arg_v \max \sum_{(\mathbf{x}_i,y_i)\in N_k(\mathbf{x})}\mathbf{1}_{v,y_i}$$dove :
$$\mathbf{1}_{v,y_i}=
\begin{cases}
1 & if & v=y_i \\
0 & &\text{otherwise} 
\end{cases}
$$
## Variante
Una variante in cui viene dato più peso ai punti più vicini e meno a quelli più lontani è la seguente: $$h(\mathbf{x})= \arg_v \max \sum_{(\mathbf{x}_i,y_i)\in N_k(\mathbf{x})}\mathbf{1}_{v,y_i} \cdot \cfrac{1}{d(\mathbf{x},\mathbf{x}_i)^n}$$e per gestire il caso limite $d(\mathbf{x},\mathbf{x}_i)=0$ si restituisce $y_i$ perché sono lo stesso punto.


Per la [[Regression|regressione]] si usa lo stesso algoritmo ma come output si restituisce direttamente la media delle posizioni dei vicini.



# Discussione
---
## Gradi di libertà
---
In generale il al $k$ -Nearest Neighbor vengono attribuiti $\cfrac{\ell}{k}$ gradi di libertà  dove $\ell$  è il numero di dati a disposizione.
I __gradi di libertà__ son detti "parametri effettivi" del modello.

Al variare di questi cambiano le performance dell'algoritmo,come mostra il seguente grafico:
	![[Pasted image 20250309020201.png]]

## Approssimazione classificatore Bayesiano
---
Il classificatore $K$-NN  cerca di approssimare la soluzione di un __[[Bayesian Classificator|classificatore bayesiano]]__ mettendo in atto un'__approssimazione locale__ tramite i punti vicini al punto $\mathbf{x}$, della  __[[Probabilita condizionata|probabilità condizionata]]__ della classe di appartenenza. 
Questa probabilità condizionata ovvero ciò che il __classificatore Bayesiano__ utilizza per assegnare una classe al punto $\mathbf{x}$.


 Nell'immagine seguente si vedono dei punti che vengono estratti da due [[Variabili Aleatorie Notevoli - Gaussiane|gaussiane]] note. 
 Siccome si conoscono le distribuzioni è possibile calcolare la soluzione del __classificatore bayesiano__ direttamente (a sinistra) e si può vedere come il $K$-NN con $K=15$ riesce ad approssimare questa soluzione (destra):
	![[Pasted image 20250309020636.png]]


# Bias-induttivo

1. __Distanza e Similarità__:  La distanza scelta nell'algoritmo determina quali esempi sono considerati più simili. La classificazione di un nuovo esempio dipende dalla classificazione dei suoi vicini più prossimi, secondo la metrica usata.

2. __Smoothness Locale__: si basa sul assunzione che esempi vicini abbiano etichette simili, una sorta di "regolarità locale". 
>[!tip] 
>È _possibile imparare_ la metrica 


# Importanza dello Scaling e del Preprocessing

Per assicurarsi delle buone performance è spesso necessario riscalare le variabili ma per fare ciò si è spesso legati alla conoscenza del dominio.

Se tutte le variabili devono contribuire in __modo uguale__, allora gli input range dovrebbero essere riscalati per essere uguali, ad esempio, utilizzando una normalizzazione con media zero e varianza unitaria.  
Questo però può portare a problematiche:
- il $K$-NN è  fragile al preprocessing e il semplice rescaling può cambiare di molto i risultati finali. Per agire su questo problema va cambiata anche la metrica, cosa non necessariamente banale
	![[Pasted image 20250309020914.png]]


# Limiti

Alcune problematiche del $K$-nn sono le seguenti:

- Il __Costo Computazionale__ è rimandato al momento della predizione ed è elevato poiché richiede il calcolo della distanza con __TUTTI__ i punti memorizzati nel modello. 

- Il tempo necessario cresce proporzionalmente al numero di dati, e l'algoritmo ha anche un __alto costo in termini di spazio__, poiché ogni dato deve essere mantenuto in memoria.  Esistano algoritmi di prossimità "ad-hoc" per ottimizzare questo processo ma il problema resta rilevante. ( forse [[Indici spaziali|Indici spaziali]])

## Curse of dimentionality
---
Al crescere della dimensionalità dell'input il modello è sempre meno capace di costruire una buona generalizzazione e questo è noto come **Curse of dimensionality**.  

Questo avviene principalmente dal fatto che in dimensionalità alta è molto probabile che i $K$ dati piu vicini siano spazialmente lontani e che quindi quindi la stima non sia piu "locale".

Assumendo che ogni variabile sia nel range $[0,1]$, questo fenomeno può essere notato partendo da un cubo unitario e mostrando quale è la frazione del range di range necessaria per ogni variabile per coprire una certa percentuale del volume.

si ha infatti che con $n$ dimensioni per coprire una frazione $r$ del volume abbiamo bisogno del $r^{1/n}$ range di ogni variabili
![[Pasted image 20250309021150.png]]
In più la densità di sampling scende infatti la densità è calcolata come $\cfrac{\ell}{volume}$ che è proporzionale a $\ell^{1/n}$

## Curse of noisy
---
 Un altro problema è il "__curse of noisy__", che si verifica quando i dati dipendono da poche feature rilevanti, ma includono molte feature irrilevanti. 
 Queste ultime possono dominare quelle rilevanti, portando a classificazioni errate e riducendo l'efficacia dell'algoritmo. 
 Questo problema si può mitigare pesando le feature in base alla rilevanza oppure facendo __feature Selection__, ovvero eliminando alcune variabili.
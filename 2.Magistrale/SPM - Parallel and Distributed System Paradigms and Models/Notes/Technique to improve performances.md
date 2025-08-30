---
Subject: "[[Indice - Parallel and Distributed System|SPM]]"
Super Topic: "[[Performance Engineering of System Software]]"
tags:
  - SPM
  - Programming
Creation: 2025-03-12
---
# Case study
---
Si prende in considerazione la moltiplicazione matriciale $C=A \times B$
$$C_{ij}=\sum_{k=1}^Na_{ik}b_{kj}$$
Dove $A$, $B$ e $C$ sono 3 matrici quadrate $n\times n$, e per semplicità si assume che $n=2^k$


Si prende un'architettura con queste features:
![[Pasted image 20250312091218.png]]
e si calcola il [[Performance Engineering of System Software|Peak]] :
$$\text{Peak}=(2.9\times{10}^9)\times{2}\times{9}\times{16}=836\text{GFLOPS}$$
# Improves that belong to the languages 
### Best result : $1156 \text{ secondi} \approx 19 \text{ minuti}$
1. ***Implementazione in Python***
	Con un implementazione naive in python, con $n=4096$, i nested loop nell'ordine $i,j,k$ si ottiene un running time di $21042 \text{ secondi}\approx 6\text{ ore}$
2. ***Implementazione in Java***
	Passando da un'implementazione da Python a Java si ottiene un running time di $2738 \text{ secondi} \approx 46 \text{ minuti}$, ossia si ha un miglioramento di velocità circa del $8.8\times$ rispetto a Python
3. ***Implementazione in C***
	Passando poi all'implementazione in C si ha un'ulteriore miglioramento: $1156 \text{ secondi} \approx 19 \text{ minuti}$, che è $2\times$ più veloce rispetto a Java e $18\times$ più veloce rispetto a Python.

Queste differenze di velocità sono date dal fatto che Python è un [[Interpreti e Compilatori|linguaggio interpretato]] mentre C è un [[Interpreti e Compilatori|linguaggio compilato]] direttamente in linguaggio macchina.
Java invece è compilato in byte-code e poi questo viene interpretato in linguaggio macchina.

# Interchange Loops
### Best result : $177.68 \text{ secondi} \approx 3 \text{ minuti}$

Modificare l'ordine dei cicli nel codice C ha portato a un significativo aumento delle prestazioni, con un fattore di speedup di circa $6.5 \times$ rispetto alla versione C iniziale. 
Questo è dovuto al miglioramento della **[[Principio di località|località spaziale]]** nell'accesso ai dati e alla riduzione dei **[[Cache misses|cache miss]]**. 

Diverse combinazioni dell'ordine dei cicli hanno mostrato tempi di esecuzione molto diversi.
	![[Pasted image 20250312133908.png]]
	Per sapere la percentuale di cache misses si utilizza [[Valgrind|valgrind]] con il tool per la simulazione della cache:
	`valgrind --tool=cachegrind ./mm`


# Compiler optimization flags
### Best result : $54.63 \text{ secondi}$

Con l'utilizzo di flag di ottimizzazione con il compilatore Clang si ha un ulteriore miglioramento delle prestazioni, ottenendo uno speedup di circa $3.25 \times$ rispetto alla versione con l'interscambio dei cicli.

Alcune flag di Clang, e i rispettivi significati e tempistiche su questo problema, sono:
	![[Pasted image 20250312134935.png]]
Inoltre Clang supporta livelli di ottimizzazione per scopi speciali come :
- `-Os` che permette di limitare la dimensione del codice
- `-Og` che si usa per il debugging
# Parallel Loops
### Best result : $3.04 \text{ secondi}$
Si vogliono introdurre cicli paralleli per sfruttare i 18 core disponibili sulla macchina.
Ciò porta uno speedup notevole, quasi $18\times$ rispetto alla versione sequenziale ottimizzata. 
Si osserva che è preferibile parallelizzare i cicli esterni piuttosto che quelli interni.

Con il comando `click_for` si da il permesso di eseguire il loop in parallelo.
Quindi il codice si mostrerà come:
```C
click_for (int i=0;  i<n: i++){
	for (int k=0; k<n; k++){
		for (int j=0; j<n; j++){
			C[i][j] += A[i][k] * B[k][j]
		}
	}
}
```
Questo riduce il run time a $3.04 \text{ secondi}$. 

⚠ non tutti i programmi sono parallelizzabili così facilmente.
# Tiling
### Best result : $1.79 \text{ secondi}$
Il *Tiling* è una tecnica che prevede la suddivisione delle matrici in blocchi più piccoli per migliorare il riutilizzo dei dati nella cache. 
Per farlo si ristruttura la computazione in modo tale da poter riusare i dati in cache il più possibile.
L'implementazione con tiling mostra un ulteriore miglioramento delle prestazioni, con una riduzione significativa delle **cache reference** e dei **cache miss**. 
La dimensione ottimale della tile deve essere trovata tramite sperimentazione.
	![[Pasted image 20250312141023.png]]
```C
click_for (int ih=0;  ih<n; ih+=s){
	click_for (int jh=0; jh<n; jh+=s){
		for (int kh=0; kh<n; kh+=s){
			for (int il=0; il<s; ++il){
				for (int kl=0; kl<s; ++kl){
					for (int jl=0; jl<s; ++jl){
						C[ih+il][jh+jl] += A[ih+il][kh+kl] * B[kh+kl][jh+jl] 
					}
				}
			}
		}
	}
}
```
![[Pasted image 20250312141647.png]]
# Parallel Divide-and-Conquire
### Best result : $1.30 \text{ secondi}$

Si utilizza un approccio ricorsivo per la moltiplicazione di matrici, combinato con la parallelizzazione.
Ciò ha portato a ulteriori guadagni di performance. È stato necessario "irrobustire" la ricorsione (coarsening) per superare il costo delle chiamate di funzione per i casi base troppo piccoli. 
La dimensione del caso base è un parametro di tuning importante.
![[Pasted image 20250312142537.png]]
`click_spawn` e `click_sync` servono per controllare l'esecuzione. Con il primo comando la funzione figlio è *spawned*, ossia viene eseguita in parallelo con il padre, mentre, con il secondo, si impone che l'esecuzione non può proseguire fino a quando la unzione spawned non restituisce un risultato. 
# Compiler Vectorization
### Best result : $0.70 \text{ secondi}$
Con l'utilizzo di flag del compilatore (come `-march=native -ffast-math`) per abilitare l'uso di istruzioni vettoriali [[SIMD]] (Single Instruction, Multiple Data) ha quasi raddoppiato le prestazioni.

# Intrinsics
### Best result : $0.39 \text{ secondi}$
L'uso esplicito degli [[Intrinsic AVX]] fornite da Intel ha consentito un controllo ancora maggiore sull'hardware vettoriale, portando a un ulteriore miglioramento delle prestazioni e raggiungendo un livello competitivo con la libreria Math Kernel Library (MKL) di Intel ($0.41\text{ secondi}$).

# Others
- **Altre ottimizzazioni**: Oltre alle tecniche principali, sono state menzionate ulteriori ottimizzazioni come la pre-elaborazione, la trasposizione della matrice, l'allineamento dei dati e le ottimizzazioni della gestione della memoria.

# Discussion
---
![[Pasted image 20250312135548.png]]
![[Pasted image 20250312141813.png]]
1. Notare che nelle soluzioni *linguaggi*, *inverted loops* e *compiler's flags* si ha una percentuale di peak molto basso perché non si sta utilizzando l'hardware parallelo fornito. Infatti viene usato solo 1 dei 18 core del sistema.
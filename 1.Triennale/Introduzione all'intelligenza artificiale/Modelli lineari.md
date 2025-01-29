![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30ee2ca2-9bef-46ae-9116-330f95ae1916/Untitled.png)

In base al tipo del target d si hanno 2 tipi diversi di apprendimento:

- CLASSIFICAZIONE : $f(x)$ restituisce la classe che assume essere corretta per x. $f(x)$ è una funzione che lavora su valori discreti
- REGRESSIONE : $f(x)$ è una funzione a valori reali $(\R\ o \ \R^k)$

## MODELLO LINEARE PER REGRESSIONE

> Per regressione si intende stimare una funzione a valori reali sulla base di un insieme finito di dati rumorosi

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c48cbcf0-deec-4a1f-a9a3-b78b7e96ce1f/Untitled.png)

nell’esempio di sopra si hanno un insieme di dati rumorosi e la funzione c(x) viene approssimata con h(x)=2x.

La funzione approssimata è difficile da scegliere a mente se a più variabili.

Ci possono essere altre funzioni che l’approssimano ma si cerca la migliore.

La funzione lineare ha forma $y=w_1x+w_0$

## Modello lineare con una sola variabile (Univariato)

Il caso in cui è presente una sola variabile si ha una semplice regressione lineare: 1 input → 1 output

$$ out=h(x)=w_1x+w_0 $$

dove $w_1$ e $w_0$sono coefficienti reali chiamati parametri liberi.

Per approssimare la funzione bisogna scegliere valori per i parametri liberi in modo che i dati di training fanno fitting sulla retta.

> TASK E MODELLO

Trovare h (modello lineare) che fa il fit dei dati di training al meglio. Assumendo che la variabile y data è relazionata alla variabile x in base alla funzione $y=w_1x+w_0+noise$, dove $w_1$ e $w_0$ sono parametri liberi e il rumore è l’errore di misurazione del target.

L’obbiettivo è costruire un modello, ossia cercare il valore di $w_1$ e $w_0$, per predire il valore di y di valori x non ancora osservati.

## Costruzione del modello : come trovare $w_1$ e $w_0$

Si vogliono trovare il valore dei parametri liberi in modo da minimizzare l’errore dell’output e fare un buon fitting dei dati.

Lo spazio delle ipotesi è infinito (w può assumere valori in un insieme continuo) ma si usa la matematica classica per risolvere tale problema: si definisce una FUNZIONE DI ERRORE usando l’approccio LEAST MEAN SQUARE (LSM).

> LSM (Least Mean Square) è un approccio matematico per minimizzare l'errore nella costruzione di un modello lineare. In pratica, si cerca di trovare i valori dei parametri liberi (nel caso di una semplice regressione lineare, $w_0$ e $w_1$) che minimizzino la somma dei quadrati delle differenze tra i valori stimati dal modello e i valori reali osservati nei dati di training. Questo approccio è ampiamente utilizzato in analisi di dati e machine learning per la costruzione di modelli predittivi.

Dato un insieme $l$ di dati di esempio $(x_p,y_p)$, $p:1...l$

trovare $h_w(x)$ della forma $h_w(x)=w_1x+w_0$ tale che minimizza l’errore aspettato sui dati di training.

$Loss(h_w)=E(w)=\sum_{p=1}^l(y_p-h_w(x_p))^2=\sum_{p=1}^l(y_p-(w_1x_p+w_0))^2$

La formula sopra è la formula per il calcolo della funzione di perdita $Loss(h_w)$ in un modello lineare con una sola variabile, dove $h_w(x)=w_1x+w_0$ è la funzione approssimata e $E(w)$ è l'errore aspettato sui dati di training. L'errore aspettato è calcolato come la somma dei quadrati delle differenze tra i valori stimati dal modello e i valori reali osservati nei dati di training per ogni punto p nell'insieme di dati di esempio $(x_p,y_p), p:1...l.$. In pratica, si cerca di trovare i valori dei parametri liberi $w_0$ e $w_1$ che minimizzano l'errore aspettato sui dati di training. Questo approccio è noto come Least Mean Square (LSM).

L'elevamento al quadrato viene usato nella formula perché si vuole penalizzare maggiormente gli errori più grandi, rispetto a quelli più piccoli. In questo modo, minimizzando la somma dei quadrati degli errori, si cerca di trovare un modello che faccia il miglior fitting possibile dei dati di training.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d77a24e-6338-44d7-adb3-3a3412975e38/Untitled.png)

Per trovare i valori dei parametri w è bene ricordare che il minimo locale è un punto stazionario in cui la derivata è nulla. Dato che le variabili w sono due bisogna fare le derivate parziali del loss e porle uguali a zero (calcolare il gradiente nullo).

$$ \frac {\delta E(w)}{\delta w_i}=0, \ \ i:1...,dim\_input+1 $$

Per una regressione lineare si ha :

$$ \frac {\delta E(w_1)}{\delta w_1}=0 \ \ \ \frac {\delta E(w_0)}{\delta w_0}=0 $$

$$ \frac {\delta E(w)}{\delta w_i}=\frac {\delta (y-h_w(x))^2}{\delta w_i}=\\ =2(y-(h_w(x))\frac {\delta (y-h_w(x))}{\delta w_i}=\\ =2(y-h_w(x))\frac {\delta(y-(w_1x+w_0))}{\delta w_i} $$

$$ \frac {\delta E(w)}{\delta w_0}=2(y-h_w(x))\ \ \ \ \ \ \ \ \frac {\delta E(w)}{\delta w_1}=2(y-h_w(x))x $$

### Gradiente discendente (ricerca locale)

Per ricercare i parametri w si può eseguire una ricerca locale basata su $\frac{\delta E(w)}{\delta w_i}$.

Ci si muove verso il minimo con un n gradiente discendente : $\Delta w=-gradiente(E(w))$

Il segno meno davanti al gradiente discendente è dovuto al fatto che si cerca il minimo della funzione di errore, quindi si vuole muoversi nella direzione opposta alla pendenza della funzione stessa. Il gradiente discendente rappresenta la direzione in cui la funzione di errore cresce più rapidamente, quindi muovendosi nella direzione opposta si cerca di minimizzare l'errore.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/67aa5e5c-2278-40b2-a802-59ec80fd34fb/Untitled.png)

Si inizia la ricerca locale con un vettore w che si modifica in modo iterativo fini a minimizzare l’errore.

$$ w_{new}=w+\eta*\Delta w $$

dove $\eta$ è una costante chiamata learning rate che serve per regolare la dimensione dei passi che vengono fatti durante la ricerca del minimo.

È un parametro importante perché, se impostato troppo alto, potrebbe causare oscillazioni intorno al minimo locale, mentre se impostato troppo basso, potrebbe richiedere troppo tempo per raggiungere il minimo. Il valore del learning rate deve essere scelto con attenzione per garantire una convergenza rapida e stabile dell'algoritmo.

> Questo è un modo per sistemare l’errore ed è chiamato DELTA RULE e serve per cambiare in modo proporzionale rispetto all’errore i parametri w

se : → y-h(x) = 0 allora non avviene nessuna correzione → h(x)>y quindi (y-h(x))<0 bisogna diminuire l'output aggiornando il valore dei parametri w come segue: - riducendo $w_0$ - se l’input è >0 ridurre $w_1$ altrimenti aumentarlo → h(x)>y quindi (y-h(x))<0 bisogna diminuire l'output aggiornando il valore dei parametri w come segue: - aumentando $w_0$ - se l’input è >0 aumentare $w_1$ altrimenti diminuirlo

Il gradiente discendente permette di fare una ricerca all’interno di uno spazio delle ipotesi infinito. Può essere applicato in modo semplice per spazi H continui e errori differenziabili e quindi non solo per i modelli lineari.

Si può rendere efficiente eseguendo alcune modifiche.

> GPT HELP

Il metodo del gradiente discendente può essere reso più efficiente attraverso alcune modifiche, come ad esempio l'utilizzo di un learning rate adeguato, che permetta di regolare la dimensione dei passi durante la ricerca del minimo. Inoltre, è possibile utilizzare una strategia di adattamento del learning rate, come ad esempio il metodo di Adagrad, che adatta il learning rate a ogni passo della ricerca in modo che i passi siano più piccoli vicino al minimo e più grandi lontano dal minimo. Inoltre, si può utilizzare la regolarizzazione, che aiuta a prevenire l'overfitting del modello, o l'utilizzo di algoritmi di ottimizzazione più avanzati, come il metodo di BFGS o il metodo di Newton, che utilizzano informazioni sulle derivate seconde della funzione di errore per accelerare la convergenza.

## Estensione metodo del gradiente per $l$ patterns

> $\Delta w_0 = \frac{\delta E(w)}{w_0}=2\sum_{p=1}^l(y_p-h_w(x_p))$

$\Delta w_1 = \frac{\delta E(w)}{w_1}=2\sum_{p=1}^l(y_p-h_w(x_p))*x_p$

Si può aggiornare w dopo un’epoca, ossia dopo aver terminato il data set di training, o On-line, ossia dopo ogni pattern p [metodo STOCASTICO]
### Domande generali su Machine Learning

1. Quali sono i principali motivi per cui si utilizza il Machine Learning rispetto ai metodi tradizionali?
2. Quali sono le condizioni che rendono utile l'applicazione del ML in un problema?
3. In che modo il Machine Learning si inserisce nel contesto dell'intelligenza artificiale e della scienza computazionale?

### Dati e rappresentazione

4. Quali sono i diversi tipi di dati che possono essere utilizzati in ML? Fornisci esempi per ciascuno.
5. Qual è la differenza tra dati strutturati e non strutturati in ML?
6. Che cos'è il problema della rappresentazione dei dati e perché è importante?
7. Quali sono alcune tecniche di encoding utilizzate per rappresentare i dati categoriali?

### Task ML

8. Qual è la differenza tra apprendimento supervisionato e non supervisionato? Fai un esempio per ciascuno.
9. Cosa si intende per apprendimento semi-supervisionato e quando può essere utile?
10. In cosa consiste l’apprendimento per rinforzo e come differisce dagli altri tipi di apprendimento?
11. Qual è la differenza tra classificazione e regressione? Fai un esempio pratico per ognuno.

### Modelli e metodi

12. Cos'è lo spazio delle ipotesi in ML e perché è importante?
13. Qual è il significato dell'espressione "No Free Lunch Theorem" nel contesto del ML?
14. Quali sono i principali paradigmi di modellazione nel Machine Learning?
15. In cosa si differenziano i modelli simbolici, sub-simbolici e probabilistici?

### Funzioni di loss e generalizzazione

16. Cos'è una funzione di perdita e perché è fondamentale in ML?
17. Qual è la differenza tra errore di addestramento ed errore di generalizzazione?
18. Quali sono le principali funzioni di perdita utilizzate per la regressione e per la classificazione?
19. Perché la validazione è una fase cruciale in un modello di Machine Learning?

### Concetti Generali

1. Quali sono i cinque elementi fondamentali in un sistema di Machine Learning?
2. Cosa significa che il problema del ML è "ill-posed" e come si affronta questa criticità?
3. Qual è la differenza tra il rischio empirico e il rischio vero in un modello di apprendimento?
4. Perché l'uso corretto del Machine Learning è più importante della semplice applicazione di strumenti ML?

---

### Bias, Underfitting e Overfitting

5. Cosa si intende per "Inductive Learning Hypothesis"?
6. Come si manifesta il problema dell’overfitting e quali sono le cause principali?
7. Cos’è l’underfitting e in quali situazioni si verifica?
8. Qual è la relazione tra la complessità del modello e il numero di dati disponibili?
9. Guardando l'esempio della regressione polinomiale, cosa accade aumentando il grado del polinomio?
10. Perché un polinomio di 9° grado potrebbe avere errore zero sui dati di training ma non generalizzare bene?

---

### Teoria Statistica dell'Apprendimento (SLT)

11. Cos'è la Vapnik-Chervonenkis (VC) dimension e perché è importante?
12. In che modo la VC-dimensione influenza il compromesso tra underfitting e overfitting?
13. Come la Statistical Learning Theory (SLT) aiuta a spiegare il comportamento dei modelli ML?
14. Cosa rappresenta la formula R≤Remp+ε(VC,l,δ)R \leq R_{emp} + \varepsilon(VC, l, \delta)R≤Remp​+ε(VC,l,δ) e qual è il suo significato pratico?
15. Perché un modello con bassa capacità può avere elevato errore empirico?

---

### Validazione e Generalizzazione

16. Qual è la differenza tra Model Selection e Model Assessment?
17. Perché è fondamentale separare il training set, validation set e test set?
18. In cosa consiste la tecnica di Hold-out e quali sono i suoi limiti?
19. Cos’è la Cross-Validation e perché è più robusta della Hold-out validation?
20. Come il K-Fold Cross Validation permette un uso più efficiente dei dati rispetto alla semplice divisione TR/VL/TS?
21. Qual è il ruolo della matrice di confusione nella valutazione delle prestazioni di un classificatore?
22. Perché la curva ROC è utile per analizzare le prestazioni di un modello di classificazione?

---

### Ciclo di Progettazione e Interpretazione

23. Quali sono le fasi principali nel ciclo di progettazione di un modello ML?
24. Perché la scelta delle features e la pre-elaborazione dei dati sono fondamentali?
25. Quali sono i rischi di interpretare erroneamente i risultati di un modello ML?
26. Perché correlazione non implica causalità? Fai un esempio di un errore comune nell’interpretazione dei dati.
27. Perché anche un modello molto potente può produrre risultati fuorvianti se applicato a dati spazzatura?
28. 
### Modelli Lineari e Regressione

1. Qual è la differenza tra regressione e classificazione in Machine Learning?
2. In cosa consiste la regressione lineare univariata e come si esprime matematicamente?
3. Qual è il significato dei parametri w0w_0w0​ e w1w_1w1​ in un modello di regressione lineare?
4. Cos’è il criterio dei minimi quadrati (Least Mean Squares, LMS) e perché viene utilizzato?
5. Perché la regressione lineare può essere vista come un caso particolare di ottimizzazione?

---

### Apprendimento dei Modelli Lineari

6. Quali sono i due principali approcci per trovare i pesi di un modello lineare?
7. In cosa consiste l’equazione normale e quali sono i suoi vantaggi e svantaggi?
8. Come funziona la discesa del gradiente e qual è il ruolo del learning rate η\etaη?
9. Qual è la differenza tra discesa del gradiente batch e stocastica?
10. Come si può risolvere il problema di una matrice $X^TX$ non invertibile nell'equazione normale?

---

### Classificazione con Modelli Lineari

11. In che modo i modelli di regressione lineare possono essere adattati per la classificazione?
12. Cosa rappresenta il termine $w^T x = 0$ in un modello di classificazione lineare?
13. Come si interpreta geometricamente un classificatore lineare?
14. Perché è importante la scelta della funzione soglia in un classificatore lineare?
15. Qual è la differenza tra classificazione binaria e multi-classe nei modelli lineari?

---

### Bias, Overfitting e Regolarizzazione

16. Qual è il problema principale dei modelli lineari quando il dataset non è linearmente separabile?
17. Cosa rappresenta il concetto di bias nei modelli di Machine Learning?
18. Qual è l’effetto della regolarizzazione Ridge (Tikhonov) sulla complessità del modello?
19. Come si può interpretare la regolarizzazione in termini di compromesso tra bias e varianza?
20. Qual è il ruolo del parametro λ\lambdaλ nella regolarizzazione?

---

### K-Nearest Neighbors (K-NN)

21. In che modo il K-NN si differenzia dai modelli lineari?
22. Qual è il principio alla base dell’algoritmo K-NN?
23. Come si calcola la distanza tra i punti nel K-NN e quali metriche possono essere usate?
24. Qual è la differenza tra un classificatore K-NN con K=1K=1K=1 e con KKK grande?
25. Perché un valore di KKK troppo basso può portare a overfitting?

---

### Confronto tra Modelli Lineari e K-NN

26. Quali sono i principali vantaggi e svantaggi dei modelli lineari rispetto a K-NN?
27. In quali scenari K-NN è preferibile rispetto ai modelli lineari?
28. Perché K-NN è considerato un metodo "lazy" e i modelli lineari "eager"?
29. Qual è il legame tra la complessità del modello e il numero di parametri effettivi in K-NN?
30. Perché K-NN soffre del problema della "maledizione della dimensionalità" e come si può mitigare?

---

### Approfondimenti e Limitazioni

31. Qual è il significato della curva di errore Bayesiano e perché è utile per valutare i modelli?
32. Come il metodo K-NN approssima la decisione Bayesiana ottimale?
33. Quali problemi introduce la scelta della metrica di distanza nel K-NN?
34. Qual è il costo computazionale di K-NN in fase di predizione rispetto ai modelli lineari?
35. Perché il preprocessing dei dati (ad esempio la normalizzazione) è cruciale per il K-NN?
---
### Introduzione alle Reti Neurali

1. Qual è il significato del teorema di Cybenko sulle reti neurali?
2. In che senso le NN sono considerate "universal approximators"?
3. Quali sono le principali differenze tra una NN e un modello lineare?
4. In che modo le NN possono gestire dati rumorosi o incompleti?

---

### Modelli di Reti Neurali

11. Quali sono le principali funzioni di attivazione usate nelle NN?
12. Qual è la differenza tra un Perceptron e una rete Multi-Layer Perceptron (MLP)?
13. In che modo un Perceptron può risolvere problemi di classificazione?
14. Perché un Perceptron non può risolvere il problema dell’XOR?
15. Come una rete con due strati nascosti può risolvere il problema dell’XOR?

---

### Algoritmi di Apprendimento

16. Come funziona l’algoritmo di apprendimento del Perceptron?
17. Qual è il significato geometrico dell’algoritmo di apprendimento del Perceptron?
18. Qual è la differenza tra la regola di aggiornamento del Perceptron e la regola Delta?
19. Cos’è la discesa del gradiente e perché è utile nelle NN?
20. Quali sono le principali difficoltà nel training di una rete neurale?

---

### Architetture delle Reti Neurali

21. Qual è la differenza tra una rete feedforward e una rete ricorrente?
22. Cosa rappresentano gli strati nascosti in una MLP?
23. Come il numero di unità nascoste influenza la capacità di generalizzazione di una NN?
24. Perché la scelta della funzione di attivazione è fondamentale in una NN?
25. In che modo le NN possono essere viste come un’estensione dei modelli lineari?

---

### Proprietà e Limitazioni delle Reti Neurali

26. Cos’è il problema dell’assegnazione del credito nelle reti neurali?
27. Perché il problema del caricamento (loading problem) è considerato NP-completo?
28. Quali sono le implicazioni del teorema di convergenza del Perceptron?
29. Qual è l’impatto della non linearità delle funzioni di attivazione sulla capacità della rete?
30. Quali sono le principali differenze tra il training di una rete con l’algoritmo di backpropagation e quello del Perceptron?

---

### Backpropagation e Ottimizzazione

31. Come funziona l’algoritmo di backpropagation?
32. Perché le funzioni di attivazione devono essere differenziabili per l’uso di backpropagation?
33. Qual è il significato del gradiente nella discesa del gradiente nelle NN?
34. Perché la scelta dell’iperparametro di apprendimento (learning rate) è critica?
35. Quali problemi possono sorgere durante l’addestramento di una NN e come possono essere mitigati?

---

### Generalizzazione e Overfitting

36. Perché una rete neurale con troppi parametri rischia di overfittare?
37. Qual è il legame tra la dimensione VC e la capacità della rete?
38. Quali strategie possono essere utilizzate per prevenire l’overfitting nelle NN?
39. In che modo la regolarizzazione può aiutare a migliorare la generalizzazione delle NN?
40. Qual è la differenza tra dropout e weight decay come tecniche di regolarizzazione?

---


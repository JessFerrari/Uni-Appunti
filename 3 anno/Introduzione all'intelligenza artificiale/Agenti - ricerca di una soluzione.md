Gli algoritmi di ricerca prendono in input un problema e restituiscono un cammino soluzione.

Lo spazio degli stati è un grafo su cui bisogna trovare il cammino di costo minore per arrivare alla soluzione. su tale grafo si eseguono delle AZIONI per spostarsi sui vari nodi.

L’insieme dei possibili percorsi è molto esteso e in questo va trovato quello con costo minore.

[qui abbiamo fatto dei problemi giocattolo: aspirapolvere, puzzle dell’otto e otto regine, GUARDARE SULLE SLIDES]

→ DIMOSTRAZIONI DI TEORERMI CON AGENTI DI RISOLUZIONE DI PROBLEMI. Si ha un grafo di assiomi e si vuole arrivare alla soluzione con il cammino minimo.

→ problemi reali

## RICERCA AD ALBERO

Si genera un albero di ricerca sovrapposto al grafo dello spazio degli stati, generato delle possibili sequenze di azioni.

Quando si fa una funzione di ricerca su un albero si da come input il problema e si avrà come ritorno o la soluzione o il fallimento.

Se la frontiera è vuota, ossia se non ci sono più nodi figli si restituisce fallimento, altrimenti si scegli un nodo foglia da espandere e si rimuove dalla frontiera.

Se il nodo contiene uno stato obbiettivo ritornare la soluzione corrispondente.

Un NODO n è una struttura dati con 4 componenti

- n.stato
- n.padre
- n.azione (servita per generarlo)
- n.costo-cammino, ossia il costo del cammino dal nodo iniziale ad n, si indica con g(n)

La FRONTIERA è la lista dei nodi in attesa di essere espansi, ossia le foglie dell’albero di ricerca. Viene implementata come una coda con le tipiche operazioni della coda:

- isEmpty(coda)
- Pop(coda), per estrarre il primo elemento
- insert(elemnto, coda)

Diversi tipi di coda hanno diverse funzioni di inserimento ed implementano strategie diverse.

Si hanno 3 tipi di implementazioni di code:

- FIFO, si usa nella BFS (Breadth-first search). Si toglie l’elemento più vecchio
- LIFO, si usa nella DFS (Depht-first search ). Si togli l’elemento più recente
- CODA CON PRIORITà (Si)
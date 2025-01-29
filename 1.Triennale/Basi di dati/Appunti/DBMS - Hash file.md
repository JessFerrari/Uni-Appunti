---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[DBMS - Organizzazione della memoria]]"
tags:
  - BD
Creation: 2024-02-29
---
Obiettivo: noto il valore di una chiave, trovare il record di una tabella con qualche accesso al disco (idealmente 1)

Se ci sono collisioni tra i record è meglio in quanto si trovano nella solita pagina.
Alla funzione hash gli si passa la chiave e ci restituisce la pagina.

- **Metodo procedurale (hash)**
    
    In un file hash i record vengono allocati in una pagina il cui indirizzo dipende dal valore di chiave del record: $key \rightarrow H(key) \rightarrow page \ address$
    
    Una comune funzione hash è il resto della divisione intera: $H(k) = k \ mod \ NP$ Questo metodo si può anche applicare a chiavi alfanumeriche dopo averle convertite. NOTA: L’insieme delle chiavi dovrebbe essere molto più grande dell’insieme dei possibili valori dell’indice.
    
**Svantaggi delle Strutture Hashle
- Se il numero di blocchi è troppo piccolo rispetto al database si hanno frequenti collisioni (con catene di overflow).
- Se il numero di blocchi è troppo grande rispetto al database si ha un fattore di riempimento molto basso.
- La struttura hash non è efficiente per query su un range di valori
- La struttura hash non è efficiente per operazioni che coinvolgono attributi che non sono la chiave.

# Metodo procedurale statico
![[Pasted image 20240229070758.png]]
## Parametri di progetto

- La funzione per la trasformazione della chiave
- Il fattore di caricamento _$d = \frac{N}{M_C}$*
- Capacità $c$ delle pagine
- Metodo per la gestione dei trabocchi

### Fattore di caricamento
Frazione dello spazio fisico disponibile mediamente utilizzata.

Se $N$ è il numero di tuple previsto per il file, $M$ il fattore di pagine e $c$ il fattore di caricamento, il file può prevedere un numero di blocchi $B$ pari al numero intero immediatamente superiore a $d$.

Ci possono essere dei casi, ad esempio per gli inserimenti, che le collisioni potrebbero dare problemi.

## Strutture hash
- Le collisioni di pagine (overflow) sono di solito gestite con linked list. 
- Organizzazione più efficiente per l’accesso diretto basato su valori della chiave con condizioni di uguaglianza (**accesso puntuale**)
- Non è efficiente per _ricerche basate su intervalli_ (e nemmeno per ricerche basate su altri attributi).
- Funzionano solo con file la cui dimensione non varia molto nel tempo (Ecco perché chiamato procedurale _statico_).

### Svantaggi delle strutture hash
- Se il numero di blocchi è troppo piccolo rispetto al database si hanno frequenti collisioni (con catene di overflow).
- Se il numero di blocchi è troppo grande rispetto al database si ha un fattore di riempimento molto basso.
- La struttura hash non è efficiente per query su un range di valori
- La struttura hash non è efficiente per operazioni che coinvolgono attributi che non sono la chiave.
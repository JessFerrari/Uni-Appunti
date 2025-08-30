---
Subject: "[[Indice - Human Language Technologies|HLT]]"
Subject 2: "[[Indice - Information Retrieval|IR]]"
tags:
  - HLT
  - IR
Creation: 2025-04-01
---
# Natural Language Processing
Il *Natural Language Processing* è il processo della normalizzazione ed analisi di un testo per riuscire a comprenderlo e poter restituire dei risultati adeguate.

# Linguaggio
---
Il linguaggio naturale è quello che gli umani utilizzano per comunicare tra di loro.
Questo linguaggio è complesso, è composto da migliaia di simboli, è per la maggior parte composizionale, potenzialmente ambiguo, ed evolve nel tempo.
Il linguaggio naturale è variabile, contiene significati impliciti ed è ricco di relazioni interne ed esterne.
L'85% delle informazioni è in forma non strutturata e principalmente sotto forma di testo.

# Natural Language Understanding
---
Lo scopo del ***Natural Language Processing (NLP)*** è riuscire a processare oil linguaggio naturale per simulare il *Natural Language Understanding*, ossia rendere una macchina capace di capire il linguaggio naturale, elaborarlo e produrre dei risultati usando lo stesso linguaggio. 

Dal punto di vista computazionale il ***Natural Language Understanding*** è considerato un problema *AI-completo*. 

Il Natural Language Processing è costituito da dei task pratici di analisi del testo che semplificano il problema del NLU.

# IR e NLP
---
Anche nei sistemi di [[Information Retrieval|IR]] in cui si utilizzano [[Machine Learning Model|modelli di machine learning]] si esegue dell'elaborazione del testo detta *processing pipeline*, in quanto il testo deve essere rappresentato in maniera adeguata al modello di machine learning.

# Approccio algoritmico
---
Il Natural language processing si focalizza sulla costruzione di modelli per comprendere, analizzare e generare del testo. 
Per farlo deve seguire una pipeline di istruzioni da applicare al testo.
![[Pasted image 20250401121951.png]]
Dato un testo per prima cosa si vogliono *separare le parole*, ma per farlo bisogna avere alcune accortezze come ad esempio :
- non basta separare per lo spazio bianco in quanto alcune parole contengono spazi al loro interno
- Vanno separate alcune parole che, per forma contratta della lingua vengono unite utilizzando punteggiatura (')
- l'apostrofo non sempre separa due parole
Il come separare le parole dipende dalla lingua che si sta usando.

Il processo di separazione si chiama [[Tokenizzazione]] e viene eseguito utilizzando le [[Regular expressions]].

Un'altro elemento della normalizzazione del testo è la [[Lemmatizzazione]] che serve per mappare ogni parola alla propria radice per far assumere il significato corretto alle parole. Un modo per fare lemmatizzazione è attraverso lo *stemming* che semplicemente estrae il suffisso dalle parole.

La normalizzazione di un testo comprende anche la divisione in frasi servendosi della punteggiatura.

Infine si devono compare tra di loro le parole attraverso l'[[Edit distance]], metrica usata per misurare quanto due stringhe si assomigliano.
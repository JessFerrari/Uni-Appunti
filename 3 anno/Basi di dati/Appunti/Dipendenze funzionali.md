---
Subject: "[[Indice - Basi di dati]]"
Super Topic: "[[Normalizzazione di schemi]]"
tags:
  - BD
Esempi: "[[Esempi dipendenze funzionali]]"
Creation: 2024-02-24
---

# Dipendenze funzionali
Le _dipendenze funzionali_ sono una _formalizzazione_ del concetto di vincolo dei dati su un altro dato.

Le dipendenze funzionali sono una proprietà semantica cioè dipendono dei fatti rappresentati e non da come gli attributi sono combinati in schemi di relazione.

Questo _formalismo_ è necessario per analizzare la qualità di un [[Base di dati|Database]] e per poterlo trasformare in [[Forme normali|forma normale]]  

Un'istanza valida di $R$ è una nozione semantica che dipende da ciò che si conosce del dominio del discorso e non è deducibile da altre istanze dello schema.
Se si hanno due concetti non concordanti di ciò che si deve inserire nella base di dati va concordato con il committente. ^3d8c8a

> [!NOTE] Dipendenza funzionale
> _Sia_ 
> - $R(T)$ uno _[[Modello relazionale|schema di relazione]]_ 
> - $r$ un istanza valida di $R(T)$ 
> - $X$ e $Y$ sottoinsiemi di attributi di $T$ 
> 
> _Allora_ una _dipendenza funzionale_ è un [[Conoscenza astratta#^c7fe4d|vincolo d'integrità]] sulle istanze della relazione tale che $$ \begin{array}{} X \rightarrow Y  & \iff &  \forall t_{1},t_{2} \in  r. \ t_{1}[X]=t_{2}[X] \\ & \implies &  t_{1}[Y]=t_{2}[Y] \end{array} $$ 
> OSSIA:
> Esiste in $r$ una dipendenza funzionale da $X$ a $Y$ se PER OGNI coppia di ennuple $t_1$ e $t_2$ di $r$ con gli stessi valori su $X$ risulta che $t_1$ e $t_2$ hanno anche gli stessi valori su $Y$
> 
> Una _dipendenza funzionale_ $X \rightarrow Y$  specifica che, per ogni _istanza valida_ $r$ di $R(T)$, $\pi_{XY}(r)$ è una [[Funzioni|funzione]] con _dominio_ $X$ e codominio $Y$.

 In una _dipendenza funzionale_ $X \rightarrow Y$, si dice che 
 - $X$ determina $Y$,
- $Y$ è _determinato_ da $X$. 



Un istanza $r_0$ di $R$ soddisfa la dipendenza funzionale $DF\ X\rightarrow Y\ (r_0 \models X\rightarrow Y)$ se la proprietà vale per $r_0: \forall t_1, t_2\in r$  : se $t_1[X] =t_2[X]$ allora $t_1[Y]=t_2[Y]$
	Si dice che un’istanza $r_0$ di $R$ soddisfa la dipendenza funzionale $X \rightarrow Y$ (possiamo indicarlo con $r_0 \models X \rightarrow Y$) se la definizione di dipendenza funzionale vale per $r_0$.


_Sia_  $F$  un _insieme di dipendenze funzionali_ $DF$ su $R(T)$, 
_allora_  $r$ è un’_istanza valida_ di $R(T)$, _rispetto_ ad $F$, 
_se_ per ogni $X \rightarrow Y \in F$  è rispettata la definizione di dipendenza funzionale
	Si dice che un’istanza $r_0$ soddisfa un insieme $F$ di dipendenze funzionali se $\forall \: X \rightarrow Y \in F$ vale che $r_0 \models X \rightarrow Y$.

Le _dipendenze funzionali_: 
- _sono definite solo_ all’interno di uno _schema di relazione_, non possono esistere fra attributi appartenenti a _relazioni diverse_
- sono proprietà _intensionali_, legate al _significato dei fatti_ che si rappresentano; non è quindi possibile _inferirle_ dall’osservazione di alcune istanze della relazione. 



> [!note]
> Le _dipendenze funzionali_ sono uno strumento per la verifica della validità della base di dati e per la sua [[Normalizzazione di schemi|normalizzazione]].
> 
>  Sono cosi importanti che i schemi relazionali sono Indicato con $R\langle T,F\rangle$ dove $F$ è una insieme di _dipendenza funzionali_ su $T$


Ogni dipendenza funzionale viene poi tradotta in un [[Conoscenza astratta#^c7fe4d|vincolo d'integrità]].
Bisogna capire quali sono le dipendenze funzionali prima ancora di iniziare a progettare. Quindi non va sbagliata l'analisi dei requisiti


## Chiave
Nel modello relazionale, una [[Modello relazionale - chiave|chiave]] è un sottoinsieme di attributi che identifica unicamente una ennupla.

Con le dipendenze funzionali una chiave è un'insieme di attributi che fa ottenere l'informazione, identifica, di tutti gli altri attributi della relazione (ossia di tutto l'insieme T)

- Se X è una superchiave, allora X determina ogni altro attributo della relazione: X → T 
- Se X è una chiave, allora X → T è una DF completa

Per trovare tutte le chiave si usa la [[Schema relazionale - Ricerca delle chiavi|ricerca delle chiavi]] e per trovare semplicemente una chiava si usa la [[Copertura#^778bbb|copertura con la ricerca e rimozione ]]di [[Copertura#Attributo estraneo|attributi estranei]]

# Dipendenze funzionali atomiche
Ogni dipendenza funzionale $X \rightarrow A_1A_2...A_n$ si può scomporre nelle dipendenze funzionali $X \rightarrow A_1, X \rightarrow A_2, ..., X \rightarrow A_n$ .

Le dipendenze funzionali del tipo $X \rightarrow A$ si chiamano **dipendenze funzionali atomiche**
![[Pasted image 20240224195648.png]]

# Dipendenze funzionali banali
$X \rightarrow A$  è **banale** se $A$ è contenuta in $X$

Esempio:
	La dipendenza funzionale $Impiegato, Progetto \rightarrow Progetto$ è sempre valida, per cui si tratta di una dipendenza funzionale “banale”.

$X \rightarrow A$ è **non banale** se $A$ non è contenuta in $X$

# Dipendenze  funzionali complete

Si parla di **dipendenza funzionale completa** quando $X \rightarrow Y$ e per ogni $W \subset  X$, non vale $W \rightarrow Y$.

Se $X$ è una _superchiave_, allora $X$ determina ogni altro attributo della relazione $X \rightarrow T$.

Se $X$ è una chiave, allora $X \rightarrow T$ è una dipendenza funzionale completa.

# [[Dipendenze funzionali derivate|Dipendenze implicate]]
In generale da un insieme F di dipendenze funzionali sono “implicate” altre dipendenze funzionali da F.
![[Pasted image 20240224214147.png]]

Sia $F$ un insieme di DF sullo schema $R$, diremo che $F$ implica logicamente $X \rightarrow Y$ $(F \models X \rightarrow Y)$ se ogni istanza $r$ di $R$ che soddisfa $F$ soddisfa anche $X \rightarrow Y$.

Una dipendenza banale è quella implicata dal vuoto $(\{ \} \models X \rightarrow X)$.

## Manipolazione di clausole
![[Pasted image 20240224233054.png]] ![[Pasted image 20240224233121.png]]
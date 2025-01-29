## Sintassi

La sintassi definisce quali sono le frasi legittime, ossia BEN FOMATE, del linguaggio

$$ formula \rightarrow formulaAtomica \ |\ formulaComplessa \\ formulaAtomica\rightarrow True\ |\ False\ |\ simbolo\\ simbolo\rightarrow P\ |\ Q\ |\ R\ | ...\\ formulaComplessa \rightarrow \neg formula\\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ |\ (formula \wedge formula) \\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ |\ (formula\vee formula) \\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ |(formula \Rightarrow formula)\\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ |(formula \Leftrightarrow formula) $$

Precedenza tra operatori:

$$ \neg >\wedge>\vee>\Rightarrow, \Leftrightarrow $$

Si può decidere la precedenza anche con le parentesi:

$\neg P\vee Q\wedge R\Rightarrow S$ è la solita cosa di $(((\neg P)\vee (Q\wedge R))\Rightarrow S)$

## Semantica

La semantica ha a che fare con il significato delle frasi : definisce se un enunciato è vero o falso rispetto a una interpretazione, ossia un mondo possibile.

Un’interpretazione definisce un valore di verità per tutti i simboli proposizionali.

Il valore di una formula complessa è fissato di conseguenza all’interpretazione.

Un MODELLO di una formula è una interpretazione che la rende vera.

Esempio:

- interpretazione : $\{P_{1,1}=true, \ P_{1,2}=false, \ W_{2,3}=true\}$
- formula : $P_{1,1}\Rightarrow W_{2,3}\vee P_{1,2}$ , è vera nella interpretazione

## Semantica composizionale

Il significato di una frase è determinato dal significato dei suoi componenti, a partire dalle frasi atomiche:

- $True$ è sempre vero; $False$ è sempre falso
- $P\wedge Q$ vero se P e q sono entrambi veri
- $P\vee Q$ vero se P o Q o entrambi sono veri
- $\neg P$ vero se P è falso
- $P\Rightarrow Q$ vero se P è falso o Q è vero
- $P\Leftrightarrow Q$ vero se entrambi veri o entrambi falsi

## Conseguenza logica

Una formula $\alpha$ è consegua logica di un insieme di formule KB se e solo se in ogni modello di KB $\alpha$ è vera ($\alpha \models KB$)

Indicando con M(KB) i modelli dell’insieme di formule in KB e con $M(\alpha)$ l’insieme delle interpretazioni che rendono vera $\alpha$ (ossia i modelli di $\alpha$)

$$ KB\models\alpha \Leftrightarrow M(KB)\subseteq M(\alpha) $$

## Equivalenza logica

$$ \alpha \equiv \beta \Leftrightarrow \alpha \models \beta \wedge\beta\models \alpha $$

Una formula $\alpha$ è equivalente alla formula $\beta$ se e solo se $\alpha$ è conseguenza logica di $\beta$ e $\beta$ è conseguenza logica di $\alpha$



## Validità e soddisfacibilità

Una formula $\alpha$ è valida se e solo se è vera in tutte le interpretazioni, ossi se è una TAUTOLOGIA

ES : $\alpha =A\vee\neg A$

Una formula $\alpha$ è soddisfacibile se e solo se esiste un’interpretazione in cui $\alpha$ è vera, ossia se esiste un MODELLO di $\alpha$

Ne discende che:

- $\alpha$ è valide se e solo se $\neg\alpha$ è insoddisfacente
- $\alpha$ è soddisfacibile se solo se $\neg\alpha$ non è valida![[Equivalenze logiche.png]]
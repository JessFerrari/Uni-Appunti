Si parla di agenti che vivono in un ambiente e che hanno dei sensori con i quali hanno percezioni che servono per descrivere come il mondo si evolve e l’effetto delle azioni che l’agente compie.

Con le condition-action rule si descrivono gli effetti che si hanno dopo aver selezionato una determinata azione da compiere sull’ambiente.

La maggior parte dei problemi di IA sono knowledge intensive in quanto il mondo su cui l’agente deve lavorare è molto complesso. Per questo è necessaria una rappresentazione PARZIALE ed INCOMPLETA.

Per ambienti PARZIALMENTE OSSERVABILI e COMPLESSI servono dei linguaggi di rappresentazione della conoscenza ESPRESSIVI e con CAPACITÀ INFERENZIALI.

La conoscenza può essere codificata a mano, essere estratta da testi e/o esperti o essere appresa con esperienza.

## Approccio dichiarativo vs procedurale

La knowledge based racchiude tutta la conoscenza necessaria a decidere l’azione da compiere in forma dichiarativa.

→ un agente KB è più flessibile di uno procedurale in quanto è semplice acquisire conoscenza incrementale e modificare il comportamento con l’esperienza

L’approccio procedurale consiste invece nello scrivere un programma che implementa il processo decisionale una volta e basta.

La soluzione migliore è la combinazione dei due approcci.

## Agente basato su conoscenza

Un agente basato su conoscenza mantiene una BASE DI CONOSCENZA (KB), ossia un insieme di enunciati espressi in un linguaggio di rappresentazione.

Interagisce con la KB mediante un’interfaccio funzionale TELL-ASK , la quale è composta da tre funzioni :

- TELL : per aggiungere enunciati
- ASK : per interrogare la KB
- RETRACT : per eliminare enunciati

Gli enunciati nella KB rappresentano le OPINIONI E LE CREDENZE DELL’AGENTE.

Le risposte $\alpha$ devono essere tali che $\alpha$ discende necessariamente da KB.

### Problema:

Data una base di conoscenza KB, contenente una rappresentazione dei fatti che si ritengono veri, come dedurre che un certo fatto $\alpha$ è vero di conseguenza?

## Programma di un agente KB

```jsx
function AgenteKB (percezione) return azione
	persistent : 
							- KB, base di conoscenza
							- t, contatore inizializzato a 0 che indica il tempo

function AgenteKB (percezione){
	KB[];
	var t = 0;
	KB.tell(costruzioneFormulaPercezione(percezione, t))
	azione = KB.ask(costruzioneQueryAzione(t))
	KB.tell(CostruzioneFormulaAzione(azione, t))
	t = t+1
	return azione;
}

```

## Base di conoscenza vs base di dati

Una base di conoscenza è una rappresentazione esplicita, parziale e compatta, in un linguaggio simbolico che contiene :

- fatti di tipo specifico
- fatti di tipo generale (o regole)

Una base di conoscenza è caratterizzata dalla capacità INFERENZIALE.

Una base di dati contiene solo fatti specifici che si possono solo recuperare.

## Rappresentazione della Conoscenza

Più il linguaggio è espressivo meno efficiente è il meccanismo inferenziale.

Il problema fondamentale è trovare il giusto compromesso tra espressività del linguaggio di rappresentazione e complessità del meccanismo inferenziale.

Un formalismo per la rappresentazione della conoscenza ha tre componenti:

1. una SINTASSI, ossia un linguaggio composto da un vocabolario e regole per la formazione delle frasi
2. una SEMANTICA, che stabilisce una corrispondenza tra gli enunciati e i fatti del del mondo; se un agente ha un enunciato $\alpha$ nella sua KB, crede che il fatto corrispondente sia vero nel mondo
3. un MECCANISMO INFERENZIALE che consente di definire nuovi fatti![[Agenti-Bassati-Canoscenza.png]]
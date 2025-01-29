Si suppone di scommettere su l'estrazione di una carta da un mazzo di 52 carte :

- Si scommette 1€ per un k di cuori e se esce vinco 52€
- Si scommette 1€ per una qualsiasi carta di fiori e se esce vinco 4€

[questo è un esempio di gioco onesto, più avanti la definizione]

Qual è la probabilità di vincere?

> SI HA UNA FUNZIONE SULL'ESTRAZIONE, la probabilità non è su che carta esce ma sulla vincita e perciò si deve considerare un universo diverso

Si ha $\Omega$ universo delle estrazioni e $P=probabilità \ su \ \Omega$. Si deve creare una funzione di vincita che va da $\Omega$ ad un numero reale : $X=\Omega \to \R$

- X (k di cuori) = 50 [52-2]
- X (carta di fiori) = 2 [4-2]
- X (qualsiasi altra carta) = -2

TRAMITE QUESTA FUNZIONE TRASPORTO LA PROBABILITÀ DA $\Omega$ a $\R$ ed ottengo UNA PROBABILITÀ DISCRETA

$P_X(50)=P(X=50) = P(\{\omega \in \Omega|\ X(\omega) =50\}) =P(X^{-1}(50))=1/52$

$P_X(2)=P(X=2) = P(\{\omega \in \Omega|\ X(\omega) =2\}) =P(X^{-1}(2))=13/52=1/4$

$P_X(-2)=P(X=-2) = P(\{\omega \in \Omega|\ X(\omega) =-2\}) =P(X^{-1}(-2))=38/52$

$P_X(x) = P(X=x)=0 \ se \ x \ne \{-2, 2.50\}$
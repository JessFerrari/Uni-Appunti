---
Subject: "[[Indice - Architetture e Sistemi Operativi|AESO]]"
Super Topic: "[[Sistemi di IO]]"
tags:
  - AESO
Creation: 2025-02-24
---
Solo il sistema operativo può comandare i device di I/O. 
Non vengono gestiti direttamente dall'utente e questo può fare solo delle richieste attraverso system call.

Il sistema operativo per fare I/O su un dispositivo lo fa in due modi:
1. I/O instruction: Istruzioni dedicate, istruzione del sistema architetturale per fare richieste sui dispositivo. L'utente standard non le può fare. Veniva usato nell' Intel IA-32 e nel IBM370.
2. Memory mapped I/O: È il più usato, utilizzo load e store. Il processore si interfaccia con il dispositivo con load e store attraverso indirizzi particolari, che vengono riservati per i servizi di I/O. La CPU emette degli indirizzi per l'accesso alla memoria che passano alla MMU e questa se vede gli indirizzi particolari portal'operazione ai dispositivi di I/O. Se l'utente accede a questi indirizzi verrà generata un'eccezione e il programma viene terminata (segmentation fault).

## COME FACCIO A CAPIRE CHE L'OPERAZIONE È TERMINATA?

Ci sono due approcci:
1. Programmed I/O : in cui la CPU ha diretto controllo
2. Interrupt-driven I/O : ci sono interruzioni, eventi asincroni, che viene inviato da un dispositivo per notificare un evento. Sono asincroni perché non si sa quando arrivano.

Spesso le eccezioni vengono chiamate interruzioni, che sono eventi sincroni generata da un'istruzione, ma non c'entrano nulla con i dispositivi di I/O.

## PROGRAMMED I/O (POLLING)

La CPU che ha un ruolo attivo nell'invio dei comandi e nel controllo dello stato, ossia controlla lo stato dell'operazione, fin quando non arriva una risposta la CPU continua a controllare lo stato (polling) e quando è finita continua a fare le sue operazioni. Ad esempio in un'operazione di read fa polling fino a quando non verrà letto il dato e poi lo andrà a mettere in memoria.
Questo approccio ha come vantaggi che è semplice, che richiedere la presenza solo del memory mapped I/O ed è molto reattivo , ossia quando si stabilizza ce ne si accorge subito, ma vengono sprecate risorse infatti la CPU deve aspettare senza fare lavoro utile.

## INTERRUPT-DRIVEN I/O : 
(viene spiegato bene dopo)
È più complesso dal punto di vista architetturali ma ha copre lo svantaggio principale dell'altro approccio in quando non vengono sprecate risorse in quanto quando il dispositivo è pronto genera un interruzione la CPU se ne accorge gestisce l'interruzione e fa l'operazione che doveva fare. 
Prima dell'interruzione la CPU continuava a fare le sue cose.

### PASSI:

C'è una parte che riguarda l'hardware e una il SO. 
Per l'hardware deve esserci un meccanismo che genera segnali di interruzioni e il processore deve avere qualcosa per accorgersi diquesti segnali e poterle gestire ed eseguire.
Quando arriva un'interruzione e la CPU stava eseguendo qualcos'altro la CPU va a salvare quello che stava facendo, e ciò è eseguitodal kernel del SO, e dopo che la CPU ha fatto con il device il SO va a ripristinare i registri.

### IMPATTO
Se faccio polling con un dispositivo a bassa banda, ad esempio il mouse, facendo i vari conti vedo che ho un impatto basso, con unoverhead accettabile. Mentre se lo faccio su un dispositivo ad alta banda l'impatto è molto più alto e quindi è "inutile" fare il polling,perché se ci metto più tempo a fare polling rispetto alla velocità del dispositivo rischio di perdere dati.
Con le interruzioni invece, sul dispositivo ad alta banda, il processore riceve un interruzione ogni volta che i dati sono stati trasferiti,spendo comunque lo stesso tempo ma nel mentre la CPU fa altro.
Però c'è anche da considerare che la CPU deve gestire il trasferimento dei datiPer non utilizzare la CPU ma far fare al dispositivo il trasferimento autonomo aggiungendo il DMA controller e la CPU deve solo fare il completamento.

### FUNZIONAMENTO : 
c'è un controller specializzato, mando il comando al DMA e quando il DMA ha finito manda l'interruzione. Questa attività in più si paga ma non in termini di cicli di CPU.

La CPU quando vuole interfacciarsi con il dispositivo di I/O manda alla MMU l'indirizzo speciale e manda il comando sul bus di I/O dove c'è anche attaccato il DMA che è in grado di comunicare con il dispositivo e trasferire tramite il system bus i dati che voglio leggere o prendere dalla memoria i dati che voglio scrivere sul dispositivo.

La gestione dell'interruzione è una cosa complessa che il processore gestisce in punti ben precisi, in particolare nel processor cycle.

### DMA BREAKPOINT: 
Si è attaccato un dispositivo in più sul system bus che fa concorrenza alla CPU e crea problemi in quanto ci deve essere un arbitro che sceglie tra DMA e CPU, e tra i due ha precedenza il DMA in quanto devo prima finire di scrivere se no si vanno a fare danni mentre la CPU si può mettere un attimo in stallo anche se perdo cicli.

Si ha quando si cerca di accedere alla memoria, il DMA breakpoint stalla la CPU mentre l'interrupt breakpoint non stalla la CPU ma la CUP controlla le interruzioni e le gestisce (salva ciò che aveva , esegue il nuovo codice e ripristina).

#### Quanto costa dover gestire i trasferimenti in DMA in ordine di cicli di CPU?

Supponendo di avere una CPU da 500MHz, un disk device con 4MB/s di transfer rate, un'interfaccia da 16GB utilizzata al 50%.
Abbiamo delle interruzioni che costano 400 cicli e il data transfer ne costa 100, e in più sappiamo che DMA setup costa 1600 cicli e può trasferire 16KB a volta.

Una volta fatto il setup il DMA non paga più cicli.

- Senza DMA costa:$0.5 * (4 MB/s) / (16 B) * [ ( 400 + 100 ) cicli / 500 M cicli/s ] = 12\%$
- Con DMA : $0.5 * (4 MB/s) / (16 B) * [ ( 1600 + 400 ) cicli / 500 M cicli/s ] = 0.05\%$

### DMA NELLA GERARCHIA DI MEMORIA

Nel caso che non ci sia DMA il processore fa tutto da solo e non ha limitazioni (lavora con indirizzi logici sparpagliati se lavora da solo invia solo questi e l' MMU fa la traduzione da logico a fisico). 
Non ho impatti nella gerarchia di memoria.

Se metto un DMA control si ha un problema riguardate il tipo di indirizzi con cui lavoro e un problema di coerenza di dati in memoria. 

Se si utilizza il virtual DMA, ossia un DMA in grado di lavorare con indirizzi logici, allora anche il DMA controller deve avere una "MMU" interna, che è una cache chiamata TLB contenente le associazioni tra indirizzo logico e fisico, è molto complesso ma anche flessibile.

Se si utilizza un DMA che lavora con indirizzi fisici ha una granularità più piccola, della singola pagina, è meno flessibile ma più semplice 

### COERENZA E CONSISTENZA
Il DMA pone problemi di coerenza per le cache come avviene per il multicore.
Con una politica write-back quando scrivo in una linea di cache aggiorno la memoria solo quando devo buttare fuori quel blocco.
E nel caso il DMA sta scrivendo su quella zona lì si ha un problema di coerenza. Bisogna quindi invalidare le linee di cache, si usa un protocollo.

### ACCESSO AI DEVICE
Se devo considerare un accesso ad un dispositivo lato utente si possono fare solo system call, ad esempio la fread che a sua volta ne fa un'altra, la read.
Se faccio una fread di un byte non viene letto un byte ma 4K, se la tiene in un buffer, ci restituisce quello che volevamo e in una seguente fread va a cercare direttamente nel buffer perché le chiamate di sistema costano.

Manca la parte su device driver

### Operazione di lettura su dispositivo :
Viene fatta una richiesta su un dispositivo, ossia una system call, che viene intercettata, può essere eseguita (perché magari c'erano già i dati nel buffer del driver) se no devo spedire una richiesta al dispositivo, il driver manda tutti i comandi di controllo, il dispositivo deve avere una sorta di monitoraggio dell'interruzione e poi il device controller manda l'interruzione che scatena l'interruzione della CPU da parte del sistema operativo, viene identificato il driver che si occupa di copiare i dati dal kernel allo spazio utente e poi dirà che ha finito.
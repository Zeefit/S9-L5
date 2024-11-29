L’obiettivo di questa attività è stato analizzare un cattura di traffico di rete per identificare Indicatori di Compromissione (IOC), 
formulare ipotesi sui possibili vettori di attacco e proporre contromisure per mitigare gli effetti di un attacco in corso o prevenirne di futuri.

L’analisi del traffico catturato è stata eseguita utilizzando un tool di analisi (Wireshark) e si è concentrata sull’identificazione di comportamenti anomali che potessero indicare un attacco in corso. 
Di seguito,i dettagli delle evidenze trovate.

Durante l’analisi sono stati identificati i seguenti IOC:

Pacchetti TCP con flag RST, ACK:

Numerosi pacchetti di tipo RST, ACK sono stati inviati tra l’host 192.168.200.100 e il target 192.168.200.150.
Questo pattern può indicare:
Una risposta di chiusura forzata da parte del server per connessioni indesiderate.
Un possibile TCP Reset Attack da parte di un attaccante.
Numerosi pacchetti SYN senza completamento di handshake:

L’indirizzo 192.168.200.100 ha inviato molteplici richieste SYN verso 192.168.200.150, ma queste non sono state seguite da handshake completi.
Questo comportamento è tipico di:
Un SYN flood attack (DoS).
Un port scanning, volto a individuare porte aperte sul target.

Un pacchetto BROWSER proveniente da 192.168.200.150 verso l’indirizzo di broadcast 192.168.200.255.
Il pacchetto fa riferimento a Metasploitable, un sistema noto per essere vulnerabile. Ciò suggerisce che il sistema target potrebbe essere già compromesso o esposto ad attacchi.

Comportamento anomalo nei timestamp TCP:
I campi TSval e TSecr presentano valori ripetitivi o sospetti, segno di possibile generazione automatizzata del traffico, ad esempio tramite uno script o un framework di exploit come Metasploit.
Traffico distribuito su molteplici porte:

Sono state rilevate connessioni verso porte diverse, tra cui:
443 (HTTPS): Utilizzato da servizi web sicuri.
3389 (RDP): Utilizzato per il Remote Desktop.
80 (HTTP): Utilizzato per servizi web non sicuri.
Questo suggerisce un tentativo di ricognizione o exploit.

Ipotesi sui vettori di attacco
Dai dati raccolti, si possono formulare le seguenti ipotesi sui possibili vettori di attacco:

Port scanning:
Un attaccante sta cercando di identificare porte aperte o servizi attivi sul target 192.168.200.150.
Denial of Service (DoS):
L’invio massiccio di pacchetti SYN potrebbe sovraccaricare il sistema, impedendo connessioni legittime.
Tentativo di exploit:
L’attaccante potrebbe sfruttare vulnerabilità note su servizi specifici (es. RDP, HTTP o HTTPS) una volta identificate le porte aperte.
Compromissione precedente:
Il riferimento a Metasploitable suggerisce che il sistema 192.168.200.150 potrebbe essere una macchina vulnerabile o già compromessa, che l’attaccante sta ulteriormente sondando o sfruttando.

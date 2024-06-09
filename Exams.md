# Domande Mobile Systems M

## 16/06/2022 Candidato 1 (voto 20)

### Comunicazioni Wireless
1. Si parli dei problemi dell’hidden node e exposed node
2. Maca per WiFi risolve questi problemi?
3. Caratteristiche del protocollo MACA
4. Per quanto tempo i nodi stanno in silenzio?
5. Il problema dell’exposed node è risolto da MACA?
6. Come può in nodo mobile interagire con questo protocollo?
7. Differenze tra SCO e ACL in Bluetooth

### Android
1. Come funzionano gli intent in android?
2. Come può essere mandato un intent? Unicast multicast broadcast
3. Quali sono le api relative all’intent
4. È android che fa match degli intent con l’activity
5. Come avviene il match tra intent e l’activity?
6. Cosa succede se ci sono più app che matchano l’intent?
7. Come si registra il braodcast receiver presso gli intent a cui è interessato?

### Mobile Ip
1. Cosa succede nell’handoff in mobile Ip
2. Cosa succede quando l’MH si sposta in una località diversa
3. C’è perdita di pacchetti?
4. Durante lo spostamento in una località i pacchetti continuano ad arrivare all’fa?
5. Il vecchio fa effettua la ritrasmissione dei pacchetti ?
6. Mobile ip è reattivo o proattivo?
7. È verticale o orizzontale?

## 16/06/2022 Candidato 2 (voto 30)

### Wireless Communication
1. GSM
2. Come avviene la gestion dell’handoff in GSM?
3. GSM wireless communication
4. Reattivo o proattivi?
5. Ci possono essere perdite di pacchetti?
6. Durante una chiamata lunga si crea una catena?

### MANET
1. AODV
2. Come sono fatte le tabelle ?
3. Come viene gestito il link fault?
4. Cosa succede in caso di loop?
5. Cosa succede se nessuno ha un path verso la d dopo il fault?
6. Cosa si intende per protocollo ibrido?

### Android
1. Si parli degli asynctask
2. Come vengono gestiti i thread?
3. Lo sviluppatore deve estendere AsyncTask?
4. I thread devono essere istanziati?
5. Cosa comporterebbe non avere gli asynctask?

### Service discovery UPnP
1. Parlare del supporto alle notifiche
2. Se ci sono molti control point registrati per lo stesso evento come viene gestita la propagazione? (No ottimizzato)

## 16/06/2022 Candidato 3 (voto 30, esame con attività progettuale su iot con uso di mqtt)

### Internet of things
1. Mqtt quali sono le semantiche dei messaggi?
2. Vantaggi dell’applicare la crittografie al payload del messaggio o a tutto il messaggio
3. Con payload encription si può cifrare tutto il payload o anche solo parti?
4. Ci sono modi per non asofraccaricare il broker con la decription nel caso in cui sia cifrato l’intero messaggio?

### Gestione degli eventi
1. Modalità di propagazione delle Subscription in convering based routing?
2. Come si risolve il problema della cancellazione delle sottoscrizioni più generali?

### MANET e Routing
1. Parlare di gpsr
2. Greedy forwarding
3. Perimeter forwarding
4. Come viene costruito il grafo per il perimeter forwarding?

### Sistemi di posizionamento
1. Differential GPS (D-GPS)
2. Differenza tra precisione e accuratezza
3. Perché non si risolve il multipath fading?

## 16/06/2022 Candidato 4 (voto 25)

### Wireless communication
1. Bluetooth
2. Differenze tra SCO e ACL

### Mobile ip
1. Differenze tra ipv4 e ipv6
2. Problemi scarto pacchetti ingresso e uscita?
3. Il problema di avere lo stesso indirizzo c’è anche in ip v4?
4. Perché mipv6 non è usato ?
5. In mipv4 si possono perdere pacchetti succede anche in mipv6 con il tunneling?

### Android
1. Multithreading in android
2. Differenze tra service bound o unbounded?
3. Api per definire bound e unbound services?
4. Dal punto di vista dei thread come si gestiscono i service?
5. Se sono dentro la stessa app come sono assegnati i thread?

### Sistemi di posizionamento
6. Differenza tra Ekahau e Radar

## 16/06/2022 Candidato 5 (voto 30L)

### Wireless Communication
1. GSM come viene gestito l’handoff nella stessa località?
2. Come viene gestito tra località diverse?
3. Viene mantenuta la catena di msc?
4. Può esservi la perdita di pacchetti nell’handoff?
5. Zigbee quali sono le topologie?
6. Quali sono i ruoli?

### MANET
1. Come funziona il flooding ?
2. Quando viene utilizzato?
3. Come si può ottimizzare?
4. Broadcast storm issue?

### Mobile ip
1. Differenze tra mipv4 e mipv6?
2. Ottimizzazioni del triangular routing?
3. Problema di mipv6 perché è poco adottato?
4. Ottimizzazioni presenti?

### Android
1. Asyntask
2. Primitive di asynctask
3. Come sono suddivisi i thread
4. Quali alternative sono possibili all’uso di asynctask
5. Sicurezza in android
6. Come fa un app che non contiene al suo interno un file ad accedere al file di un'altra app? (Condivide gid)
7. Come si accede al file system in android?

## 2023 - Candidato A.Z.

### MANET e Routing
1. AODV
2. Che cosa accade in caso di link error?
3. Si possono formare dei loop?

### Positioning
1. GPS

### Mobile IP
1. Mobile IP in generale
2. Handoff in Mobile IP
3. Principali differenze con Mobile IPv6

## 2023 - Candidato F.A. (voto 30)

### Comunicazione Wireless
1. Hidden node/exposed node issues
2. MACA

### MANET e Routing
1. AODV

### Positining Systems
1. Radar vs Ekahau

### Android
1. Intent e IntentFilter
2. BroadcastReceiver

## 25/01/2024 - Candidato M.R. (voto 30, in Inglese)

### Comunicazione Wireless

1. Bluetooth ACL/SCO abbastanza nel dettaglio
2. Perché in SCO c'è il massimo di 3 slot? (Perché altrimenti si potrebbe facilmente "rubare" banda ad ACL (64*3 è già parecchio, mentre ACL ha max 500))
3. ZigBee + paragone con Bluetooth, e ZigBee channel access options (roba coi beacon e i due modi di utilizzo)
4. GSM handoff (solo sotto lo stesso MSC)
5. MACA + Hidden Node/Exposed Node

### Android

1. Tutto su Intent/IntentFilter
2. Tutto su Broadcast/BroadcastReceiver, paragone con Intent/IntentFilter
3. Nel mezzo qualche domanda sul sistema in generale (DVM, etc.)

---

## Extra

### Domande Varie

- HIP
- Bluetooth
- UPnP
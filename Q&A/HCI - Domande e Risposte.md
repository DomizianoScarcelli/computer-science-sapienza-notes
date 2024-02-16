# Domande e Risposte

## Wearable Devices

- Perchè l'interazione con i Wearable Devices richiede poca attenzione?
    - Perchè generalmente sono devices che non richiedono troppa interazione, e si limitano a raccogliere dati per monitorare cose come la salute fisica ed il sonno. Molte delle azioni effettuate dai dispositivi indossabili sono basate sul contesto, altre azioni si possono invece effettuare con dei gesti, ad esempio una notifica su uno smartwatch può essere letta semplicemente girando il polso.
- Cosa si intente per *constancy* (o constanza) nei wearable devices?
    - Per *constancy* si intende il fatto che spesso i wearable devices non necessitano accensione o spegnimento, ed effettuano molte azioni in maniera automatica.
- Perchè i wearable devices vengono definiti "programmabili dall'utente"?
    - Perchè sono altamente personalizzabili, ed imparano a riconoscere le abitudini di chi li indossa.
- Cosa si intende con la frase "human in the loop" nel contesto dei wearable devices? Di che loop si parla?
    - Con *Human in the loop* si intende che la persona viene usata come feedback per la macchina, e la macchina come feedback per la persona. L'utente non è quindi un fruitore passivo del dispositivo, ma fornisce dei dati a questo, come ad esempio i dati circa l'attività fisica, che poi vengono interpretati da un algoritmo e mostrati in maniera che l'utente li possa interpretare.
- In che senso i wearable devices hanno come elemento principali i dati? (all about the data)
    - Perchè catturano ed analizzano una grande quantità di dati, in maniera da mostrare informazioni utili circa questi. I dati possono essere relativi alla salute mentale e fisica.
- Quali sono i vari tipi di interruzioni che un sistema può fare ad un utente? Fai un esempio per ognuno.
    - Le possibili interruzioni che un sistema può fare sono:
        - **Immediate**: forzano l'utente a cambiare attività e prestare attenzione immediatamente. Un esempio di tali interruzioni possono essere una chiamata, oppure un'allarme di qualche tipo.
        - **Negoziate**: notificano l'utente, senza però la necessità che questo presti subito attenzione. Un esempio è una semplice notifica di email oppure un messaggio.
        - **Programmate**: notificano l'utente periodicamente, un esempio è la sveglia, oppure un evento ricorrente sul calendario.
        - **Mediate**: sono interruzioni date dal contesto in cui l'utente si trova. Un esempio possono essere le notifiche relative alla navigazione attuale, oppure quando è previsto il prossimo autobus in caso ci si trovi vicino ad una fermata.
- Elenca qualche tipo di wearable device antico.
    - Uno dei primi dispositivi indossabili risale al 1600 e si tratta di un abaco all'interno di un anello. Uno dei più famosi, e tuttora utilizzati, è l'orologio da polso, inventato nel 1800. Poi possiamo trovare altri dispositivi come la calcolatrice digitale inserita all'interno dell'orologio da polso, oppure i primi tentativi di caschi per realtà virtuale.
- Qual è la differenza tra sensore ed attuatore?
    - I sensori acquisiscono dati relativi all'ambiente; mentre gli attuatori ricevono dati da sensori ed effettuano delle azioni su dispositivi meccanici.
- In che modo l'utente può interagire con un Wearable Device?
    - Lo schermo del dispositivo può essere touch, l'interazione può a volte avvenire tramite input vocale, oppure tramite gestures. Una gesture per gli smartwatch è ad esempio il girare il polso per attivare lo schermo, oppure coprire lo schermo con il palmo per disattivare una sveglia o timer.
- Cosa si intende per *eyes-free interaction*?
    - Per *eyes-free interaction* si intende quel tipo di interazione che non richiede l'attenzione visiva. Spesso perchè l'input viene dato con delle gestures o tramite la voce, e quindi l'utente non necessita di guardare da nessuna parte, e l'output tramite feedback tattile o audio.
- Quali sono i casi d'uso per i Wearable Devices?
    - I casi d'uso possono essere il monitoraggio dell'attività fisica e del sonno, la realtà aumentata e virtuale, oltre che per scopi medici.

## Internet of Things

- Cosa si intende per Internet of Things?
    - Per IoT si intende l'insieme di quegli oggetti che sono in qualche modo collegati ad internet. Non è necessario che siano collegati direttamente ad Internet, ma possono anche essere collegati ad un dispositivo che poi ha l'accesso ad Internet.
- Fammi un esempio di dispositivi che appartengono all'IoT.
    - Esempi possono essere elettrodomestici smart, che quindi si collegano al WiFi casalingo e possono essere controllati attraverso un'applicazione dedicata, così come sistemi di illuminazione smart, oppure orologi che si connettono ad internet per sincronizzare automaticamente l'orario. Un altro esempio sono anche gli AirTag e altri dispositivi del genere, che non si collegano direttamente ad Internet, ma si collegano al dispositivo vicino, il quale si connette ad internet e consente di aggiornare la posizione dell'AirTag rilevato.
- Quali sono le limitazioni dei dispositivi IoT?
    - Il limite principale è lo spazio disponibile ed il costo, che costringe i produttori ad utilizzare componenti minimali e a basso consumo energetico, anche perchè spesso questo tipo di oggetto viene alimentato da una batteria. Proprio per questo motivo bisogna progettare attentamente il sistema per inserire solamente le funzionalità e l'hardware strettamente necessario.
- In che maniera si può mandare un input ai dispositivi IoT? Elenca anche i pro ed i contro.
    - Si può dare un input ai dispositivi IoT in diverse maniere, ed attraverso diversi dispositivi, tra cui:
        - Controlli fisici, i quali sono comodi perchè possono essere percepiti in maniera tattile, e quindi non richiedono molta attenzione, inoltre la loro posizione è fissa. Tra i vari controlli fisici troviamo:
            - Bottoni, i quali permettono di effettuare un'azione ma non conservano lo stato.
            - Switches, simili ai bottoni, ma rimangono in posizione una volta attuati. Sono comodi perchè permettono di vedere in che stato è il sistema. Questo non è sempre il caso, perchè se lo stato può essere cambiato anche in altre maniere (altro bottone, switch o applicazione) allora lo stato del sistema non è più quello mostrato sullo switch.
            - Manopole, le quali possono essere con rotazione finita o infinita, e che possono permettere di controllare un qualche valore in maniera discreta o continua. Le manopole a rotazione finita permettono anche di vedere lo stato del sistema, a differenza di quelle con rotazione infinita, il cui stato va mostrato in un'altra maniera.
        - Schermi Touch: fanno sempre parte dei controlli fisici, ma sono differenti da questi visto che possono cambiare il contenuto che viene mostrato. Come contro c'è il fatto che i controlli non sono tattili e la loro posizione non è fissa, richiedendo quindi anche una grande quantità di attenzione.
        - UI Tangibili: consentono di muovere oggetti fisici per dare un input al sistema. Sono comodi perchè intuitivi, inoltre la posizione dell'oggetto fisico descrive lo stato del sistema, però possiedono numerose limitazioni, come il fatto che spesso richiedono molto spazio.
        - Riconoscimento Vocale: comodo perchè *hand-free* ed *eyes-free*, inoltre è economico perchè basta inserire un microfono ed un modulo per la connessione ad internet, ed il resto della computazione viene effettuata sul cloud. Il contro è che non sono molto affidabili, ed in generale l'utente non si sente in controllo rispetto ad altre interfacce più tradizionali.
        - Gestures: permettono di interagire con il sistema facendo dei gesti con il corpo, sono comode perchè non richiedono molta attenzione, ma raramente sono precise.
        - Contesto: permette al dispositivo di effettuare delle azioni in maniera autonoma basandosi sul contesto in cui l'utente si trova in quel momento.
        - Altri parametri come battito cardiaco o altri fattori corporei.
    - Vi sono inoltre anche altre tecnologie in via di sviluppo come la possibilità di comunicare tramite le onde cerebrali.
- In che maniera si può ricevere un output ai dispositivi IoT? Elenca anche i pro ed i contro.
    - Un dispositivo IoT può comunicare all'utente tramite diversi mezzi, tra cui:
        - **LED**: l'informazione viene trasmessa tramite un led, il quale può eventualmente cambiare colore e lampeggiare. I led possono ovviamente essere più di uno, e quindi aumentare la quantità di informazione che può essere trasmessa. I suoi pro sono il fatto che un LED è molto economico, occupa poco spazio ed utilizza pochissima energia, inoltre richiede poca attenzione da parte dell'utente. Ovviamente la quantità di informazione che si può trasmettere è molto limitata.
        - **Schermi**: sono in grado di trasmettere una grandissima quantità di informazione. A seconda di tale quantità, si possono utilizzare diversi tipi di schermi.
            - I *7-segment displays* permettono di rappresentare ogni cifra con un pattern di soli 7 segmenti. Sono molto economici e vengono utilizzati soprattutto in sveglie ed orologi.
            - Negli e-book vengono utilizzati gli schermi e-ink, che sono poco costosi in termini di energia, visto che i pixel rimangono in posizione una volta inseriti in quello stato, e non emettono luce propria, proprio per questo danno una sensazione molto cartacea e non urtano gli occhi. Tale tecnologia non permette di rappresentare i colori.
            - Per trasmettere informazioni più complesse c'è bisogno di schermi tradizionali, a colori o in bianco e nero.
            - In generale è una buona idea chiedersi se una certa feature che utilizza uno schermo ne ha davvero bisogno, in modo da evitare il *feature creep*, situazione in cui il prodotto viene riempito di funzionalità, la cui abbondanza rovina l'esperienza.
        - **Suoni e Text to Speech**: I suoni ed il parlato attraverso il TTS possono essere un mezzo utile per trasmettere le informazioni. Come pro c'è il fatto che un testo parlato può includere anche delle emozioni, così come i suoni. L'interazione inoltre necessita meno attenzioni, in quanto *eye-free*. Non sempre però si è in un contesto in cui è appropriato emettere dei suoni.
        - **Vibrazioni e Force Feedback**: le vibrazioni possono essere utilizzate come feedback per far capire all’utente che una certa azione è stata svolta.
        - **Altri** (Odori e Temperatura): il sistema può generare degli odori o cambiare temperatura per trasmettere delle informazioni.
- In che maniera si può ridurre l'utilizzo di batteria nei dispositivi IoT? Questo può causare dei problemi di usabilità?
    - L'utilizzo della batteria nei sistemi di IoT viene solitamente effettuato accendendo il dispositivo ad intermittenza, con una frequenza tale da trovare un compromesso tra la sincronizzazione del dispositivo e la durata della batteria. Proprio per questo potrebbe capitare che il dispositivo si possa trovare non sincronizzato con altre parti del sistema.
- Cosa si intende per IoT asincrono?
    - Visto che i dispositivi IoT devono comunicare in maniera asincrona con server attraverso Internet, ci sarà sicuramente della latenza. Questo può portare l'utente a sentirsi frustrato, visto che è abituato ad una breve attesa quando questo utilizza un computer o uno smartphone, ma quando usa gli oggetti reali si aspetta che l'interazione avvenga in maniera istantanea.
- I dispositivi IoT permettono di operare oggetti fisici da remoto o programmare un'azione futura, in che maniera si può migliorare l'usabilità per tali azioni?
    - L'astrazione della comunicazione con oggetti fisici da remoto, o la programmazione di tale azioni nel futuro deve essere accompagnata da un feedback che faccia capire all'utente che l'azione da lui desiderata è stata compiuta correttamente, visto che non si ha la possibilità di vedere fisicamente l'oggetto con cui si interagisce.
- Cosa si intende per interusabilità? (Interusability)
    - Per interusabilità si intende la facilità d'uso e il grado di integrazione di tutte le interfacce che costituiscono un sistema. Per migliorare l'interusabilità, è buona norma progettare tutte le varie parti in parallelo (dispositivo, applicazione mobile e web, telecomando fisico). Se Internet non funziona per qualche motivo, allora il sistema perde tutte, o parte, delle sue funzionalità, e questa riduce il grado di interusabilità del sistema stesso, e di conseguenza l'esperienza utente.
- Cosa si intende per Conceptual (o Mental) Model?
    - Il Conceptual Model è il modello che l'utente ha del sistema, che è più astratto del modello tecnico del sistema, ma permette all'utente di capire come questo funziona evitando i dettagli tecnici.
- Quali step sono inclusi all'interno dello stack di progettazione per i dispositivi IoT?
    - Le componenti dello stack di progettazione per dispositivi IoT sono le seguenti, partendo dalla più visibile all'utente finale, alla più tecnica e trasparente:
        1. *UI Design*: si incentra sulla progettazione dell'interfaccia, principalmente del layout, di ciò che riguarda l'estetica e delle sensazioni che l'interfaccia provoca;
        2. *Interaction Design*: analizza l'interazione che l'utente ha con il sistema, in tutte le sue parti;
        3. *Interusability*: (definito sopra);
        4. *Service Design*: si incentra di capire qual è il ciclo di vita del sistema, analizzando i futuri aggiornamenti, l'assistenza clienti, l'esperienza nello Store ecc.
        5. *Conceptual Model* (definito sopra);
        6. *Productisation*: analizza gli obiettivi che rendono speciale un tipo di prodotto, e i modi per dare più importanza al valore aggiunto dal sistema.
        7. *Platform Design*: si focalizza sul framework software che permette agli sviluppatori di far comunicare servizi esterni con il sistema, questo comprende SDK ed API.

## Beacons

- Cos'è la tecnologia BLE?
    - La tecnologia BLE - Bluetooth Low Energy è un protocollo che permette di trasferire dati fino a 90 metri di distanza utilizzando una bassa quantità di energia. Il protocollo utilizza le onde radio a frequenza 2.4 Ghz.
- Cosa cambia tra Bluetooth 4.0 e 5.0?
    - Il Bluetooth 5.0, introdotto nel 2016, quadruplica la portata della versione precedente e raddoppia la velocità di trasferimento (che a 50MiB/s non permette comunque di trasferire grandi quantità di dati, ma ricordiamo che è un protocollo per trasferimento dati a bassa energia).
- Cosa si intende per *BLE advertising*?
    - L'advertising è la fase in cui un *broadcaster* invia dei pacchetti che contengono delle informazioni circa la sua identità ai dispositivi nelle vicinanze. Gli *observer* possono ricevere questi pacchetti ed effettuare delle azioni di conseguenza, a seconda dell'identità del *broadcaster*.
- Cosa sono *broadcaster*, *advertiser*, *peripheral*, *observer* e *central*?
    - Un *Broadcaster* è un dispositivo che trasmette pacchetti tramite BLE per fornire informazioni riguardanti la presenza e l'identità ai dispositivi nelle vicinanze. Tale azione viene chiamata *advertising*, per questo ci si può riferire a tale ruolo anche come *advertiser*.
    - Un *peripheral* è in generale un dispositivo che si connette ad un dispositivo *central* tramite BLE.
    - L'*observer* è il dispositivo che ascolta i pacchetti che vengono inviati dal *Broadcaster*, e che agisce di conseguenza.
    - Il *Central* è un dispositivo in grado di connettersi al *Broadcaster* e di leggere e scrivere i dati. Questo dispositivo viene solitamente utilizzato per configurare il beacon.
- Quali sono i protocolli per dispositivi beacon?
    - iBeacon, per Apple. Un dispositivo iOS può ascoltare fino a 20 beacon simultaneamente. Quando il dispositivo riceve un segnale di un beacon vicino, il sistema operativo manda un segnale all’applicazione interessata, la quale può eseguire delle azioni.
    - Eddystone, sviluppato da Google, è supportato sia su Android che iOS.
- Quali sono i casi d'uso per i beacons?
    - I beacons vengono usati solitamente nel tracciamento della posizione *indoor*, oppure per svolgere azioni automaticamente quando si entra in una determinata regione. Così come possono essere utilizzati per contare le persone all'interno di una stanza (si assume che ogni persona abbia uno e un solo smartphone, non in modalità aereo).
- Cos'è il *ranging*?
    - Il ranging è una tecnica che permette di capire a che distanza di trova il dispositivo beacon dall'*observer*, in questo modo l'observer può effettuare delle azioni non solo in base alla presenza del beacon, ma anche dalla sua distanza.
- In che maniera i beacon possono essere utilizzati per la localizzazione da interno? A quanto ammonta l'errore di precisione?
    - Tramite il *ranging* e la triangolazione si può localizzare un dispositivo anche all'interno con un'errore nell'ordine dei metri. La triangolazione avviene posizionando tre beacon nella stessa regione, e calcolando il punto in cui le tre circonferenze (che hanno come raggio la distanza tra il beacon ed il dispositivo) si può trovare il punto in cui il dispositivo si trova.

## UWB

- Cos'è la tecnologia UWB?
    - La tecnologia Ultra Wide Band è una tecnologia di trasmissione dati alternativa al BLE, la quale opera su una frequenza più alta (500Mhz) e che utilizza comunque una bassa quantità di energia. Solitamente i dispositivi che utilizzano questa tecnologia sono più costosi.
- In cosa differisce la tecnologia UWB da quella usata nei beacon?
    - UWB permette di propagare il segnale ad una distanza maggiore, ed è molto più preciso per quanto riguarda il ranging, questo perchè viene calcolato con il ToF.
- Cosa si intende per Time of Flight nei dispositivi che utilizzano la tecnologia UWB?
    - Il Time of Flight è il tempo che il segnale impiega per raggiungere il dispositivo e per tornare indietro. Viene utilizzato per capire la distanza dal dispositivo *observer* al dispositivo UWB, con una precisione nell'ordine dei centimetri.

## Chatbots

- Cos'è un chatbot?
    - Un chatbot è un programma che interagisce con l'utente attraverso un'interfaccia testuale fatta a chat, in cui possono essere scambiati dei messaggi.
- Dove vengono usati i chatbot solitamente?
    - È comodo per l'utente avere dei chatbot che sono integrati all'interno di app di messaggistica, visto che l'utente scarica l'applicazione per parlare con amici e familiari, e poi ha come bonus l'opzione di parlare anche con dei bot. Solitamente questi chatbot sono più banali ed *hard-coded*. Altri chatbot possono essere usati all'interno di piattaforme di assistenza, in modo da ridurre il numero di operatori umani, oppure altri ancora possono avere la loro interfaccia web o mobile dedicata (GPT), nonchè poter essere usati attraverso delle API.
- Cosa cambia tra i chatbot sviluppati una volta e quelli di ora?
    - I chatbot più antichi non avevano nessun tipo di AI all'interno, e le risposte erano inserite in modo *hard-coded* ad una serie di possibili domande, con magari dei differenti parametri. Questo portava ad un'interazione meno naturale. Al giorno d'oggi, con l'avvento dei Large Language Model (LLMs) vengono usate tecniche avanzate di NLP e la conversazione è molto simile, a volte anche indistinguibile, con quella umana.
- Cos'hanno in comune i chatbot presenti nelle applicazioni di messaggistica?
    - Solitamente questi presentano un'interfaccia che è un mix tra un'interfaccia classica, con bottoni da premere, ed un'interfaccia a chatbot. Questo perchè solitamente questi bot mettono a disposizione dei comandi, che possono essere scritti o semplicemente cliccati.
- Pro e contro dei chatbot.
    - Come pro abbiamo il fatto che se il chatbot è moderno, l'interazione è spesso paragonabile a quella umana e quindi è uno strumento molto utile in diversi campi. Come contro c'è il fatto che, se il chatbot non è moderno, lo stato della conversazione non viene salvato, e quindi ad ogni nuova frase il chatbot non ricorda nulla di ciò che si è detto in precendenza. Questo non è più vero per i LLMs.
- In che maniera vanno gestiti gli errori nei chatbot?
    - Quando un chatbot non sa come rispondere ad una richiesta, dovrebbe chiarire nella maniera più comprensibile possibile cos'è che è andato storto, così l'utente può effettuare nuovamente la richiesta, o capire semplicemente che il bot non è in grado di soddisfare tale richiesta.
- Cos'è il Turing Test?
    - Il Turing Test è un test per classificare se una macchina ha un'interazione percepibile come umana o no. Il partecipante deve effettuare delle richieste, e a volte la risposta arriva da un umano, a volte da una macchina. Se il partecipante non riesce a distinguere quando la risposta è stata generata dalla macchina, allora questa passa il Turing Test.

## Voice User Interfaces

- Cos'è una VUI?
    - È un'estensione del chatbot al campo esclusivamente vocale. L'input quindi viene solitamente pronunciato dall'utente, il quale riceve una risposta sotto forma di voce dal dispositivo, in maniera da effettuare un dialogo con la macchina.
- Differenza tra Voice User Interface e Voice Command Device.
    - Il Voice Command Device è il dispositivo fisico su cui viene inserita la Voice User Interface, che è invece il software che permette la gestione del dialogo.
- Cosa si intende per *Barge-in* nel contesto delle VUI?
    - Per *Barge-In* si intende la possibilità di interrompere la VUI mentre sta parlando per chiarire qualcosa o per cambiare discorso. Questa è una funzionalità difficile da implementare.
- Quali sono i problemi delle VUI?
    - Le VUI presentano diversi problemi non semplici da risolvere, tra cui il fatto che non si possono ricevere delle lunghe frasi come risposte, a differenza di quello che può avvenire con i chatbot, altrimenti la risposta vocale durerebbe troppo; un'altra limitazione è la difficoltà di capire chi sta parlando tra una serie di interlocutori; la possibilità di effettuare *barge-in*, oppure il capire quali sono i comandi che sono accettati da una VUI, e quali sono quelli che porterebbero ad un errore. Un altro problema è il fatto che le VUI si basano sulla *recall* e non sulla *recognition*, nel senso che i comandi vanno ricordati, e non possono essere scelti da una lista di comandi disponibili. Un altro problema ancora è che l'attesa tra la richiesta e la risposta dovrebbe essere breve, altrimenti l'utente potrebbe pensare che la VUI non abbia compreso quello che si è detto, e quindi potrebbe ripetere la frase, il che porterebbe ad un'ulteriore confusione.
- Quali sono i tipi di interazioni che un utente può avere con una VUI?
    - Esistono tre tipi di interazioni:
        - *Command and Control*, interazione *one-way* in cui l'utente utilizza la voce per dare dei comandi al sistema. L'output del sistema però è un output tradizionale. Un esempio potrebbe essere un qualche tipo di di dispositivo controllabile tramite la voce.
        - L'interazione *one-way* opposta, in cui l'utente comunica con la macchina nella maniera tradizionale, ma la macchina risponde tramite output vocale.
        - *Spoken Dialogue System*m, interazione *two-way* più interessante, in cui avviene un dialogo tra l'uomo e la macchina.
- Qual è la tradizionale pipeline per la gestione di un dialogo tra uomo e VUI?
    - In una VUI, la pipeline è la seguente:
        1. Riconoscere che l’utente sta interpellando l’assistente vocale;
        2. Capire chi, tra una serie di utenti, sta facendo la richiesta;
        3. Riconoscere cosa l’utente sta dicendo attraverso un sistema di Automatic Speech Recognition;
        4. Interpretare la richiesta dell’utente tramite un sistema di Natural Language Understanding;
        5. Seleziona l’azione ottimale a seconda dell’intento dell’utente, considerando eventualmente anche il contesto attuale;
        6. Generare una risposta in linguaggio naturale;
        7. Trasformare la risposta da testo al parlato tramite un sistema di Text to Speech.
- Quali sono le competenze necessarie per progettare una buona VUI?
    - Per progettare un buona VUI sono necessarie competenze informatiche, linguistiche e psicologiche.
- Cosa sono i *power users* e cosa bisogna cambiare nella VUI per permettere una migliore usabilità per questo tipo di utenti?
    - I *power users* sono quella nicchia di utenti che utilizzano molto spesso il sistema in maniera agile, e quindi per loro si dovrebbero inserire delle scorciatoie che permettono di eseguire un task in maniera più veloce. Un esempio è la possibilità di inserire tutti i parametri di una richiesta in una sola frase, invece di risolvere un parametro per volta attraverso un dialogo.

## Haptic Interaction

- Cosa si intende per feedback tattile?
    - Il feedback tattile è quel tipo di feedback che coinvolge il senso del tatto. Può essere trasmetto in differenti modi, come vibrazione, abrasione, allungamento della pelle o tramite piccole scariche elettriche.
- Su quali capacità umane si basa il feedback tattile?
    - L'interazione tattile si basa su diverse capacità umane, tra cui:
        - Percezione tattile, ovvero l'abilità di percepire il contatto ed altre sensazioni sulla pelle;
        - Senso cinestetico (Kinesthetic Sense): l’abilità di capire dove solo le parti del corpo senza effettivamente guardarle.
        - Percezione cinestetica (Kinesthetic Perception): dipende dal senso cinestetico, ed è l’abilità di capire dove sono le parti del corpo anche senza il senso tattile (si pensi quando vengono usati degli anestetici).
        - Percezione tattile passiva (Passive Haptic Perception): la capacità di capire il posizionamento del corpo dalle informazioni tattili. Passivo perchè le informazioni vengono dal mondo esterno e il cervello le elabora soltanto.
        - Copia dell’Efferenza (Efference Copy): consiste nella predizione del movimento e delle azioni da questo causate. Questo è utile perchè l’effettivo movimento può essere aggiustato a seconda della predizione.
- Quali sono le differenze tra la percezione visiva e quella tattile?
    - La percezione visiva è più veloce di quella tattile, però il loop tattile ha una frequenza maggiore del loop visivo con 1000Hz per il primo, e 60Hz per il secondo, nel senso che una persona può percepire molte più sensazioni differenti, o oggetti differenti con il tatto rispetto a immagini differenti in un secondo con la vista. La vista spesso è più affidabile, tranne che in alcuni particolari casi, come per il riconoscimento di *texture*, le quali sono impossibili da riconoscere con la vista, se non tramite l'associazione tra estetica e il ricordo del contatto con una cosa simile, il quale però può ingannare.
- Quali sono le limitazioni dell'interazione tattile?
    - Quando si progetta un'interazione tattile, bisogna tener conto di una serie di fattori, che potrebbero limitare l'esperienza utente:
        - Risoluzione spaziale, ovvero la distanza minima per cui due punti vengano percepiti come uno solo;
        - Risoluzione temporale, il tempo di attesa affinchè due feedback tattili vengano distinti, solitamente va tra i 2 e i 40ms;
        - Effetto del punto fantasma, in cui se due stimoli sono ampiamente distanziati, un ulteriore stimolo fittizio potrebbe essere percepito. Ad esempio se due punti vengono percepiti da tutte e due le mani, si potrebbe percepire anche un punto nel mezzo. (?)
        - L'incapacità di concentrarsi sull'interazione quando ci sono un eccesso di informazioni.
- Simboli rialzati o incisi, quali sono i migliori da riconoscere con il tatto? C'è qualche altra *good practice* di questo tipo?
    - I simboli rialzati vengono percepiti meglio di quelli incisi. Altre pratiche sono %%TODO: continua%%
- Cosa si intende per Degree of Freedom?
    - Per Degree of Freedom di un dispositivo si intende il numero di assi su cui il dispositivo si può muovere. Ad esempio un volante ha 1 DoF, perchè si pùo muovere solamente a destra e sinistra. Una cloche di un aereo che può quindi andare anche avanti e indietro avrebbe 2 DoF. Una penna con sensibilità alla pressione avrebbe 3 DoF. Esistono anche dispositivi con 6 DOF (più dei 3 assi spaziali), visto che questi possono essere mossi nel mondo tridimensionale, ma si può arrivare in un punto mediante strade differenti. Questo è possibile perchè ci sono due parti che entrambe hanno 3 DOF (two rotating arms). In generale, più DOF significa più facilità nel muovere l’oggetto.
- Cosa si intende per Haptic Rendering?
    - Per Haptic Rendering si intende l’effettuare una forza opposta quando l’oggetto virtuale viene toccato, in maniera da dare l’illusione della solidità.

## Tangible Interaction

- Cosa si intende per interazione tangibile?
    - Per interazione tangibile si intende quel tipo di interazione in cui è possibile dare un input al sistema muovendo degli oggetti reali. Differisce da quella tattile proprio in quest'ultima cosa.
- Fai qualche esempio di interazioni tangibili che si possono usare quotidianamente.
    - Prendere in mano il telefono da una superficie per attivare lo schermo;
    - Bussare sullo schermo per fare uno screenshot;
    - Mettere il telefono a faccia in giù su una superficie per attivare la modalità “non disturbare”.
- Ricordi la *Marble Answering Machine*?
    - La *Marble Answering Machine* è stato un prototipo di segreteria telefonica tangibile, in cui i messaggi erano modellati da delle biglie, e che quindi potevano essere sentire semplicemente ponendo la biglia relativa sulla macchina.
- Cosa si intende per *Graspable Interfaces*?
    - Le *Graspable Interfaces* sono interfacce che permettono di interagire con oggetti fisici che vengono posti sopra lo schermo, in modo da interagire con le forme digitali che vengono visualizzate sullo schermo.
- Cosa si intende per *affordance*? Qual è la differenza tra *affordance* reale e percepita?
    - Si definisce come affordance le proprietà di un oggetto che suggerisce come questo può essere usato. Ad esempio un pomello suggerisce che questo può essere girato, un bottone di essere premuto ecc. Gli oggetti tangibili possiedono un’affordance reale, quelli virtuali un’affordance percepita.
- Differenza tra VR e AR.
    - Per realtà virtuale si intende un'interfaccia in cui l'utente è completamente immerso. Per realtà aumentata si intende un sistema che aggiunge degli elementi virtuali al mondo reale, con cui l'utente può interagire.
- Quali sono le categorie delle TUI?
    - Superfici Interattive, come *tangible bits*.
    - Assemblamento Costruttivo, come *sandscape*
    - Token + Vincoli, come la *Marble Answering Machine*
- Quali sono le limitazioni delle TUI?
    - Le TUI possiedono molteplici limitazioni. Una delle più importanti è che una volta effettuata un'azione, non c'è nessun modo di ripristinare lo stato precedente, se non ricordandolo. Non può quindi essere presente nessuna funzione di undo. Le TUI richiedono spesso molto spazio, non sono generalizzabili visto che sono progettate per uno scopo ben preciso, e non esiste il concetto di macro per automatizzare una serie di azioni svolta frequentemente.
- Cos'è il *Model-Control-Representation* nelle TUI?
    - Il MCR è un modello di sistema che viene utilizzato nelle TUI. Il modello del sistema è rappresentato dai dati digitali, il controllo avviene con gli oggetti reali, i quali rappresentano inoltre lo stato del sistema (totale o parziale) anche quando questo viene spento.
- Quali sono le tecnologie principali per lo sviluppo di TUI? Elenca anche i pro ed i contro di ognuna.
    - Le tecnologie principali per lo sviluppo di TUI sono:
        - RFID, per l’identificazione di oggetti sulla superfice. Gli RFID sono comodi perchè non richiedono una batteria.
    - Computer Vision, permettono non solo di capire se un oggetto è presente o meno, o di identificare tale oggetto, ma anche di capire la sua forma, il colore, la posizione esatta, la forma e l’orientamento.
    - Microcontrollori, sensori ed attuatori.

## Gestural Interaction

- Cosa si intende per interazione gestuale?
    - Per interazione gestuale si intende quel tipo di interazione con il sistema attraverso movimenti con il corpo
- Cosa cambia tra *touch gestures* e *touchless gestures*?
    - Touch Gestures: effettuate su una superfice touch, permettono di interagire in maniera più intuitiva con il sistema. Un esempio di queste interazioni sono lo ***swipe*** o il ***pinch***.
    - Touchless Gestures: vengono effettuate nello spazio tridimensionale, senza toccare nessun dispositivo. Vengono principalmente usate in VR e AR.
- Fai degli esempi di interazioni gestuali.
    - Un esempio di interazioni gestuali *touch* sono lo *swipe* o il *pinch*, mentre per quanto riguarda le interazioni *touchless* un esempio può essere il muovere la mano davanti al sistema in una direzione per cambiare una canzone, e nell'altra per tornare indietro.
- Quali sono i limiti dell'interazione gestuale, e in che modo alcuni di questi possono essere risolti?
    - A parte il fatto che a volte possono essere poco affidabili, in alcuni casi non è adeguato effettuare dei gesti. Inoltre, seppur l'interazione gestuale richiede meno attenzione rispetto ad altri tipi di interazione, spesso dopo un gesto si ha la necessità di guardare lo stato del sistema per vedere se effettivamente il gesto è stato compreso, e l'azione svolta, cosa che comunque richiede dell'attenzione.
- Cosa cambia tra interazione gestuale consapevole e non consapevole?
    - Quando l'utente è consapevole che i suoi gesti sono presi in input da un sistema, si comporterà in maniera diversa, e cercherà di rendere i gesti il più chiaro possibile. D'altra parte, se non ne è consapevole, i suoi gesti saranno molto più naturali.
- Cosa si intende per *Gorilla Arm*?
    - Per *gorilla arm* si intende quel fenomeno in cui l'interagire per un lungo periodo tramite un'interfaccia gestuale può portare a stanchezza.
- Quali sono le limitazioni della realtà virtuale?
    - Per quanto riguarda la realtà virtuale, questa presenta vari problemi. Uno di dato dal fatto che lo spazio virtuale è molto più grande dello spazio reale in cui la persone è immersa, quindi non si può liberamente camminare nello spazio reale, ma bisogna teletrasportarsi utilizzando appositi comandi nello spazio virtuale, il che rende l’esperienza meno realistica.
- Cosa si intende per *Interaction Fidelity* (o Fedeltà dell'interazione)?
    - Per fedeltà di interazione si intende il grado con cui le azioni all’interno della UI corrispondono a quelle effettuate nel mondo reale. Ad esempio quanto devo muovere il braccio per effettuare uno spostamento nel mondo virtuale. Maggiore la fedeltà, più realistica l’interazione.
- Cosa si intende per *Hypernatural Movements* (o Movimenti Ipernaturali) nel contesto della realtà virtuale?
    - Si intende la possibilità di fare movimenti nel mondo virtuale che non sarebbero possibili nel mondo reale. Questo non intacca la fedeltà visto che l’utente è consapevole di star facendo movimenti possibili sono nel mondo virtuale.

## Zooming Interfaces

- Cos'è una zooming interface?
    - Una zooming UI è un’interfaccia che si presenta come una tela infinita, con risoluzione infinita, in cui l’utente può fare “zoom out” per vedere la situazione generale, e poi fare “zoom in” per vedere sempre più dettagli.
- Quali movimenti possono essere effettuati all'interno di una ZUI?
    - Zoom in per vedere più dettagli;
    - Zoom out per vedere meno dettagli, e meglio il quadro generale;
    - Muoversi liberamente nella tela.
- Quando una ZUI è meglio di una UI tradizionale?
    - Quando si ha a che fare con molti contenuti e differenti schermate, la cui navigazione potrebbe altrimenti portare ad una confusione, paragonabile al trovarsi in un labirinto.
- Fai qualche esempio di ZUI.
    - Esempi di ZUI sono google maps, figma ed excalidraw.

## HCI in the car

- Cosa si intende per HCI nell'automobile?
    - Per HCI nell'automobile si intende la progettazione di interfacce che permettano al guidatore di interagire con i sistemi smart all'interno dell'auto con la minima distrazione possibile.
- Fai qualche esempio di sistemi che utilizzano HCI nell'automobile.
    - Esempi possono essere Android Auto o Apple Car Play, che permettono di interagire con il cellulare direttamente nel sistema dell'auto, in modo da avere meno distrazioni. Altri possono essere completamente trasparenti all'utente, come l'ABS e il controllo della stabilità. Un altro esempio ancora è il *cruise control*.
- Di che tipo possono essere le distrazioni alla guida?
    - Sono possibili due tipi di distrazioni, quelle visuali, in cui la persona sta guardando da un'altra parte; e quelle cognitive, in cui la persona sta pensando a qualche altra cosa, e quindi non sarebbe in grado di reagire velocemente ad un evento improvviso.
- Quali sono i tipi di interazione che si possono usare alla guida? Elenca anche i loro pro ed i loro contro.
    - In generale alla guida si preferiscono interazioni il più possibile *eye-free* e magari anche *hand-free*. I pulsanti fisici possono essere una buona idea, soprattutto se posti sul volante, visto che possono essere percepiti tramite il tatto e quindi premuti senza guardare. I comandi vocali e le gestures anche possono essere buone idea, anche se possono non essere completamente affidabili e a volta non è appropriato parlare ad alta voce o fare dei gesti.
- In che modo si può inserire un comando per terminare facilmente una funzionalità critica all'interno dell'automobile?
    - Si dovrebbe inserire un comando che si può azionare istintivamente. Ad esempio il *cruise control* può essere disattivato sia premendo il bottone fisico sul volante, che premendo il pedale del freno.

## Context Aware Interaction

- Cosa si intende per *Context Aware Interaction*?
    - Un sistema si dice *context aware* se è in grado di capire in che contesto si trova l'utente, ed effettuare delle azioni in maniera automatica di conseguenza.
- Fai qualche esempio di sistema che utilizza una *Context Aware Interaction*
    - Gli smartwatch che rilevano in automatico quando si fa attività fisica o si dorme possono essere un esempio, ma anche solamente un dispositivo che cambia da tema scuro a chiaro a seconda dell'ora del giorno, o della luminosità dell'ambiente circostante. La modalità auto di parecchie applicazioni musicali anche è un tipo di sistema *context aware*.
- Cosa si intende per *Awareness Mismatch*?
    - È quel fenomeno in cui il contesto percepito dalla persona non è allineato con il contesto percepito dal sistema. Ad per un sistema che accende la luce quando si verifica un movimento, il contesto è "c'è stato un movimento", mentre la persona potrebbe pensare che il contesto è "sono nella stanza". Questo porta ad una peggiore usabilità, visto che la luce si spegnerà se non percepirà nessun movimento, anche se la persona è ancora all'interno della stanza.

- **Cos’è l’algoritmo di Viola-Jones?**
    
    L’algoritmo Viola-Jones è un algoritmo in grado di localizzare facce all’interno di una certa immagine.
    
    L’algoritmo utilizza delle haar features (che sono classificatori deboli), ovvero delle features rettangolari.
    
    Esistono 3 tipi di haar features:
    
    - Formata da due rettangoli, verticali o orizzontali, uno nero ed uno bianco;
    - Formata da 3 rettangoli, estremi di un colore e centro di un altro;
    - Formata da 4 rettangoli, la cui diagonale è di un colore e l’altra di un altro.
    
    Ogni feature viene applicata in una parte dell’immagine, ripetendo il processo molteplici volta, cambiando la grandezza e la posizione del rettangolo. Il valore ritornato da ognuna di queste operazioni è la differenza tra la somam di pixels nella zona bianca e la somma di quelli nella zona nera.
    
    L’idea è quella di catturare caratteristiche uniche di una faccia, come il naso, la bocca ecc.
    
    Viene stabilita una threshold per questo valore in modo da poter restituire un risultato binario (si/no) in base alla presenza di questo tipo di pattern nell’immagine originale.
    
    Visto che all’interno di un’immagine il numero di possibili haar features è enorme, il calcolo delle varie somme sarebbe troppo costoso a livello computazionale, per questo vengono utilizzare le immagini integrali (Integral images) come ottimizzazione.
    
    Il classificatore finale, che permetterà di capire se è presente o meno una faccia all’interno di un’immagine, viene costruito mediante la tecnica AdaBoost. I classificatori deboli in questo caso sono le haar features, e tramite questa tenica è possible capire quali sono le haar features più discriminative al fine di trovare una faccia.
    
    Una volta allenato il classificatore, si ha un insieme di classificatori deboli, ovvero haar features, le quali vengono messe in una cascata, ordinate dalla meno discriminativa alla più discriminativa. Se uno di questi classificatori deboli ritorna un output negativo, allora l’immagine viene scartata. Una faccia è presente solo se l’immagine ritorna un ouput positivo per ogni classificatore.
    
    L’allenamento, ovvero la costruzione del classificatore finale, può impiegare molto tempo, visto che vengono applicate tutte le possibili haar features. Una volta che il classificatore è allenato, e quindi le features migliori sono selezionate, questo è molto rapido nel localizzare facce all’interno di una foto.
- **Perché è meglio un basso False Acceptance Rate invece di un basso False Rejection Rate?**
    
    Un basso FAR indica una piccola probabilità che un individuo non autorizzato (impostore) venga erroneamente autenticato dal sistema, e questo è un problema sopratutto nelle applicazioni in cui la sicurezza è decisiva.
    
    Un alto FRR invece può essere fastidioso in quanto un individuo autorizzato potrebbe essere visto come non autorizzato e quindi dovrebbe ripetere l’autenticazione.
- **Quali sono le regole per un buon training?**
    
    Il training set, così come tutto il dataset, dovrebbe includere modelli di diverse qualità e dovrebbe considerare le variazioni PIE.
    
    Dovrebbe inoltre avere vari campioni positivi, ad esempio volti in caso di face recognition, e campioni negativi, ovvero qualcosa che sembra un volto ma che non lo è. Questi dovrebbero essere in pari quantità, in quanto aiutano il modello a capire come non essere ingannato.
- **Differenza tra tratti biometrici deboli e forti (strong and soft)**
    
    I tratti biometrici forti sono da soli sufficienti a distinguere un individuo da un altro in maniera accurata.
    
    I tratti biometrici deboli invece non lo sono, in quanto possono mancare di alcuni requisiti come l’unicità. Un esempio di un tratto biometrico debole è il colore degli occhi o dei capelli.
    
    I due tipi di tratti possono comunque essere combinati insieme in maniera da avere un sistema più robusto, in quanto un impostore dovrebbe cercare di imitare più tratti per ingannare il sistema.
- **Cos’è l’Equal Error Rate?**
    
    L’equal error rate è il valore del rapporto di errore nel punto di intersezione tra la curva di False Acceptance Rate e quella di False Rejection Rate, dove entrambi i valori sono circa uguali. 
    
    È utile in quanto modella il punto di equilibrio in cui i due tipi di errori sono uguali. Indica quindi l’errore minimo che il sistema avrà da un lato o dall’altro. Più tale errore è basso, migliori le performance generali del sistema.
- **Differenza tra Verifica ed Identificazione, cosa sono la Re-identification e la Continuous Identification?**
    
    La procedura di verifica prende in input un probe ed un claim, il probe è la rappresentazione del tratto biometrico, come ad esempio l’immagine della faccia, ed il claim è la dichiarazione di identità da parte dell’individuo. La comparazione tra probe e template nella gallery è 1 ad uno, significa che il probe viene comparato con i template associati all’identità dichiarata e viene ritornato un risultato binario.
    Da notare che a volte il claim può essere implicito, come ad esempio nel riconoscimento dello smartphone.
    
    La procedura di identificazione è diversa, in quanto viene preso in input un probe e viene resituito in output l’identità associata al probe. In questo caso la comparaizone è 1 ad N, ovvero il probe viene comparato con tutti i templates di tutti gli individui nella galleria e viene restituito l’identità associata al template con somiglianza maggiore al probe.
    
    In caso di identificazione open-set può anche essere restituito il valore nullo in caso l’individuo non è presente nella galleria.
    
    Re-identificazione è quel processo in cui una persona non viene identificata, però il sistema è in grado di capire se la persona appare più volte in diversi probe.
    
    L’identificazione continua è semplicemente la re-identificazione che restituisce però anche l’identità associata all’individuo.
- **Come si misura la False Acceptance nella Verifica, e il False Rejection Rate? Cosa si intende invece per Genuine Rejection Rate e Genuine Acceptance Rate?**
    
    Una False Acceptance, nella verifica, accade quando un individuo impostore, che quindi dichiara un’identità non veritiera, viene accetato nel sistema.
    Il False Acceptance Rate è semplicemente il rapporto tra numero di False Acceptance su numero totale di tentativi impostori.
    
    Una False Rejection accade quando un individuo genuino, che quindi dichiara un’identità veritiera, viene rifiutato dal sistema.
    Il False Rejection Rate è il rapporto tra numero di False Rejection su numero totale di tentativi genuini.
    
    Da notare che entrambi i rapporti sono in funzione della threshold.
    
    L’inverso di tali rapporti sono il Genuine Rejection Rate e il Genuine Acceptance Rate.
    
    Le formule sono quindi le seguenti:
    
     
    
    ```
    FAR(t) = FA/TI
    FRR(t) = FR/TG
    GAR(t) = GA/TG
    GRR(t)= GR/TI
    ```
- **I valori assoluti dei False Negatives e False Positives non sono abbastanza per una giusta valutazione del sistema, perchè?**
    
    Non bastano in quanto bisogna misurare i rapporti che tali numeri influenzano, come il FRR, FAR, GRR e GAR. Anche questi potrebbero non bastare, in quanto bisogna misurare la qualità e generalizzabilità del dataset su cui viene fatta l’evaluation, così come la reliability del sistema.
- **Cos’è la curva ROC?**
    
    La curva ROC, acronimo di Receiving Operating Characteristic, è una curva che permette di tracciare un comportamento generale del sistema, ed è utile per confrontare le performance di diversi sistemi.
    
    La ROC rappresenta la probabilità di un Genuine Acceptance Rate (espresso come 1 - FRR) in funzione del numero di False Acceptance Rate. Più alta è la curva verso la metà sinistra, maggiore è il sistema.
    
    Si può prendere l’area sotto la curva, denominata come AUC, come valore unico per il confronto. maggiore il valore, migliore il sistema.
- **Performance evaluation per identificazione open set**
    
    Un buon modo per effettuare la performance evaluation è l’all-against-all. Tramite questa tecnica si calcola una matrice delle distanze i cui tutti i template vengono comparati tra di loro e viene inserita tale distanza nella matrice.
    
    In caso dell’all-against-all la divisione tra probes e gallery non viene fatta a priori. 
    
    In caso di identificazione open-set, ogni template viene comparato ad ogni altro template. Un template prende il ruolo di probe e gli altri prendono il ruolo di gallery. A seconda del risultato dell’operazione di comparazione, vengono calcolati i vari rate e il DIR al rango k.
    
    Questa procedura viene ripetuta per vari livelli di thresholds.
    
    **In particolare, possiamo scrivere l’algoritmo in pseudocodice (usando la similarità):**
    
    ```
    for each threshold t:
    	for each row i:
    		best_match <- identità con il miglior match
    		best_simil <- similarità con il miglior match
    		if (best_simil >= t):
    			DI(t, 1)++
    			for each column j:
    				se esiste una similarità >= t con label(i) != label(j):
    					FA++
    				else:
    					se esiste una posizione k in cui similarità >= t con label(i) == label(j):
    						DI(t, k)++
    		else:
    			GR++
    DIR(t,1) = DI/TG
    FRR(t) = 1 - DIR(t,1)
    FAR(t) = FA/TI
    GRR(t) = GR/TI
    while DI(t,k) != 0:
    	DIR(t,k) = DI(t,k)/TG + DIR(t, k-1)
    ```
    
    È possibile calcolare:
    
    - Il numero di operazioni per riga: $2$, in quanto si analizza il primo match genuino ed il primo impostore;
    - Numero di operazioni genuine per riga: $1$
    - Numero di operazioni impostori per riga: $1$
    - Numero totale di tentativi genuini: $|G|$
    - Numero totale di tentativi impostori: $|G|$
- **Performance evaluation per identificazione closed set**
    
    L’all-against-all in caso di identificazione closed set è più semplice perchè non è presente la threshold, ma visto che si ha la certezza che i probe appartengono sicuramente ad un’identità in galleria, l’identità restituita è la quella relativa alla prima posizione nel vettore delle somiglianze.
    
    In questo caso vengono calcolate le misure CMS (Cumulative match score) al rango k, dove CMR(k) rappresenta la probabilità di una corretta identificazione al rango k, ovvero la probabilità di trovare l’identità corretta nei primi k valori di similitudine nel vettore di somiglianza.
    
    In particolare, possiamo scrivere l’algoritmo in pseudocodice:
    
    ```
    for each row i
    	{L[i,m] | m = 1,...,|G|-1} = {M[i,j] | j = 1,...,|G|} - M[i,i] ordered by increasing value
    	find the first L[i,k] such that label(i) != label(L[i,k])
    	CMS(k) ++
    	CMS(1) = CMS(1) / TA
    	RR = CMS(1)
    	
    	k = 2
    	while k < |G| -1:
    		CMS(k) = CMS(k)/TA + CMS(k-1)
    ```
    
    È possibile calcolare:
    
    - Numero di operazioni per riga: $1$, in quanto viene considerato solo il best match;
    - Numero di tentativi genuini per riga: $1$
    - Numero di tentativi impostori per riga: $0$, in quanto non esistono impostori in un sistema open-set;
    - Numero di tentativi genuini totali: $|G|$
- **Performance evaluation per la verifica**
    
    Anche nella verifica possiamo utilizzare l’all-against-all, e dobbiamo distinguere due casi: la verifica single template, ovvero che considera tutti i template; e la verifica multiple template, in cui nella comparazione tra due identità viene considerato solamente il template che ha il best match.
    
    **Vediamo innanzitutto l’algoritmo per la verifica single-template:**
    
    Il probe viene confrontato con tutti gli altri template, e quindi ci saranno molti più tentativi impostori che genuini. In caso la somiglianza è maggiore della threshold e l’identità è la stessa, allora si ha una GA, altrimenti una FA. In cso invece la threshold sia minore, se l’identità è la stessa si ha una FR, altrimenti una GR.
    
    **In particolare, possiamo scrivere l’algoritmo in pseudocodice (si usano sempre le somiglianze):**
    
    ```
    for each threshold t:
    	for each cell M[i,j] with i != j:
    		if M[i,j] >= t:
    			if label(i) == label(j):
    				GA++
    			else:
    				FA++
    		else:
    			if label(i) == label(j):
    				FR++
    			else:
    				GR++
    GAR(t) = GA/TG
    GRR(t) = GR/TI
    FAR(t) = FA/TI
    FRR(t) = FR/TG
    ```
    
    È possibile calcolare:
    
    - Numero di operazioni per riga: $|G|-1$
    - Numero di tentativi genuini per riga: $S-1$, visto che consideriamo i template corrispondenti all’identità del probe, tranne il probe stesso;
    - Numero di tentativi impostori per riga: $S(N-1)$, visto che consideriamo i template delle altre $N-1$ identità, moltiplicati per il numero di template.
    - Numero totale di tentativi genuini: $|G|(S-1)$;
    - Numero totale di tentativi impostori: $|G|(N-1)S$.
    
    **Per quanto riguarda l’algoritmo di verifica multiple-template:**
    
    L’unica differenza rispetto alla verifica single template è che non compariamo più il probe con ogni altro singolo template, ma con gruppi di template della stessa identità. Prendiamo poi come somiglianza la somigliana maggiore tra i template della stessa identità. Il procedimento per il resto è uguale alla verifica single-template.
    
    In particolare, possiamo scrivere l’algoritmo in pseudocodice:
    
    ```
    for each threshold t
    	for each row i
    		for each group M_label of cells M[i,j] with same label(j) excluding M[i,i]
    			diff = min(M_label)
    			if diff <= t then
    				if label(i) = label(M_label) then GA++
    				else FA++
    			else if label(i) = label(M_label) then FR++
    			else GR++
    	GAR(t) = GA/TG
    	FAR(t) = FA/TI
    	FRR(t) = FR/TG
    	GRR(t) = GR/TI
    ```
    
    È possibile calcolare:
    
    - Numero di operazioni per riga: $N$, in quanto il probe viene comparato con identità;
    - Numero di tentativi genuini per riga: $1$, in quanto è solo una l’identità genuina;
    - Numero di tentativi impostori per riga: $N-1$;
    - Numero totale di tentativi genuini: $|G|$
    - Numero totale di tentativi impostori: $|G|(N-1)$
- **L’identificazione open set è più difficile della verifica?**
    
    È più difficile perchè la comprazione è 1 ad N, inoltre va soddisfatta la threshold e va ritornata l’identità corretta e non solo un valore binario.
- **Quali sono i differenti livelli di fingerprint recognition?**
    
    Ogni livello di features è utile per dividere l’insieme di impronte in categorie sempre più specifiche. 
    
    La tassonomia è stata definita dallo studioso inglese da Sir Francis Golton.
    
    Al primo livello troviamo le macro-singularities, che si basano sul numero di delta, ovvero il punto nell’impronta in cui le creste irradiano verso l’esterno in tre diverse direzioni.
    
    - Un pattern “loop” è presente se è presente un solo delta
    - Un pattern a spirale è presente se ci sono due delta;
    - Un pattern ad arco è presente se non ci sono delta.
    
    Al secondo livello troviamo le minutiae, anche chiamate micro-sigolarità o Galton features. Sono quel punto nell’impronta in è presente un bivio o l’interruzione di una linea dell’impronta (cresta). 
    Le minutiae sono essenziali in quanto permettono di comparare più in dettaglio le impronte, a seconda della loro distanza relativa e la loro frequenza.
    
    Al terzo livello troviamo il pattern dei pori della pelle. Questo può essere acquisito solo mediante un sensore ad altissima qualità.
- **Cos'è il Rubber Sheet Model?**
    
    Il Rubber Sheet Model è una tecnica di normalizzazione utilizzata nella pipeline di preprocessing nell’iris recognition. Lo scopo è quello di ottenere dei dati normalizzati che descrivano l’iride e che possano permettere l’estrazione delle feature e la successiva comparazione tra differenti iridi.
    
    L’idea è quella di prendere un numero fisso di punti su ogni raggio che è contenuto nella regione tra il confine della pupilla e il confine dell’iride. Ognuno di questi punti viene trasformato in coordinate polari, dove il centro di tali coordinate è il centro della pupilla.
    
    Questa operazione permette di generare un’immagine rettangolare su cui sarà possibile poi estrarre il feature vector per comparare diversi iridi.
- **Cos’è il Borda count e a cosa serve?**
    
    Il Borda count è un metodo per effettuare la fusione a livello di score. Viene utilizzata in caso vi siano più classificatori, e ognuno di questi ritorna una lista ordinata dei migliori classificati. Il Borda count prevede che ad ogni posizione nella lista venga assegnato un punteggio. I punti relativi ad ogni classe vengono sommati e come risultato viene scelta la classe con il punteggio più alto.
- **Cos’è lo spoofing e quali sono le strategie per prevenirlo?**
    
    Per spoofing si intende un tipo di attacco in cui la persona cerca di imitare un certo tratto biometrico di un altro individuo in modo da ingannare il sistema per avere l’accesso. È diverso del camuffaggio, in cui lo scopo dell’individuo è quello di non farsi riconoscere dal sistema.
    
    Lo spoofing può essere effettuato in varie maniere, ad esempio mostrando una foto o un video della faccia di un altro individuo, oppure mediante metodi sofisticate come maschere o pellicole applicate sul dito per imitare un’altra impronta digitale.
    
    Tra le strategie principali di anti-spoofing abbiamo:
    
    - Interazione con l’utente: il modo più semplice, si chiede all’utente di effetuare un’azione casuale e non prevedibile, in modo che questo non possa utilizzare una foto o un video pre-registrato.
    - Informazioni di profondità: si cerca di estimare l’informazione 3D dall’immagine 2D, in modo che l’utente non possa usare nessun tipo di immagine bidimensionale per ingannare il sistema.
    - Eveybling detection: si calcola il tempo di battitura degli occhi, che per un individuo varia dai 2 ai 4 secondi, e dura per 250 millisecondi.
    - Micro texture analysis: utilizzata principalmente per evitare attacchi con maschere facciali, si analizza il riflesso che il materiale ha sul sensore, in quanto la pelle ha un riflesso ben diverso da altri materiali sintetici.
    - Analisi del moirè pattern aliasing: Uno schermo proiettato su un altro schermo crea il moirè pattern, e quindi è facilmente identificabile come spoofing.
    - Gaze stability: analizza la coordinazione tra il movimento della testa, della mano e degli occhi quando una certa azione è richiesta dal sistema per capire se si tratta di un attacco di spoofing o meno.
- **Come si possono valutare le performance di anti-spoofing in un sistema?**
    
    Una misura per valutare l’abilità del sistema di contrattaccare lo spoofing è lo SFAR, ovver Spoofing False Acceptance Rate, che modella il numero di attaccanti che sono autorizzati dal sistema.
    
    Ci sono anche due altre misure, che sono:
    
    - False Living Rate: percentuali di attacchi di spoofing erroneamente classificati come reali;
    - False Fake Rate: percentuale di accessi reali erroneamente classificati come spoofing.
    
    È possibile fondere la fase di riconscimento con la fase di anti-spoofing in maniera tale che il risultato finale sia la combinazione dei due risultati, in modo da avere un sistema più robusto.
- **Perchè l’iride è particolarmente unico?**
    
    Pechè l’iride è un tratto altamente randotipico, ovvero non è affetto dall’eredità famigliare. L’iride destro è diverso da quello sinistro, e anche due gemelli identici hanno iridi differenti.
- **Cosa sono le impronte latenti? (Latent fingerprints)**
    
    Le impronte latenti sono le impronte che vengono lasciate su qualsiasi superficie dopo il contatto. Queste possono essere raccolte in un secondo momento tramite tecniche apposite senza che l’indivduo ne sia a conoscenza.
    
    Il problema di tali impronte è che possono essere di bassa qualità e non complete, tale problema può essere risolto tramite l’allineamento.
- **Cos’è un sistema multibiometrico?**
    
    Un sistema multibiometrico è un approccio per aumentare la robustezza di un sistema biometrico, combinando più di un approccio per ricavare un risultato in un solo risultato finale.
    
    Questo aumenta la robustezza in quanto evita gli errori e rende il lavoro di un utente malitenzionato più difficile in quanto deve ingannare più sottosistemi per essere autenticato.
    
    Esistono vari tipi di sistemi multibiometrici:
    
    - Approccio multimodale puro: combinare il risultato di più tratti biometrici in uno solo.
    - Istanze multiple: il sistema richiede multiple istanze dello stesso tratto biometrico, ma preso da una fonte differente. Questo è possibile con alcuni tipi di riconoscimento, come impronta e iride, in quanto un individuo ne possiede più di uno, ma non con altri ad esempio risconoscimento facciale.
    - Istanze ripetute: il sistema richiede multiple istanze dello stesso tratto biometrico preso dalla stessa fonte.
    - Algoritmi multipli: il sistema combina le risposte ottenute da diversi algoritmi in una singola risposta.
    - Sensori multipli: Il sistema combina le risposte ottenute da multipli sensori in una singola risposta.
- **In che modo i risultati possono essere fusi in un sistema multibiometrico? Descrivi i vari livelli di fusione.**
    
    La fusione tra sistemi può essere effettuata in vari livelli, da quello più vicino all’acquisizione del segnale a quello più vicino alla decisione finale:
    
    - **Livello del sensore**: la fusione avviene nella prima fase, prima della feature extraction. I segnali catturati dal sensore vengono fusi in un solo segnale, se questi sono compatibili. Spesso tale fusione è possibile solo se si ha lo stesso tratto biometrico e i due tipi di segnali sono uguali;
    - **Livello di feature extraction**: la fusione avviene tra feature vectors. Ad esempio è possibile estrarre le feature di due iridi differenti e poi fondere il feature vector in un solo vettore e continuare l’esecuzione in tal modo. Qui possono esserci problemi di compatibilità in quanto i vettori devono essere dello stesso tipo, per esempio non è possibile fondere istogrammi a vettori. Un altro problema è che la fusione di due vettori può portare ad uno spazio di alta dimensionalità e quindi si potrebbe dover usare una tecnica di riduzione della dimensionalità;
    - **Livello di score**: i tratti biometrici vengono processati indipendentemente da vari sottosistemi e l’insieme di scores viene fuso in un singolo score, su cui si basa la decisione. Da qui è possibile optare per due differenti approcci:
        - **Basato sulla trasformazione**: i risultati vengono normalizzati e poi combinati tra di loro in un unico risultato. La normalizzazione può non essere ottimale ed è un approccio sensibile agli *outliers*.
        - **Basato sul classificatore**: i risultati vengono inseriti in un vettore e un altro classificatore è allenato con tale vettore.
        
        Diverse regole possono essere seguite per fondere i vari score, a seconda del tipo di classificatore:
        
        - **Solo etichetta della predizione**: in caso il classificatore ritorna solo l’etichetta della classe predetta e nessuna informazione circa il rango o lo score, è possibile prendere l’etichetta votata dalla maggioranza come risultato finale;
        - **Rango**: in caso il classificatore ritorni il rango dei candidati ma non lo score, la fusione avviene tramite il *Borda count*, ovvero ogni rango viene convertito in un punteggio e tali punteggi vengono sommati per ogni classe. Viene scelta la classe con il punteggio più alto.
        - **Misura**: in caso il classificatore ritorni uno score per ogni candidato, allora è possibile combinare i vari score con metodi come la somma, la media, il prodotto, il massimo etc.
    - **Livello di decisione**: la decisione è una combinazione delle varie decisioni dei classificatori. Può essere presa secondo un’operazione logica come AND e OR tra le varie decisioni, o semplicemente si può prendere la decisione votata dalla maggioranza.
- **Cos’è il Detection and Identification rate?**
    
    Il DIR (Detection and Identification rate) al rango K viene usato nella perfomance evaluation per l’identificazione e modella la probabilità di trovare l’identità corretta in posizione k nel vettore delle distanze con un template della medesima identità. La posizione 1 modella il Genuine Acceptance Rate.
    
    È un fattore che dipende dalla threshold e quindi viene utilizzato solamente nell’identification open set.
- **Cosa manca ai tratti biometrici caratteriali? (Behavioural biometric traits)**
    
    I tratti biometrici caratteriali sono difficili da riprodurre ma mancano di permanenza, in quanto dipendono molto dall’umore e da altre caratteristiche. Sono utili per la identificazione continua nel breve periodo. Esempi di questo tipo di tratti biometrici sono la firma e la digitazione sulla tastiera.
- **Cosa si intende per doddington zoo?**
    
    Il doddington zoo è la definizione di varie classi di invididui che hanno delle proprietà comuni nell’ambito del riconoscimento biometrico. Le classi definite sono:
    
    - Pecore: produce template con match simili a se stessa e molto poco simili con templates di altre persone (Più GA che FA).
    - Capre: vengono riconosciute poco visto che i loro template non sono simili tra di loro. Causano alte FR.
    - Agnelli: sono facilmente impersonabili, ovvero i template di altre persone matchano bene con i loro template. Causano alti FA. (Un esempio di agnelli sono i bambini)
    - Lupi: riescono facilmente ad impersonare le altre persone. Causano FA quando dichiarano un’identità non genuina.
    
    Queste sono le classi che si basano su esclusivamente errori non genuini oppure genuini, vengono poi definite anche altre classi che si basano su entrambi gli errori:
    
    - Camaleonti: simili ai lui, matchano molto bene con altre persone. Divergono dai lupi in quanto matchano bene sia con se stessi sia con gli altri. Causano molti pochi FR ma anche alti FA.
    - Fantasmi: matchano male con qualsiasi persona, se stessi compresi. Questo causa un alto numero di FR ed un basso numero di FA.
    La causa è spesso perchè una persona ha dei tratti biometrici molto poveri e quindi si trovano delle difficoltà nella feature extraction.
    - Colombe: matchano molto bene con loro stessi e molto male con gli altri. Sono individui molto riconoscibili e che spesso vengono riconosciuti erroneamente, causando alti numeri di GA e FR.
    Questo accade perchè tali persone possiedono tratti poco comuni, come un naso molto distintivo.
    - Vermi: sono il peggior individuo presente, visto che matchano molto male con se stessi ma molto bene con i templates di altre persone, risultando in un alto numero di FA e bassi FR.
- **Tutti i tratti biometrici sono vulnerabili allo spoofing oppure no?**
    
    I tratti che si basano sull’apparenza sono soggetti a spoofing, i tratti comportamentali generalmente no perchè sono molto difficili da replicare.
- **Differenza tra infrarossi e luce visibile nel riconoscimento dell’iride**
    
    L’acquisizione dell’iride tramite luce visibile porta alla visione di tutti i colori che appaiono nell’iride, ma introduce diversi problemi, come il riflesso (dato da luci ambientali, lenti a contatto o occhiali), vi è la presenza di rumore sulla trama del’iride e in caso di iridi molto scure questa potrebbe essere completamente invisibile.
    
    L’acquisizione tramite luce infrarossa elimina l’informazione relativa al colore, però risolve il problema del riflesso e della poca visibilità della trama. I sensori ad infrarossi sono inoltre meno popolari a quelli a luce visibile e quindi sono spesso necessarie delle attrezzature ad-hoc.
- **Vantaggi e svantaggi del riconoscimento facciale 2D e 3D**
    
    In generale il riconoscimento facciale 3D porta numerosi vantaggi rispetto al riconoscimento facciale 2D, con il compromesso di una maggiore complessità computazionale ed un maggiore costo dei dispositivi di acquisizione.
    
    Per quanto rigurda la posa, un modello 3D non viene influenzato, visto che modella il viso a 360 gradi, a differenza di un riconoscimento 2D che modella il viso su un solo piano, quindi in caso di rotazione, di pitch o di yaw potrebbero esserci dei problemi.
    
    Il modello 3D permette inoltre di essere ruotato in un ambiente virtuale in maniera da sintetizzare le diverse illuminazioni, e quindi risolvere probelmi di diverse illuminazioni, non come un modello 2D.
    
    Comunque il modello 3D non è perfetto, in quanto è vulnerabile a variazioni di forma come chirurgia plastica, e ad altre complicanze come l’occlusione.
- **Cos’è un morphable model**
    
    Un morphable model è un modello 3D della faccia che può essere distorto in maniera tale da riprodurre ogni tipo di espressione. Questo è utile in quanto permette di tollerare le le variazioni di posa e di espressione durante il riconoscimento facciale. Il costo computazionale dell’operazione però è molto maggiore.
- **Cos’è AdaBoost? Che differenze ci sono tra un sistema di face detection basato su Adaboost e quelli basati su determinate caratteristiche del volto?**
    
    AdaBoost è una tecnica utilizzata in machine learning che consente di ottenere un classificatore forte e partire da una serie di classificatori deboli, dove un classificatore debole è semplicemente un classificatore con una bassa accuracy.
    
    L’idea è quella di assegnare ad ogni sample nel training set un peso, ed aggiornare tale in maniera tale che ad ogni iterazione i sample che vengono classificati erroneamente hanno un peso maggiore nell’iterazione successiva. Per ogni iterazione viene allenato il classificatore, e alla fine i vari classificatori che sono stati allenati per ogni iterazione vengono linearmente combinati in un classificatore forte.
- **In che modo si può calcolare la distanza tra due minutiae?**
    
    Presi due punti $a$$,b$ all’interno di un’impronta, è possibile avere una misura astratta che può modellare la distanza tramite la “ridge count”, ovvero il numero di “ridges”, ovvero le creste, che si incrociano con il segmento che va da $a$ a $b$. Questa misura è utile per confrontare due impronte in quanto spesso come punti vengono presi dei punti rilevanti, come minuzie o delta.
- **Problemi principali del riconoscimento dell’iride**
    - Visto che l’area dell’iride è molto piccola, è necessario un sensore ad alta risoluzione per catturare i vari dettagli, a infrarossi o a luce visibile.
    - In caso di acquisizione mediante sensore a luce visibile, il riflesso causato da lenti a contatto, occhiali o luce esterna potrebbe alterare la cattura;
    - Sempre se viene utilizzato un sensore a luce visibile, i dettagli di un iride molto scuri potrebbero non essere catturati;
    - Affinchè due iridi siano comparabili, i due individui dovrebbero guardare nella stessa direzione. Questo problema si può comunque risolvere con delle tecniche come l’off-axis-problem.
- **Come si può risolvere il problema dell’iride scuro? (Dark iris problem)**
    
    Utilizzando un sensore ad infrarossi, in quanto questo riesce a catturare i dettagli anche per iridi molto scuri, a differenza dei sensori a luce visibile.
- **Quali sono le differenze principali tra PCA e LDA?**
    
    La differenza principale è che PCA è un metodo non supervisionato, nel senso che non è necessario sapere l’identità della persona, mentre LDA è superivsionato, e quindi necessita di sapere l’identità associata ad ogni faccia.
    
    In maniera più generale, l’obiettivo di PCA è quello di trovare una combinazione lineare delle features che massimizzano la varianza totale del dataset, senza sfruttare l’informazione riguardante le classi; mentre l’obiettivo di LDA è quello di trovare la combinazione lineare delle features che massimizza la separazione tra le diverse classi.
- **Cosa si intende per Cross Validation?**
    
    Per cross validation si intende una tecnica per effettuare l’evaluation con differenti sottoinsiemi di training e testing, visto che diverse sottodivisioni potrebbero portare a risultati diversi.
    
    Una tecnica comune è il K-Fold Cross Validation, in cui gli elementi del dataset vengono suddivisi in K diversi sottoinsiemi tutti della stessa grandezza e per ogni iterazione un gruppo viene usato come testing set e gli altri come training set. Si finisce quando ogni gruppo è stato usato una volta come testing set.
- **Cosa sono i Gabor filters? Esempio di uso di un banco di filtri (filter bank)**
    
    I filtri di Gabor sono un tipo di filtri utilizzati principalmente per effettuare edge detection. Il filtro cattura solo le frequenze dell’immagine che sono sopra un certo livello.
    
    È possibile ottenere un feature vector a partire dall’immagine tramite la convoluzione dell’immagine con un banco di Gabor filters, ovvero un insieme di filtri con orientazioni e dimensioni differenti.
    
    Il set di immagini risultati da questa operazione permetterà di risaltare diversi contorni come occhi, naso, bocca ecc. 
- **Cos’è il Local Binary Pattern?**
    
    Local Binary Patterns è un operatore che può essere utilizzato in vari campi. Nel campo del riconoscimento facciale, viene utilizzato come feature extractor.
    
    Viene utilizzato su immagini in bianco e nero. L’idea è quella di prendere un pixel centrale, e compararlo con i suoi vicini. Solitamente si tiene conto solo di un’area di pixel $3\times3$, quindi un pixel avrà 8 vicini. Ogni valore del vicino sostituito con 1 se il pixel centrale ha valore maggiore, 0 altrimenti. Partendo dall’angolo in alto a sinistra tali valori vengono concatenati in un array formato da 8 bit. Tale array viene convertito in un numero decimale. Applicando questo procedimento per ogni pixel, è possibile costruire un array che rappresenta il vettore delle features che descrive l’immagine.
    
    È possibile comparare due vettori delle features con vari metodi di comparazione come la cosine distance, o il coefficiente di correlazione di Pearson.
    
    Questo operatore è utile in quanto è molto veloce, ed è invariante all’illuminazione. Tuttavia è sensibile ad alte variazioni come posa e rotazione dell’immagine.
- **Dove si trova il moiré pattern?**
    
    Il moiré pattern è un fenomeno che avviene quando uno schermo viene mostrato ad un sensore di acquisizione di immagini e tale immagine viene mostrata su un altro schermo. È utile per riconoscere attacchi di spoofing. 
- **Quali sono le possibili forme di impronta digitale?**
    
    Le impronte possono essere classifiate in tre macroclassi, denominate anche macro-singularities o features di primo livello. Queste sono:
    
    - Whorls
    - Loop
    - Arches
- **Possiamo usare dei modelli 3d per il volto, quali sono le strategie migliori per utilizzarli? Se voglio continuare ad avere in input modelli 2D ma nella gallery ho modelli 3D, come posso utilizzarli nel riconoscimento?**
    
    Si è possibile utilizzare dei modelli 3D per il volto. 
    
    È possibile creare un modello 3D a partire da un set di immagini 2D, visto che è possibile recuperare delle informazioni riguardanti la profondità dalle ombre.
    
    Ci sono anche altri approcci che permettono di creare un modello 3D parziale solo tramite un’immagine, con una precisione ovviamente minore.
    
    Altrimenti si potrebbe anche utilizzare il modello 3D e generare da questo delle immagini 2D mediante la proiezione, e quindi poi utilizzare tali immagini come comparazione con quelle in input.
- **Descrivi le variazioni PIE. In che modo la posa influenza? abbiamo dei metodi per valutare la posa del viso? quale rotazione distorce in modo irreparabile?**
    Per PIE si intendono quelle variazioni del viso riguardanti una differente posa, una differente illuminazione ed una differente espressione facciale, le quali potrebbero influenzare in maniera negativa il processo di riconoscimento.
    
    È possibile valutare le variazioni mediante lo score di posa, quello di illuminazione e quello di simmetria. Lo scopo di calcolare tale score riguarda la reliability del sistema, in quanto in questo modo è possibile scartare a priori quelle immagini che non sono affidabili per il riconoscimento.
    
    L’abbassare la testa e il mettersi di profilo non permettono di raccogliere tutte le informazioni relative al viso.
- **Differenza tra tratti genotipici e randotipici**
    
    I tratti genotipici sono quei tratti che vengono ereditati geneticamente dai parenti. Un esempio è la faccia, in cui alcune caratteristiche sono simili a quelle dei propri parenti;
    
    I tratti randotipici invece sono quei tratti che non vengono ereditati, oppure che ereditano solamente alcune features deboli. Un esempio sono gli occhi, la cui forma ed il colore può essere ereditata ma non i dettagli dell’iride.
- **Cos’è l’indice di Poincaré?**
    
    L’indice di Poincarè viene utilizzato nella fingerprint recogntiion per ricavare le macro-singolarità, ovvero le singolarità di primo livello (la forma dell’impronta).
    
    L’impronta viene rappresentata come una curva immersa nella directional map. L’indice di Poincarè viene definito come la rotazione totale dei vettori di questo campo una volta che la curva viene percorsa. L’indice può assumere i seguenti valori (in gradi):
    
    - 0: non sono presenti singolarità;
    - 360: è presente un vortice;
    - 180: è presente un loop;
    - -180: è presnete un delta.
- **Cosa sono le immagini integrali e come vengono usate nel calcolo delle haar features?**
    
    Un immagine integrale è una matrice i cui elementi alla coordinata ($x,y)$ hanno come valore la somma di tutti gli elementi presenti nella parte superiore a tale coordinata, quindi tutti quei valori con coordinate $x' \le x$ ed $y' \le y$. 
    
    Questo trova utilità nell’algoritmo Viola-Jones in quanto la somma di valori deve essere calcolata molteplici volte durante l’esecuzione, e quindi l’utilizzo di immagini integrali permette di ridurre il costo computazionale senza perdere informazioni.
    
    - Ecco un esempio di come le immagini integrali possono ridurre il numero di computazioni necessarie:
        
        Sia questa l’immagine:
        
        | 10 | 12 | 7 |
        | --- | --- | --- |
        | 1 | 17 | 9 |
        | 0 | 10 | 23 |
        | 12 | 8 | 71 |
        
        Si costruisce l’immagine integrale:
        
        | 10 | 22 | 29 |
        | --- | --- | --- |
        | 11 | 40 | 56 |
        | 11 | 50 | 89 |
        | 23 | 70 | 180 |
        
        Se si vuole calcolare la somma dei pixel nella terza riga, basta fare $180 - 70 = 110$  
- **Quali sono i requisiti dei tratti biometrici?**
    
    Affinchè un tratto biometrico sia affidabile, deve possedere dei requisiti. Minori i requisiti posseduri, minore l’efficienza del tratto biometrico:
    
    - *Universalità*: il tratto deve essere posseduto da ogni persona;
    - *Unicità*: il tratto di un individuo deve essere distinguibile da quello di altri individui;
    - *Permanenza*: il tratto non dovrebbe cambiare nel tempo.
    Nota: alcuni tratti sono permanenti fino ad una certa età, come la faccia, che cambia molto da giovani ma poi rimane molto simile fino ad un’età più avanzata.
    - *Collezionabilità*: il tratto deve essere misurabile o collezionato mediante qualche sensore.
    - *Accettabilità*:  gli individui coinvolti devono essere a loro agio con le procdure di collezione del tratto biometrico.
    Nota: per esempio il riconoscimento della retina oculare prevede che il sensore sia a contatto con la pupilla.
- **Cosa sono directional, density e frequency maps? A cosa servono?**
    
    La directional map è un campo vettoriale in cui ogni punto indica l’orientazione media delle ridges in quel punto. Viene utilizzata per calcolare l’indice di poincaré in un determinato punto.
    
    La density map è una matrice in cui associa ad ogni regione il numero medio di ridges presenti in quella regione.
    
    La frequency map è una matrice in cui in ogni punto determina il numero di ridges che intersecano l’ipotetico segmento che ha l’origine in quel punto ed è tangente alla direzione della ridge.
    
    Tali mappe sono utili per effettuare l’estrazione delle features. 
- **Cos’è il Cumulative Match Score e la Cumulative Match Characteristic Curve? (CMS e CMC)**
    
    IL CMS è una misura simile al DIR, però relativa alla closed set identification, in cui non è presente una threshold e quindi non è possibile calcolare il DIR.
    
    Il CMS al rango k indica la probabilità di una corretta identificazione al rango k, ovvero la probabilità di trovare il template associato all’identità corretta in posizione k nel vettore delle somigliaze ordinato.
    
    Il CMC è la curva ottenuta calcolando il CMS per ogni possibile k, dove k è il numero di soggetti nella galleria.
- **Problemi principali nell’acquisizione delle impronte**
    
    I principali problemi durante l’acquisizione delle impronte digitali sono causati da:
    
    - Impronta catturata solo in parte visto che non era centrata sul sensore;
    - Cattiva qualità della cattura dovuta ad una brutta condizione della pelle;
    - I template di due diverse impronte possono cambiare a seconda della pressione imposta sul sensore;
    - Distorsione dell’impronta a causa di movimento;
- **Dispositivi per acquisizione delle impronte, con i loro pro e contro**
    
    I dispositivi per acquisire le impronte sono principalmente tre:
    
    - Scanner ottico: è economico, ma la piastra dove poggiare il dito deve essere abbastanza grande per far entrare l’intera punta del dito, inoltre potrebbe introdurre del rumore a causa dei residui che si trovano sulla piastra.
    - Scanner capacitivo: è più piccolo e più economico dello scannero ottico, e può essere integrato in dispositivi come smartphone. La durabilità del silicio è ancora da provare e potrebbe essere meno durabile di quello ottico. Il fatto che è uno scanner piccolo significa che bisogna prestare attenzione durante la fase di enrollment.
    - Scanner termico: è tollerante alla temperatura, e questo lo permette di essere più robusto in attacchi di spoofing con impronte artificiali. È uno scanner più costoso, e l’immagine scompare molto velocemente visto che viene acquisita mediante lo sbalzo di temperatura tra il sensore e il dito.
- **Differenti tecniche per il matching delle impronte. Elenca anche i principali problemi in tali operazioni.**
    
    Le impronte possono essere matchate in varie maniere:
    
    - Basandosi sulle immagini. Vengono usati algoritmi che sovrappongono le due immagini e calcolano una somiglianza a partire da queste. Questi non sono ne molto efficienti ne accurati;
    - Basato sulle ridges. Viene estratto un feature vector che si basa sul numero di ridges, sul loro orientamento e sulla loro posizione;
    - Basato sulle minutiae. Viene estratto un feature vector basato sulla posizione e il tipo delle minutiae.
    - Ibridi. Sfruttano più informazini come entrambe le ridges e le minutiae. Un esempio è la convoluzione mediante i filtri di Gabor, tessellando prima l’immagine.
    
    Prima dell’applicazione di ognuno di questi algoritmi è spesso necessario allineare l’immagine probe con il template in galleria. Questo viene fatto prendendo come orientamento di riferimento quello che allinea il maggior numero di minutiae tra due impronte.
    
    **Dettagli sull’estrazione delle features con tessellazione e filtri gabor:**
    
    L’impronta viene tessellata, ovvero viene suddivisa in varie celle della stessa dimensione, e l’illuminazione di tale celle viene normalizzata. Per ogni cella viene estratto il feature vector tramite la convoluzione con un banco di 8 filtri di Gabor, con la stessa frequenza ma differente orientamento. I feature vector delle varie celle vengono concatenati in un solo vettore.
    
    Per effettuare il matching viene calcolata la distanza tra le minutiae con un metodo come la somma degli errori al quadrato.
    
    **Problemi:**
    
    Durante la cattura possono insorgere dei problemi che potrebbero portare ad un template con minore qualità.
    
    Questo può accadere ad esempio quando il dito non è centrato sul sensore e quindi solo una parte di questo viene catturata. In questo caso il confronto con altre impronte va fatto solamente sulla parte comune.
    
    Se la condizione della pelle non è buona, la qualità della cattura può peggiorare, così come una differente pressione sul sensore può alterare l’impronta, così come il movimento del dito sul sensore.
- **Cos’è il crossing number? A cosa serve?**
    
    Il crossing number è il numero di cambiamenti di colore che avviene nell’area vicino ad un certo pixel. A seconda di questo valore, è possibile capire in che parte dell’impronta si trova il pixel:
    
    - Se uguale a 2, allora il pixel si trova in un punto interno alla cresta. Non è un punto interessante;
    - Se uguale a 1, allora si trova in un punto di terminazione, che rappresenta una minutia;
    - Se uguale a 3, allora si trova in un punto di biforcazione, che rappresenta una minutia;
    - Se maggiore di 3, allora si trova un punto di una minutia più complessa.
- **Quali sono le fasi di processazione dell’iride**
    
    L’estrazione delle features a partire dall’immagine dell’iride avviene in diversi passaggi:
    
    1. Segmentazione: in questa estratta dall’intera immagine solamente la parte che contiene l’iride. Vengono rimosse le parti della pupilla e delle ciglia applicando un edge detector come il canny. Vengono inoltre rimossi i riflessi.
    2. Normalizzazione: viene applicata una procedure di normalizzazione come il rubber sheet model in mnaiera da ottenere immagini con formato simile a partire da iridi diverse. In questo modo qualsiasi variazione della grandezza della pupilla, che influenza la forma dell’iride, viene rimossa.
    3. Codifica: viene estratto il vettore delle features con delle tecniche come LBP.
- **Come vengono comparati due iridi?**
    
    Dopo la processazione degli iridi, e quindi quando si hanno una serie di feature vectors che rappresentano i diversi iridi, questi si possono comparare tramite una misura di distanza.
    
    Una delle più usate è la distanza di Hamming, che considera la media tra gli XOR per ogni elemento dei due vettori.
    
    In caso gli iridi presentino due maschere differenti, allora la formula è leggermente diversa.
- **Metodi per la localizzazione dell’orecchio**
    
    Sono tre i metodi principali per la localizzazione dell’orecchio:
    
    - Il primo prevede la localizzazione di punti di interesse tramite una rete neurale, che deve quindi essere prima allenata. Una volta acquisiti i punti di interesse, è possibile estrarre il rettangolo che localizza l’orecchio;
    - Il secondo prevede di utilizzare gli haar classifiers con AdaBoost, così come avviene per la localizzazione della faccia;
    - Il terzo, più complicato ma anche più accurato, sfrutta le informazioni tridimensionali dell’orecchio. Prevede una fase di training offline, in cui l’immagine viene convertita in binaria, dopo aver individuato i punti di massima curvatura, che rappresenteranno i punti di interesse. Le regioni corrispondenti all’orecchio vengono poi manualmente estatte, e vengono fuse insieme in maniera da creare un template che verrà utilizzato nella fase di testing (online) per localizzare l’orecchio. Il template è rappresentato da un istogramma che modella l’indice della forma delle varie regioni dell’orecchio. Anche durante il testing l’immagine viene convertita in binaria prima di effettuare la ricerca delle regioni che corrispondono al training template.
- **Metodi di Liveness detection nella fingerprint recognition**
    
    Sono vari i metodi utilizzati per capire se un’impronta è vera o si tratta di una replica, tra i più importanti troviamo:
    
    - Analizzare le caratteristiche dei pori della pelle tramite un sensore ad alta qualità, visto che queste sono molto difficili da replicare su un impronta finta;
    - Analizzare il colore della pelle quando il dito viene premuto sul sensore;
    - Analizzare il flusso sanguigno, la temperatura e la pulsazione, quest’ultima misurabile tramite la trasmissione di luce attraverso il dito;
    - Analizzare la resistenza che il dito ha alla corrente;
    - Verificare la presenza di sudore o meno.
- **Problemi nell’utilizzare delle foto all’interno di un dataset che, per ogni individuo, sono state scattate in diversi periodi**
    
    Il problema nel catturare foto dello stesso individuo in diverse sessioni è che in tal modo si introducono delle variazioni, che per quanto possano essere minime, possono comunque alterare il processo di valutazione. Si pensi solo alla crescita della barba in un giorno, o magari allo stato della pelle.
- **Cos’è il bertillonage?**
    
    Il bertillonage era una tecnica usata alla fine del 1800 per identificare le persone tramite diverse misurazioni a varie parti del corpo, come la faccia, le mani, il busto ecc. Queste misure venivano comparate per capire se si trattava della stessa persona o no. Questa tenica fu abbandonata dopo un indicende in cui un individuo Will West fu riconosciuto come un criminale di nome William West, molto simile a lui.
- **Cosa si intende per setting controllato e non controllato?**
    
    Un setting controllato è una situazione in cui il campione del tratto biometrico viene acquisito in maniera controllata, e quindi avrà una qualità maggiore. Dall’altra parte, in un setting non controllato non c’è nessuna garanzia riguardante la qualità. Questo porta a diverse complicanze, ma è anche il setting più realistico. 
- **Quali sono i differenti tipi di utenti?**
    
    Un utente può essere:
    
    - Cooperativo o non cooperativo, in caso l’utente stia cooperando nella fase di identificazione, oppure sia indifferente o avverso. Un individuo che non vuole essere riconosciuto è non cooperativo.
    - Privato o pubblico, in caso il sistema sia pubblicato in un ambiente privato, come un azienda, o pubblico, come in un dispositivo utilizzato pubblicamente da ognugno;
    - Consapevole o non consapevole, in caso l’utente sia consapevole o meno del processo di riconoscimento biometrico.
- **Quali sono i differenti tipi di tratti**
    
    I tratti biometrici sono classificati come:
    
    - *Fisiologici*: sono i tratti che sono naturali per la fisionomia dell’invididuo. In questa categoria troviamo le impronte, la faccia, la geometria delle mani, le orecchie ecc.
    - *Comportamentali*: sono i tratti che dipendono dal carattere e dalla personalità dell’individuo. Variano molto in base all’umore e sono molto difficili da imitare, per questo sono efficaci nel breve termine ma non nel lungo termine. Un esempio di tratto comportamentale è la firma, il modo di camminare, il modo di scrivere con la tastiera.
    - *Biologici*: esempi di tratti biologici sono il DNA, il quale è molto accurato ma l’analisi richiede giorni e la procedura di estrazione può essere invasiva.
    - *Misti:* in questa categoria troviamo dei tratti che possono appartenere a più di una delle categorie appena citate. Un esempio è la voce, che è sia un tratto fisiologico che comportamentale.
- **Differenza tra all against all e all gallery against all probes**
    
    Nella all-against-all completa, viene costruita una matrice di somiglianze in cui ogni template viene comparato con ogni altro template tranne se stesso, e quindi non c’è nessuna divisione in probe e gallery set, bensì questa viene simulata in maniera dinamica, per ogni riga della matrice, il template corrente fa da probe e tutti gli altri da gallery;
    
    Nella all-gallery-against-all-probes invece viene prima effettuata una divisione esplicita tra probe e gallery set, e poi viene costruita una matrice delle somiglianze in cui ogni probe viene comparato ad ogni elemento della gallery, ma mai ad un altro probe.
- **Cosa si intende per Curse of Dimensionality?**
    
    Per maledizione della dimensionalità si intende un fenomeno comune in vari campi, in cui al crescere delle dimensioni, il volume dello spazio cresce in maniera esponenziale, e i dati all’interno diventano sparsi. Maggiore la dimensione, più è difficile trovare della correlazione trai dati all’interno di tale spazio. È possibile rimediare a questo fenomeno tramite delle tecniche di riduzione di dimensionalità come PCA o LDA.
- **Cos’è un modello facciale in 2.5D?**
    
    Un modello in 2.5D è una rappresentazione intermedia tra il 2D ed il 3D. Un esempio di tale modello pùo essere la “Range Image”, ovvero una matrice in cui ogni coordinata rappresenta la distanza tra quel punto e la fonte di luce. Sono utilizzati quando serve avere delle informazioni tridimensionali senza effettivamente andare a costruire un modello 3D.
- **Quali sono altre tecniche per la face localization a parte Viola-Jones?**
    
    Una tecnica efficace per la localizzazione della faccia è l’algoritmo di Hsu, Mattleb e Jain.
    
    Questo algoritmo segue una serie di passaggi al fine di localizzare una faccia. A differenza di Viola-Jones, questo si focalizza sulle parti principali della faccia, come gli occhi e la bocca, e fa uso dell’informazione cromatica sull’immagine, quindi non è applicabile in caso di immagini in scala di grigi.
    
    Il primo passaggio è normalizzare il colore dell’immagine. Questo viene fatto prendendo un “bianco di riferimento”, ovvero il colore del 5% dei pixel con la luminosità più alta. Se quindi vengono trovati abbastanza pixel, l’intensità degli altri pixel viene scalata linearmente in base al bianco di riferimento.
    
    Il secondo passaggio prevede la scelta di una threshold ottimale in modo da selezionare solamente i pixel che appartengono alla faccia, considerando la varianza di colore locale.
    
    Il terzo passaggio prevede la localizzazione degli occhi, costruendo due differenti tipi di mappe, a seconda del chroma e della luma, ovvero del colore e della luminanza. Per quanto riguarda la mappa cromatica, si basa sul fatto che la zona intorno agli occhi ha una gran quantità di pixel blu e una scarsa quantità di pixel rossi; mentre per la mappa di luminanza, si fa uso delle operazioni erosione e dilatazione, le quali sono in grado di evidenziare la zona degli occhi. Le due mappe vengono messe in AND tra di loro e poi la mappa finale viene processata in maniera tale che la zona degli occhi risalti.
    
    Il quarto passaggio prevede la localizzazione della bocca, costruendo la mappa, la quale si basa sull’alta presenza di pixel rossi rispoetto a quelli blu. 
    
    Infine viene creato il contorno della faccia analizzando i vari triangoli che vengono composti dalle zone di occhi e bocca rilevate nelle precendenti operazioni. Ad ogni triangolo viene dato uno score e viene preso come migliore quello con lo score più alto, se supera una certa threshold.
- **Cosa sono erosione e dilatazione?**
    
    Erosione e dilatazione sono due operatori morfologici utilizzati per processare delle immagini.
    
    In particolare entrambi prendono in input un’immagine binaria $X$ e un elemento strutturante, anche detto kernel, $K$.
    
    Tale elemento ha un origine in un punto $x$, e questo kernel viene fatto scorrere su tutta l’immagine. In caso di dilatazione, i pixel dell’immagine in cui è presente l’origine del kernel vengono settati all’OR tra gli elementi del kernel e dell’immagine.
    
    In caso di erosione, viene preso l’AND logico.
    
    La dilatazione è utile per espandere una certa immagine e rimuovere dei “buchi” all’interno di questa, mentre l’erosione è l’operazione opposta ed è utile per restringere l’immagine e rimuovere elementi indesiderati.
- **Descrivi brevemente PCA e come viene usato nella face recognition**
    
    PCA è una tecnica di riduzione della dimensionalità. In realtà è una tecnica per la tasformazione lineare dei dati, in quanto l’obiettivo è quello di creare un nuovo sottospazio delle features in cui, una volta proiettati i dati, questi abbiamo la maggior varianza possibile.
    
    Per fare ciò, PCA trova le componenti principali, che non sono altro gli autovettori con gli autovalori maggiori. Ogni componente principale è ortogonale a tutte le componenti principali trovate in precedenza e, per questo motivo, il massimo numero di componenti principali corrisponde alla dimensionalità dello spazio originale.
    
    Visto che le componenti principali sono ordinate in ordine decrescente a seconda della varianza dei dati, è possibile considerare un sotto-spazio di dimensionalità $k<n$ mantenendo la maggior parte dell’informazione e riducendo quindi la dimensionalità.Questo approccio è applicabile al riconoscimento facciale, e in questo caso le componenti principali, ovvero gli autovettori, vengono chiamate “eigenfaces". 
    
    Una volta proiettate le immagini originali delle facce sul nuovo piano, queste possono essere confrontate tra di loro in maniera più accurata.
    
    PCA è un metodo non supervisionato, nel senso che non necessita di sapere a che classe appartengono i dati, è molto veloce ma è sensibile alle variazioni intra-classe, e quindi non riesce a riconoscere in maniera efficace un individuo sottoposto a variazioni PIE. 
- **Descrivi brevemente LDA e come viene usato nella face recognition**
    
    LDA è una tecnica di trasformazione lineare dei dati che può essere usata, così come PCA, per ridurre la dimensionalità dei dati. A differenza di PCA che crea un nuovo spazio in cui la varianza tra i dati è massimizzata, LDA massimizza la separazione tra le classi. Per questo motivo è un metodo supervisionato, nel senso che necessita di sapere le classi a priori al fine di creare il nuovo spazio.
    
    L’idea è quella di calcolare la media delle features per ogni classe e la matrice di covarianza totale, che sarà una per tutte le classi. Vengono poi calcolare le componenti distrimanti lineari per creare il nuovo sottospazio che avrà k dimensioni invece di n. Queste componenti predono il nome di Fisherfaces ed è possibile poi proiettare le nuove immagini nel sottospazio per rappresentarle con un numero minore di dimensioni, in maniera tale da aumentare l'accuratezza e l’efficienza del riconoscimento. 
- **Cos’è la System Response Reliability? (In che modo si può valutare l’affidabilità di un sistema di riconoscimento)**
    
    L’affidabilità di un sistema è una misura abbastanza importante perchè permette di scartare risultati buoni se effettuati su templates non affidabili.
    
    ### Affidabilità delle immagini in input al sistema
    
    Per quanto riguarda il riconoscimento facciale, è possibile analizzare l’affidabilità calcolando la qualità del template medio dato in input al sistema analizzando la posa, l’illuminazione e l’espressione tramite appositi score. Questo perchè template con pose avverse, espressioni esagerate e illuminazioni particolari potrebbero causare problemi nel riconoscimento, e quindi un risultato, anche se buono, potrebbe non essere affidabile.
    
    ### Affidabilità del sistema
    
    DIfferentemente dal calcolare l’affidabilità dell’immagini in input al sistema, è possibile calcolare l’affidabilità della risposta del sistema ricorrendo all’indice di System Response Reliability, o SRR, che è definito sull’intervallo tra 0 ed 1.
    
    L’indice dipende da una funzione $\phi$ che può variare. Tra le implementazioni più comuni troviamo la distanza relativa (relative distance) e il rapporto di densità (density ratio).
    
    Per quanto riguarda la distanza relativa, la funzione si basa sulla distribuzione delle somiglianze all’interno del vettore delle somiglianze. Questo perchè se tutti i valori sono ben separati, e quindi le somiglianze sono ben distribuite, vuol dire che il risultato dell’operazione sarà sicuramente più affidabile rispetto ad un vettore con i valori tra di loro molto simili. In particolare, il valore $\phi$ viene calcolato come il rapporto tra la differenza delle prime due somiglianze e il valore più alto nella lista (in caso si tratti di distanza, penso il più alto in caso di somiglianza). Più alto $\phi$, minore la densità, maggiore l’affidabilità.
    
    Per quanto riguarda il rapporto di densità, questo dipende da un certo insieme $N_b$ che contiene tutti quei template la cui distanza dal probe è minore o uguale al doppio della distanza tra il probe ed il primo elemento nella lista. In particolare formula è $1 - \frac{|N_b|}{|N|}$. Questo secondo approccio è migliore del primo in quanto dipende di meno dagli *outliers*, ovvero quei template che sono molto fuori dalla media.
    
    ---
    
    Una volta calcolato il fattore $\phi$, si può calcolare l’indice si SRR sfruttando il valore $\bar\phi$, ovvero il valore critico di massima incertezza, il quale varia a seconda del tratto biometrico e del classificatore. Il valore SRR si basa sulla distanza normalizzata tra il valore $\phi$ calcolato e il valore $\bar\phi$.
- **Come acquisire dati per costruire un modello 3D della faccia, problemi con questi**
    
    È possibile acquisire i dati per creare un modello 3D della faccia mediante diversi tipi di sensori.
    
    - Il più semplice ed economico è tramite videocamere stereoscopiche, le quali permettono di cattuare l’immagine da più punti di vista. L’accuratezza del risultato è media però il costo è basso. Come contro abbiamo la difficoltà di costruzione del modello in real-time.
    - Un altro metodo è quello di utilizzare uno scanner a luce strutturata. Un fascio di luce colpisce l’oggetto e mappa il punto in un modello 3D, e ottiene le informazioni circa la profondità a seconda della distorsione dei vari fascio di luce. Ogni scan è un’immagin in 2.5D. Al fine di ottenere un modello completo, l’operazione va ripetuta per varie prospettive. Da molteplici immagini in 2.5D si ottiene il modello 3D. L’accuratezza del risultato è medio-alta ma ad un prezzo maggiore.
    - Il metodo più accurato, ma anche quello più costoso, è tramite uno scanner a laser. Simile al metodo visto prima, in questo è presente un singolo raggio di luce, la cui luce viene deformata dall’oggetto, e in questo modo è possibile ottenere un modello 3D. Anche in questo caso la procedura va ripetuta per differenti punti di vista. Il raggio laser può danneggiare gli occhi.
    
    I problemi principali sono il fatto che potrebbero esserci dei “picchi” nel modello, causato da errori, che possono essere rimossi con dei filtri. Inoltre possono essere presenti dei buchi, che possono essere rimolti mediante smoothing gaussiano e altre tecniche. Il clutter va rimosso manualmente.
- **Differenza tra metodi locali e globali, con i pro ed i contro**
    
    I metodi globali sono quei metodi che utilizzano l’intera immagine. Un esempio di questi sono PCA, LDA e alcune reti neurali. Tra i vantaggi di questi metodi troviamo il fatto che utilizzano tutte le possibili informazioni della faccia, e che molti dei metodi sono robusti alle variazioni PIE. Tra gli svantaggi troviamo l’alta necessità computazionale, il fatto che il training e testing set devono essere altamente correlati e il fatto che, almeno nelle implementazioni basiche, ogni area dell’immagine assume lo stesso peso.
    
    I metodi locali sono invece quei metodi che considerano solo alcune aree significative dell’immagine. Un esempio sono LBP e EBGM. Tra i vantaggi di questi metodi troviamo la minor complessità computazionale, il che consente di effettuare l’estrazione delle features e il matching in maniera rapida. Inoltre i modelli sono leggeri e richiedono poca memoria. Tra gli svantaggi troviamo il fatto che deve essere effettuata una scelta su quale siano le features migliori da considerare. Se non esistono features abbastanza discriminative, allora il metodo avrà delle performance scadenti.
- **Metodi per il riconoscimento dell’orecchio (anche in generale)**
    
    Tra i differenti metodi per il riconoscimento dell’orecchio troviamo: 
    
    1. Il sistema Iannarelli, il quale parte da un’immagine 2D dell’orecchio, da cui viene estratta la ROI, prima di essere normalizzata. Viene settato come origine la radice dell’elice. Da tale origine vengono effettuate varie misurazioni, in particolare 12, ed il feature vector viene costruito con le misurazioni, il genere e l’etnia. Il metodo ha buone performance però se l’origine viene settato in maniera errata, allora tutte le misure vengono errate e le performance del metodo crollano.
    2. Un secondo metodo è quello che prevede l’utilizzo dei diagrammi di Vonoroi. Questo metodo è stato introdotto per cercare di risolvere i problemi nel sistema Iannarelli, anche se la sua risoluzione non è mai stata provata in maniera sperimentale.
    L’idea è quella di costruire dei diagrammi di Vonoroi a partire dalla ROI, e poi costruire un grafo di Vonoroi dell’orecchio, in quanto questo ha un grado di indipendenza maggiore dalle variazioni di posa ed illuminazione.
    Un diagramma di Vonoroi è una partizione del piano che si basa sulla vicinanza da un punto base, chiamato “seed”. Le partizioni nel diagramma sono chiamate celle di Vonoroi. 
    3. Il terzo metodo prevede l’utilizzo di campi di forza (force fields).
    Con questo metodo, ogni pixel dell’immagine viene trattato come un attrattore gaussiano, il cui campo di forza è proporzionale alla sua intensità. Per ogni pixel, il campo di forza viene calcolato, insieme alla forza che gli altri pixel applicano su di questo, compresa di modulo, direzione e verso.
    Vengono poi fissati dei punti in maniera ellittica intorno all’orecchio, e da questi viene seguito il campo di forza presente da quel punto fino all’orecchio. Le linee di tutti i punti convergono in punti chiamati “sinks”.
    Questi sinks possono essere considerati le features di un particolare orecchio, e quindi poi il matching tra due orecchie considera tali punti in maniera tale da avere una misura di somiglianza. 
    4. Il quarto metodo invece utilizza i punti di interesse.
    L’immagine dell’orecchio viene convoluta con dei filtri di Gabor, e i rispettivi Gabor jets vengono estratti dai punti di interesse. Questi gabor jets possono essere usati come i nodi per costruire un grafo dell’orecchio. 
    Viene usato PCA per estrarre il cosiddetto “eigenear graph”. La recognition viene effettuata costruendo il medesimo grafo per il probe e poi confrontandolo con i vari grafi nella galleria.
- **Cosa si intende per Wavelet Transforms e in che maniera differisce da Fourier Transforms**
    
    Fourier Transform è un algoritmo che permette di estrarre le varie frequenze a partire da un segnale. È utile per capire quali frequenze, e in che quantià, queste appaiono all’interno di un determinato segnale. Questo algoritmo però non ritorna l’informazione riguardante il tempo in cui le frequenze appaiono, cosa che invece fa il Wavelet Transforms.
- **Quali sono i vari step per effettuare la segmentazione dell’iride?**
    
    Per effettuare una buona segmentazione, sono necessari dei passaggi ben definiti, come:
    
    - Preprocessazione dell’immagine, utile a rendere più precisa la segmentazione. Una tecnica è ad esempio la posterizzazione, in cui l’immagine viene divise in celle di uguale grandezza, ed i pixel all’interno di ogni cella vengono sostituiti con il pixel che appare la maggior parte delle volte.
    - Localizzazione dell pupilla, in quanto il centro della pupilla è necessario nella fase di normalizzazione, in oltre la pupilla va rimossa dall’iride in quanto non fa parte di questo. Spesso al pupilla è la zona più scura dell’immagine, ma non sempre questo è vero per esempio in immagini con del rumore o dei riflessi. Viene usato il canny edge detector con threshold differenti per capire quali sono le possibili regioni circolari, e ad ognuna di queste viene assegnato uno score a seconda dell’omogeneità e separabilità. La sezione della pupilla sarà rappresentata dalla regione circolare con lo score più alto;
    - Linearizzazione: consiste nel normalizzare l’immagine mappando ogni punto dalle coordinate cartesiane a coordinate polari, in cui il centro di riferimento è il centro della pupilla.
    - Localizzazione del limbus corneale, che è la regione tra la cornea e la sclera. Questo viene trovato sfruttando il fatto che la zona della pupilla occupa la parte più in basso dell’immagine normalizzata, e quindi il limbus sarà la parte più chiara subito sopra a quella regione.
    
    Una volta fatto ciò, è possibile segmentare l’immagine e trovare solamente la zona dell’iride.
- **Cos’è l’EBGM (Elastic Bunch Graph Matching)?**
    
    L’Elastic Bunch Graph Matching è una tecnica che può essere utilizzata per il riconoscimento facciale.
    
    Una faccia può essere rappresentata tramite un grafo in cui i nodi sono rappresentati dai Gabor jets, che descrivono le texture locali in un determinato punto, mentre i collegamenti tra i nodi rappresentano la distanza tra i vari nodi all’interno dell’immagine.
    
    L’idea è quella di costruire un grafo che rappresenti tutte le facce in una certa posa, in maniera tale che poi possa essere confrontato con un’altra faccia per effettuare il matching.
    
    Visto che l’operazione di Gabor wavelets transform ritorna una serie di valori per ogni pixel in cui viene applicata, l’insieme di questi valori viene chiamato Gabor jet, e contiene le informazioni relative alla texture locale.
    
    Ogni nodo all’interno di un bunch graph non corrisponde ad un solo jet, ma ad un insieme di jet. I collegamenti rappresentano sempre la distanza, ma stavolta è la distanza media tra i due nodi nelle varie immagini che il bunch graph modella.
    
    Generalmente il bunch graph viene costruito nella seguente maniera:
    
    - Inizialmente, viene presa un’immagine e il bunch graph corrisponde al grafo di quella immagine.
    - Per ogni altra immagine, si crea un altro grafo e si fa il match con il bunch graph. Si cerca di cambiare il grafo dell’immagine finchè il match non è migliore. Una volta arrivati a questo punto, si fondono i due grafi e si ottiene un bunch graph con due immagini.
    - Si ripete questo per le prime $k$ immagini, dove $k$ è una partizione delle immagini totali.
    - Per le altre immagini, viene solo calcolato il grafo e poi si può inserire l’immagine nel bunch graph automaticamente visto che il bunch graph già descrive la struttura in maniera molto generalizzata.
    
    Quando arriva un probe che deve essere comparato, si calcola il suo grafo e si effettua il matching con il bunch graph, che ritornerà tanti valori di somiglianza quante sono le immagini modellate dal bunch graph. Si prende come valido l’identità con la somiglianza maggiore.
- **Modi di dividere il dataset in training e testing e in probe e gallery.**
    
    Per quanto riguarda la divisione in training e testing, è possibile effettuarla:
    
    - Per samples, nel senso che non esisteranno identità presenti solamente nel training o nel testing set;
    - Per soggetto, nel senso che alcune identità appaiono solamente nel testing set e non nel training set. Questo fa si che il sistema sia valutato in maniera più robusta, perchè si possono vedere le performance per soggetti mai visti. (Nota che il caso contrario aumenta le performance in nessun modo).
    
    Ovviamente non è possibile che uno stesso sample sia presente in entrambi gli insiemi. 
    
    Per quanto riguarda la divisione tra probe e gallery set, abbiamo diverse buone usanze:
    
    - Inserire nella galleria i samples con la qualità migliore, visto che spesso l'enrollment avviene in condizioni controllate, a differenza del probe la cui qualità potrebbe essere peggiore;
    - Utilizzare samples con il soggetto in diverse variazioni all’interno della galleria, in maniera tale che il probe sia comparato con differenti pose e condizioni.
- **Cosa si intende per Impostor e Client score distribution**
    
    L’impostor score e il client score descrivono la distribuzione data dalla probabilità di ottenere un certo valore di somiglianza $s$, dato che il probe è impostore o genuino. 
- **Cosa sono e come vengono utilizzati LBP, Blob e LBP-BLOB nel iris recognition.**
    
    È possibile utilizzare LBP per estrarre le features a partire dall’immagine linearizzata dell’iride. L’immagine si può dividere in fasce vericali, orizzontali o in blocchi, e poi viene presa come somiglianza la media delle somiglianze delle varie sezioni, comprate 1 ad 1 tra il template e il probe.
    La divisione in bande orizzontali è quella che generalmetne ottiene performance maggiori
    
    Un altro metodo per l’estrazione delle features e il matching è utilizzando i Blobs, ovvero delle regioni particolari dell’iride. All'immagine dell’iride normalizzata viene applicata la “laplacian of gaussian” con scale differenti. Le immagini vengono poi fuse tra di loro e viene usata la distanza di hamming per effettuare il matching. 
    Una variazione prevede la concatenazione invece della fusione delle varie immagini, e l’utilizzo della distanza di hamming media tra le varie immagini per effetuare il matching. 
    
    È possibile concatenare LBP e Blobs in un unico metodo, che empiricamente funziona meglio dei due metodi presi singolarmente. Gli encodings vengono concatenati, e viene presa come distanza la media tra i due metodi. 
- **Dettagli su come possono essere fusi due feature vector in un sistema multibiometrico**
    
    È possibile effettuare due tipi di fusione a livello di feature vector:
    
    - Serialmente: i due vettori possono essere concatenati in un singolo vettore. Si può usare u nmetodo più avanzato per la fusione come il SIFT, oppure si possono concatenare solamente dei gruppi di features, come ad esempio dei particolari punti di interesse all’interno della faccia;
    Con questo metodo il vettore risultante generalmente sarà più grande di entrambi i vettori.
    - In parallelo: i due vettori vengono fusi mediante una combinazione. I vettori vengono portati alla stessa grandezza, nel senso che il vettore più corto viene “allungato”. Per trovare dei buoni coefficienti per la combinazione si può usare la Canonical Correlation Analysis, che consiste nel trovare i coefficienti che massimizzano la correlazione tra le features.
    Con questo metodo il vettore risulante sarà pari alla lunghezza del vettore con lunghezza maggiore.
- **Problemi nella cattura di impronte latenti**
    
    Durante la cattura di impronte latenti, si possono identificare vari problemi:
    
    - Umidità, polvere ed ulteriori segni sulla superfice dove risiede l’impronta possono introdurre del rumore nella cattura;
    - L’impronta lantente può essere incompleta;
- **Quali sono le feature importanti in un modello 3D?**
    
    Gli algoritmi per il riconoscimento facciale 3D si basano sulle curvature locali e globali del modello al fine di effettuare il riconoscimento. 
- **In che maniera due modelli tridimensionali possono essere allineati? Fai la differenza tra metodo più grossolano ed il metodo più avanzato.**
    
    È possibile effettuare un allineamento più grossolano e uno più avanzato:
    
    - Per quanto riguarda quello grossolano, si possono prendere dei punti di interesse sulla faccia e allineare le facce minimizzando la distanza tra le rispettive coppie di punti tra i due modelli.
    - Per quanto riguarda quello più avanzato, questo si basa sull’algoritmo ICP (Iterative Closest Point). L’idea di questo algoritmo è di prendere un match iniziale tra i due modelli, comparare la distanza tra le superfici e muovere un modello in maniera che questa distanza diminuisca. Questo viene fatto iterativamente fino a che la distanza non ha raggiunto una soglia minima. È un metodo più accurato ma è costoso a livello computazionale, e non è assicurato che converga.
- **Nell’ambito face recognition 3D, cos’è una normal map? Perchè è utile al fine del riconoscimento?**
    
    Una normal map è una proiezione di un modello 3D in uno spazio 2D. La mappa contiene delle componenti RGB che indicano le componenti X, Y e Z della normale alla superficie e consentono di avere un’informazione riguardo la profondità.
    
    Questo è utile in quanto le operazioni su una normal map sono molto più leggere rispetto alle operazioni su un modello tridimensionale.
- **Nell’ambito face recognition 3D, cosa sono le Iso-Geodesic Stripes? In che maniera vengono utilizzate? Parla anche del 3DWW**
    
    Visto che effettuare operazioni sull’intero modello facciale in 3D è computazionalmente costoso, è possibile utilizzare la distanza euclidea e quella geodetica insieme agli angoli tra circa 47 punti di interesse per catturare abbastanza informazioni facciali. La detection automatica dei punti di interesse però è un’operazione difficile. 
    
    Nell’approccio delle strisce iso-geodetiche, viene utilizzata l’informazione riguardante tutta la faccia. L’idea è di creare un grafo della faccia, in cui ogni nodo rappresenta una striscia iso-geodetica. La faccia viene divisa in tante strice iso-geodetiche di stessa larghezza, che si propagano dalla punta del naso.
- **Qual è e come viene usato l’operatore per micro-texture analysis nella face recognition?**
    
    Un tipo di operatore per l’analisi delle micro-texture è il multi-scale LBP. L’operatore LBP viene quindi usato su finestre di differente dimensione. I vari feature vector ottenuti vengono poi concatenati e dati in pasto ad un SVM, il quale è stato precedentemente allenato sullo stesso tipo di istogrammi. La SVM ritornerà la decisione sull’autenticità o meno della faccia.
- **Quando avvengono FA, FR, GA e GR in un sistema identificazione open-set e nella verifica?**
    - False Acceptance: avviene quando un impostore viene erroneamente accettato dal sistema.
    - False Rejection: avviene quando un utente genuino registrato nel sistema viene identificato come impostore e quindi erroneamente rifiutato;
    - Genuine Acceptance: avviene quando un utente genuino viene correttamente accettato dal sistema;
    - Genuine Rejection: avviene quando un utente impostore viene correttamente rifiutato dal sistema.
    
    **Nello specifico, per quanto riguarda identificazione open-set:**
    
    - Utente genuino appare al primo posto nella lista: Genuine Acceptance e DIR(1);
    - Utente genuino appare al posto k nella lista: False Rejection, DIR(k);
    - Utente impostore ritorna una lista con almeno un’identità valida (sotto la threshold di distanza o sopra quella di somiglianza): False Acceptance;
    - Utente impostorre ritorrna una lista senza identità valida: Genuine Rejection.
    
    **Mentre per quanto riguarda la verifica:**
    
    - Utente con claim genuino viene accettato: Genuine Acceptance;
    - Utente con claim genuino viene rifiutato: False Rejection;
    - Utente con claim impostore viene accettato: False Acceptance;
    - Utente con claim impostore viene rifiutato: Genuine Rejection.
- **Quando avvengono FA, FR, GA e GR in un sistema identificazione closed-set?**
    - False Acceptance: non è definito in quanto non sono presenti impostori
    - False Rejection: avviene quando un utente viene identificato come un’altro utente
    - Genuine Acceptance: avviene quando un utente viene correttamente identificato
    - Genuine Rejection: non è definito in quanto non sono presenti impostori

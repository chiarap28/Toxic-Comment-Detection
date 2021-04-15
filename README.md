# TOXIC COMMENT DETECTION

Si tratta di un problema di classicazione multi-label che identichi la tossicità, le minacce, l'oscenità e l'odio
razziale all'interno di un insieme di commenti in lingua inglese estratti da Wikipedia.
I modelli sono stati addestrati e validati con quattro diversi livelli di preprocessing, elencati di seguito, al fine
di valutare quanto ognuno di essi incide sull'accuratezza della classificazione.
1. Punteggiatura e cifre: sono stati rimossi da tutti i commenti che com-
pongono il dataset qualsiasi tipo di punteggiatura e le cifre.
2. URL, abbreviazioni, stop words (SW): sono stati rimossi - attraverso
l'utilizzo delle espressioni regolari (RE) gli URL. Sempre attraverso le
RE, sono state estese le abbreviazioni - sia quelle tipiche dello slang
inglese e sia quelle inerenti alle parole "tossiche" - come per esempio
I'll -> I will. In seguito, è stata rimossa la lista delle 179 SW in inglese
offerta da nltk. Il testo viene portato in lower case. Tutte le modifiche
si aggiungono a quelle del punto 1.
3. Lemmatizzazione: al punto 2, viene aggiunta la lemmatizzazione, un
processo grazie al quale i token vengono ricondotti alla propria radice
- ovvero alla forma che si trova all'interno del dizionario. Inizialmente,
dopo aver tokenizzato il testo, viene applicato il treebank POS tagging
attraverso la libreria nltk. Successivamente, i tag risultanti vengono
trasformati nei corrispondenti WordNet tag, necessari a rendere più
accurato il lemmatizzatore di WordNet utilizzato.
4. Stemming: al testo tokenizzato viene applicato il Lancaster Stemmer.
Lo stemming elimina gli affissi (sia suffissi che prefissi) dai token analizzati. 
Tutte le modifiche vengono aggiunte a quelle del punto 2.
Ciò che attrae maggiormente l'attenzione è la diminuizione
del valore dell'AUC man mano si aggiungono livelli di preprocessing successivi al primo e al secondo. Nonostante in letteratura si legga dei vantaggi
che lemmatizzazione e stemming comportano a livello di accuratezza in un
problema di classificazione di testi, in questo caso si nota che sembra essere sufficiente l'eliminazione di punteggiatura, cifre e rumore (come URL,
tag, ecc.). Questo fenomeno può essere spiegato anche da un punto di vista linguistico. L'inglese è una lingua con morfologia 
flessiva, ma - rispetto
alle altre lingue indoeuropee - presenta una quantità minima di 
flessione, in
quanto manca di genere grammaticale e concordanza aggettivale. Inoltre, in
inglese, la radice lessicale ***nuda*** può costituire una parola, mentre in italiano
non è così (***can-*** non può costituire una parola, mentre ***dog-*** sì).
Prese in considerazione queste nozioni linguistiche, il lavoro di preprocessing
che include lemmatizzazione dovrebbe restituire risultati migliori con lingue
fortemente 
flessive come l'italiano. Per quanto concerne lo stemming, invece, i miglioramenti potrebbero non essere osservabili in quanto comporta
la creazione di non-parole.
Per questo motivo, i modelli definiti sono stati testati anche con un
corpus di tweet scritti in lingua italiana, utilizzato durante la commpetizione
SENTIPOLC-16 di Evalita. Il task scelto è il numero 2, che prevede come
target due classi: positività e negatività dei commenti.

cartella **data**: inserire qui il dataset https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data

cartella **glove.twitter.27B**: inserire qui il file di word embedding ***GloVe

cartella **dataft**: inserire qui il file di word embedding ***FastText

cartella **data_it***: inserire qui il dataset ***SENTIPOLC16 di Evalita

cartella **model_**: contiene i migliori modelli per il dataset in inglese (.h5)

cartella **results**: contiene i file submission per ogni topologia testata

cartella **images**: contiene le immagini dei modelli 

cartella **models_it**: contiene i migliori modelli per la lingua italiana (.h5)

**Text_Preprocessing.ipynb**: data preprocessing

**Text_Preprocessing_it.ipynb**: data preprocessing per italiano

**CNN, CNN-it, LSTM, LSTM-it, Bi-LSTM, Bi-LSTM-it.ipynb**: costruzione e training dei modelli

**Predict.ipynb**: predizione con i modelli migliori

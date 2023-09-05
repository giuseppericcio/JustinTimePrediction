# Studio di tecniche di predizione 'Just-in-Time' di commit difettosi nello sviluppo software in contesti di Continuous Integration 📚

## Introduzione 📝
All’interno di questa tesi di Laurea verranno trattate le tecniche di predizione di commit difettosi nell’ambito dello sviluppo del software usando la metodologia **DevOps**.

<p align="center">
  <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%201.png" width="700" height="400">
</p>

In particolare, ci si riferisce al modello **Continuous Integration** che prevede una pipeline di deployment ben definita, mostrata di seguito:

<p align="center">
  <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%202.png" width="750" height="200">
</p>

Innanzitutto, occorre definire cosa si intende con il termine **commit**, esso indica quell’operazione di aggiunta, modifica e/o rimozione di file all’interno di una cartella di lavoro, che può essere locale o distribuita; nel caso di directory distribuite ci si avvale del supporto di strumenti per il controllo di versione come GitHub. 🌐

## Metodologia: Just-in-Time Prediction ⏱️
In particolare, si affronta attraverso l’uso della metodologia del **Just-in-Time Prediction**, il problema dell’estrazione delle metriche a partire da un log di commit e la conseguente creazione di un file .csv. Il file con le metriche estratte dai commit viene diviso in tre sottoinsiemi, in particolare si avrà training set, validation set e testing set al fine di etichettare ogni commit come difettoso o meno con l’uso di particolari algoritmi di **Machine Learning**. 🧠

### Workflow seguito nella trattazione 🛠️

<p align="center">
<img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%206.png" width="700" height="400">
</p>

## Step 1: Estrazione Commit History 📝
Per l'estrazione dei commit da un progetto su **GitHub** si è fatto uso del tool online [CommitGuru](http://commit.guru/) che permette di effettuare tale operazione in maniera semplice ed intituiva come mostrato nella seguente Figura.

<p align="center">
<img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%209.png" width="740" height="440">
</p>

## Step 2: Addestramento del JIT Models 🤖
Per addestrare il modello di **Just-in-Time Prediction** occorre costruire, a partire dalla commit history, il **training set** contenente le metriche (feature) rilevanti al fine della classificazione dei commit come previsto da questa tecnica.
In particolare, tramite lo stesso tool visto in precedenza si ottiene il file .csv con le metriche dei commit, come mostrato in Figura.

<p align="center">
<img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%2011.png" width="740" height="600">
</p>

### Addestramento dei modelli ML su Weka 🦤: Logistic Regression e Random Forest
Per costruire i modelli predittivi si è scelto di confrontare le prestazioni di due diversi modelli nell'esecuzione del medesimo task di classificazione, in particolare si sono scelti un modello di **Logistic Regression**, particolarmente adatto a classificazioni binarie come nel nostro caso (il commit o è difettoso o non lo è), mentre l'altro modello scelto è il **Random Forest** che risulta un modello particolarmente utile quando si vogliono evitare troppi falsi positivi nei risultati di classificazione. Per effettuare l'addestramento di questi modelli si è usato [Weka](https://www.cs.waikato.ac.nz/ml/weka/), un tool scritto in Java da un gruppo di ricerca dell'Università della Nuova Zelanda; esso permette di allenare un modello senza scrivere codice con il supporto di un'interfaccia grafica (come in Figura).

<p align="center">
<img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%2015.png" width="700" height="550">
</p>

## Step 3: Validazione del Modello ✔️
Poi ci si preoccupa di validare questo modello sottoponendogli il secondo insieme di commit, ovvero il **validation set**, che permette di verificare le prestazioni relative di un dato modello rispetto ad un altro al fine di scegliere il modello più opportuno per la predizione. 📊

## Step 4: Test del Modello 🧪
Il terzo insieme di dati, non utilizzati nei passaggi precedenti, permette di testare il modello scelto, da cui il nome testing set; con la fase di test del modello si ottengono le prestazioni in operation, ovvero si osserva come il modello si comporta nella predizione di nuovi commit rappresentativi di rilasci successivi. 📈

Per effettuare tale valutazione si possono utilizzare varie metriche, quelle scelte nel caso in esame sono tre ovvero:
- la curva caratteristica di funzionamento del ricevitore (**Area Under the receiver operating characteristic Curve**, AUC);
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%2016.jpg" width="500" height="400">
  </p>
  
- il coefficiente di correlazione di Matthews (**Matthews Correlation Coefficient**, MCC);
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Formule/MCC.svg" width="400" height="200">
  </p>
  
- il punteggio Brier (**Brier Score**).
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Formule/Brier.svg" width="200" height="100">
  </p>

## Caso di Studio: App Immuni 📱
Infine, si tratta un caso di studio particolare, quello dall’app Immuni nelle due versioni per sistemi operativi mobile, ovvero Android e iOS, al fine di mettere in pratica il processo di predizione ‘Just-in-Time’ e verificare alcuni risultati molto importanti.

### Estrazione Commit (sia per iOS che Android)

<p align="center">
  <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/70e1188c720a4a81c97ad300d7b4994b80c1ecf3/Figure/Figura%2018.png" width="700" height="400">
</p>

### Addestramento dei modelli
- **Versione Android** 📱 (```Logistic Regression -> AUC=0.551```, ```Random Forest -> AUC=0.527```)
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/e8c4fd5b816ff6002c879bb073bd638ab44c3a7b/Grafici/AUC_Android_Training.png" style="width:50%">
  </p>
  
- **Versione iOS** 🍏 (```Logistic Regression -> AUC=0.463```, ```Random Forest -> AUC=0.533```)
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/e8c4fd5b816ff6002c879bb073bd638ab44c3a7b/Grafici/AUC_iOS_Training.png" style="width:50%">
  </p>
  
### Valutazione dei modelli
- **Versione Android** 📱 (```Logistic Regression -> AUC=0.929```, ```Random Forest -> AUC=0.571```)
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/e8c4fd5b816ff6002c879bb073bd638ab44c3a7b/Grafici/AUC_Android_Testing.png" style="width:50%">
  </p>
  
- **Versione iOS** 🍏 (```Logistic Regression -> AUC=0.417```, ```Random Forest -> AUC=0.333```)
  
  <p align="center">
    <img src="https://github.com/giuseppericcio/JustinTimePrediction/blob/e8c4fd5b816ff6002c879bb073bd638ab44c3a7b/Grafici/AUC_iOS_Testing.png" style="width:50%">
  </p>
  

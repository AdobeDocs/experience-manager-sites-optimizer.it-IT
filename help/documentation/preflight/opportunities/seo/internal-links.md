---
title: Verifica collegamenti interni verifica preliminare
description: Scopri l’audit dei collegamenti interni in Verifica preliminare per AEM Sites Optimizer.
source-git-commit: d87b607248efdeecf1ba29ede03bf1628d1dff30
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%
---
# Audit dei collegamenti interni

L&#39;audit di **Collegamenti interni** esamina i collegamenti presenti nella pagina che puntano al tuo sito. Il controllo di audit controlla ogni collegamento interno dalla pagina che stai modificando e contrassegna quelli interrotti, non sicuri o puntati da qualche parte che un visitatore non può seguire.

## Perché è importante

Un collegamento interno interrotto è un vicolo cieco per il lettore e una scansiona inutile per un motore di ricerca, che non passa alcun valore sulla pagina che doveva raggiungere. I collegamenti interni sono anche il tipo più semplice per rompere per errore: una pagina viene spostata o rinominata e ogni collegamento ad essa smette silenziosamente di funzionare. Poiché i collegamenti si trovano tutti sul tuo sito, puoi anche correggerli da solo.

## Controlli dell’audit

L’audit segnala un’opportunità per ogni collegamento interno che presenta uno dei seguenti problemi:

* **Collegamento interrotto:** restituisce un errore, ad esempio `Status 404` o `Status 500`. Un collegamento che raggiunge l’errore dopo un reindirizzamento viene segnalato nello stesso modo.
* **Collegamento non sicuro:** il collegamento utilizza `http://` invece di `https://`. Quando funziona la versione protetta dello stesso URL, la verifica preliminare offre il suggerimento.
* **URL editor:** il collegamento punta a un URL dell&#39;editor di AEM anziché alla pagina del contenuto. Il collegamento funziona durante l’authoring ed è questo che lo rende facile da ignorare, ma ogni visitatore arriva all’interfaccia di authoring. Verifica preliminare suggerisce l’URL del contenuto.
* **Frammento mancante:** il collegamento punta a un ancoraggio, ad esempio `#pricing`, che non è presente nella pagina di destinazione. La pagina si apre ancora, ma il lettore arriva in cima invece della sezione che intendevi creare, quindi questo viene segnalato con un impatto inferiore rispetto a un collegamento interrotto. Se la pagina presenta lo stesso ancoraggio con maiuscole e minuscole diverse, Verifica preliminare suggerisce l&#39;ancoraggio corretto. Se la pagina di destinazione stessa è danneggiata, viene invece segnalato come **collegamento interrotto**.
* **Collegamento non verificato:** timeout del controllo o errore di rete. La verifica preliminare non è in grado di stabilire se il collegamento funziona, pertanto richiede di controllare il collegamento personalmente anziché segnalarlo come interrotto.

Un collegamento che si risolve correttamente non viene contrassegnato, anche quando sono presenti più reindirizzamenti durante il percorso. Non è nemmeno un collegamento che reindirizza a un sito diverso, perché non è più un collegamento interno.

## Controllo dei collegamenti

Il controllo di audit controlla i collegamenti dalla sessione di authoring, in modo da visualizzarli nel modo in cui hai effettuato l’accesso. Una pagina che esiste solo nell’istanza di authoring viene risolta correttamente invece di apparire interrotta.

I collegamenti che AEM Link Checker ha già contrassegnato come non validi vengono inclusi nel controllo di audit, anche se l’editor rimuove il collegamento cliccabile dalla pagina. Vengono quindi ricontrollate anziché considerate attendibili, pertanto non viene segnalato un collegamento che da allora ha iniziato a funzionare.

Viene segnalata un’opportunità per ogni posizione in cui appare un collegamento, quindi un collegamento errato utilizzato in tre punti offre tre istanze da correggere, ciascuna delle quali evidenzia il proprio punto sulla pagina. Quando uno di questi punti presenta più di un problema, la verifica preliminare li mostra insieme su un&#39;unica scheda.

## Limitazioni note

Il controllo di audit viene eseguito nell’Editor pagina di AEM Sites, in Adobe Managed Services (AMS) e nell’authoring basato su documenti tramite Sidekick. Attualmente non è disponibile nell’Editor universale.

## Come risolvere

Quando il controllo di audit individua le opportunità, ciascuna di esse descrive il problema e la modifica consigliata e identifica il collegamento coinvolto. Utilizza **Evidenzia a pagina** per passare direttamente al collegamento nel contenuto e utilizza la sezione **URL corrente** per copiare l&#39;URL o aprirlo in una nuova scheda in modo da poter confermare il problema. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

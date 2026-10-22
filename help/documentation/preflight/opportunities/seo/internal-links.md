---
title: Verifica collegamenti interni verifica preliminare
description: Scopri l’audit dei collegamenti interni in Verifica preliminare per AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 59c097682899889aa2a5d76333f80cc58e28ff1e
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%
---
# Audit dei collegamenti interni

L&#39;audit di **Collegamenti interni** esamina i collegamenti presenti nella pagina che puntano al tuo sito. Il controllo di audit controlla ogni collegamento interno dalla pagina che stai modificando e contrassegna quelli interrotti, non sicuri o puntati da qualche parte che un visitatore non può seguire.

## Perché è importante

Un collegamento interno interrotto è un vicolo cieco per il lettore e una scansiona inutile per un motore di ricerca, che non passa alcun valore sulla pagina che doveva raggiungere. I collegamenti interni sono anche il tipo più semplice per rompere per errore: una pagina viene spostata o rinominata e ogni collegamento ad essa smette silenziosamente di funzionare. Poiché i collegamenti si trovano tutti sul tuo sito, puoi anche correggerli da solo.

## Controlli dell’audit

L’audit segnala un’opportunità per ogni collegamento interno che presenta uno dei seguenti problemi:

* **Collegamento interrotto:** il collegamento restituisce un errore, ad esempio `Status 403` o `Status 404`, oppure restituisce `Status 500` o `Status 501` dopo un nuovo tentativo di verifica preliminare. Un collegamento che raggiunge l’errore dopo un reindirizzamento viene segnalato nello stesso modo.
* **Collegamento non sicuro:** il collegamento utilizza `http://` invece di `https://`. Quando funziona la versione protetta dello stesso URL, la verifica preliminare offre il suggerimento.
* **URL editor:** il collegamento punta a un URL dell&#39;editor di AEM anziché alla pagina del contenuto. Il collegamento funziona durante l’authoring ed è questo che lo rende facile da ignorare, ma ogni visitatore arriva all’interfaccia di authoring. Verifica preliminare suggerisce l’URL del contenuto.
* **Frammento mancante:** il collegamento punta a un ancoraggio, ad esempio `#pricing`, che non è presente nella pagina di destinazione. La pagina si apre ancora, ma il lettore arriva in cima invece della sezione che intendevi, quindi è meno grave di un collegamento interrotto. Se la pagina presenta lo stesso ancoraggio con maiuscole e minuscole diverse, Verifica preliminare suggerisce l&#39;ancoraggio corretto. Se la pagina di destinazione stessa è danneggiata, viene invece segnalato come **collegamento interrotto**.
* **Collegamento non verificato:** il controllo è scaduto o ha restituito un errore di rete oppure il collegamento ha continuato a restituire `Status 429` (troppe richieste) o un errore del server diverso da `Status 500` o `Status 501`, ad esempio `Status 503`. La verifica preliminare non è in grado di stabilire se il collegamento funziona, pertanto richiede di controllare il collegamento personalmente anziché segnalarlo come interrotto.

Un collegamento che si risolve correttamente non viene contrassegnato, anche quando sono presenti più reindirizzamenti durante il percorso. Non è nemmeno un collegamento che reindirizza a un sito diverso, perché non è più un collegamento interno.

## Controllo dei collegamenti

Il controllo di audit controlla i collegamenti dalla sessione di authoring, in modo da visualizzarli nel modo in cui hai effettuato l’accesso. Una pagina che esiste solo nell’istanza di authoring viene risolta correttamente invece di apparire interrotta. Poiché il sito è in esecuzione e si è connessi, un errore come `Status 403` o `Status 500` indica un problema con la pagina collegata.

I collegamenti che AEM Link Checker ha già contrassegnato come non validi vengono inclusi nel controllo di audit, anche se l’editor rimuove il collegamento cliccabile dalla pagina. Vengono quindi ricontrollate anziché considerate attendibili, pertanto non viene segnalato un collegamento che da allora ha iniziato a funzionare.

Quando si verifica un timeout, viene riscontrato un errore di rete o viene restituito `Status 429` o un errore del server, la verifica preliminare ritenta il collegamento fino a due volte. Collegamento che funziona in caso di nuovo tentativo non segnalato.

Viene segnalata un’opportunità per ogni posizione in cui appare un collegamento, quindi un collegamento errato utilizzato in tre punti offre tre istanze da correggere, ciascuna delle quali evidenzia il proprio punto sulla pagina. Quando uno di questi punti presenta più di un problema, la verifica preliminare li mostra insieme su un&#39;unica scheda.

## Includi collegamenti di spostamento del sito

Per impostazione predefinita, il controllo dei collegamenti interni ignora i collegamenti di navigazione del sito. Questi collegamenti non vengono né controllati né segnalati. Un collegamento nel corpo della pagina viene comunque selezionato anche se lo stesso URL viene visualizzato anche in un menu.

Un collegamento conta come navigazione se il collegamento stesso o qualsiasi elemento precedente è un elemento `<nav>` o ha un attributo `role="navigation"`.

Per includere i collegamenti di navigazione nella successiva esecuzione del controllo:

1. Prima di avviare un controllo di audit o al termine di un&#39;esecuzione, apri **Impostazioni** (icona a forma di ingranaggio) nell&#39;intestazione Verifica preliminare. Se l&#39;icona ingranaggio non è visibile, apri **Altre azioni** (**...**) e selezionare **Impostazioni**.
1. Selezionare **Mostra collegamenti di spostamento del sito**.
1. Selezionare **Analizza pagina** per avviare un&#39;esecuzione oppure **Rianalizza** se i risultati sono già visualizzati.

![Il menu Impostazioni verifica preliminare con l&#39;opzione Mostra collegamenti di navigazione del sito](./assets/internal-links/settings-menu.png){align="center"}

**Mostra collegamenti di spostamento del sito** controlla i collegamenti ai controlli di controllo, non solo i risultati visualizzati.

La modifica dell’impostazione non avvia un controllo di audit né modifica i risultati già visualizzati sullo schermo. Quando tali risultati hanno utilizzato un&#39;impostazione diversa, viene visualizzato un punto in **Rianalizza**, con l&#39;etichetta **Rianalizza per applicare le nuove impostazioni**. Esegui nuovamente i controlli di audit per applicare la modifica o ripristina l’impostazione precedente per cancellare il punto.

Verifica preliminare salva l&#39;impostazione nel browser e la mantiene dopo la disconnessione. Le schede sullo stesso sito condividono l’impostazione. Per ignorare nuovamente i collegamenti di spostamento, deselezionare **Mostra collegamenti di spostamento del sito** prima della successiva esecuzione.

L’impostazione non è disponibile durante l’esecuzione dei controlli di audit.

## Filtrare i risultati

Nella pagina dei dettagli, utilizza il filtro accanto all&#39;intestazione **Istanze** per mostrare solo alcune delle opportunità:

| Filtro | Opportunità visualizzate |
|---|---|
| **Tutti** (impostazione predefinita) | Ogni opportunità |
| **Interrotto** | Collegamenti interrotti e URL dell’editor |
| **Verifica necessaria** | Collegamenti non sicuri, frammenti mancanti e collegamenti non verificati |

Un collegamento `http://` non sicuro la cui versione `https://` è interrotta ha due opportunità sulla stessa scheda. **Interrotto** mostra solo l&#39;opportunità di collegamento interrotto e **Verifica necessaria** mostra solo l&#39;opportunità di collegamento non sicuro. Per ulteriori informazioni, vedere [Istanze filtro](../../audit-results.md#filter-instances).

## Limitazioni note

Il controllo di audit viene eseguito nell’Editor pagina di AEM Sites, in Adobe Managed Services (AMS) e nell’authoring basato su documenti tramite Sidekick. Attualmente non è disponibile nell’Editor universale.

## Come risolvere

Quando il controllo di audit individua le opportunità, ciascuna di esse descrive il problema e la modifica consigliata e identifica il collegamento coinvolto. Utilizza **Evidenzia a pagina** per passare direttamente al collegamento nel contenuto e utilizza la sezione **URL corrente** per copiare l&#39;URL o aprirlo in una nuova scheda in modo da poter confermare il problema. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

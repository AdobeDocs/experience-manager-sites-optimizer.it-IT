---
title: Verifica preliminare dei collegamenti esterni
description: Scopri il controllo dei collegamenti esterni in Verifica preliminare per AEM Sites Optimizer.
source-git-commit: 8a465f3ef54dbd295255f326eda2e8f37a114ace
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%
---
# Audit dei collegamenti esterni

Il controllo di **Collegamenti esterni** esamina i collegamenti presenti nella pagina che puntano ad altri siti. Il controllo di audit controlla ogni collegamento esterno dalla pagina che stai modificando e contrassegna quelli interrotti, non sicuri o che non è stato possibile verificare automaticamente.

## Perché è importante

Un collegamento esterno interrotto è un vicolo cieco per il lettore e un segnale ai motori di ricerca che la pagina non è ben mantenuta. I collegamenti esterni sono anche quelli sui quali si ha il minore controllo: l’altro sito può spostare, rinominare o rimuovere una pagina in qualsiasi momento e il collegamento smette di funzionare. Selezionandoli prima della pubblicazione, vengono rilevati i collegamenti che sono diventati obsoleti dalla prima aggiunta.

## Controlli dell’audit

L’audit segnala un’opportunità per ogni collegamento esterno che presenta uno dei seguenti problemi:

* **Collegamento interrotto:** impossibile raggiungere il collegamento oppure viene restituito un errore di tipo `Status 404`, `Status 410` o un errore del server `5xx`. Un collegamento che raggiunge l’errore dopo un reindirizzamento viene segnalato nello stesso modo. Anche un collegamento il cui sito non risponde affatto, ad esempio perché il dominio non esiste più, viene segnalato come interrotto.
* **Collegamento non sicuro:** il collegamento utilizza `http://` e il sito non lo reindirizza a `https://`. Un collegamento che inizia come `http://` ma viene reindirizzato a una pagina `https://` protetta non è contrassegnato. Aggiornare il collegamento per utilizzare `https://`.
* **Collegamento non verificato:** il sito ha risposto ma ha rifiutato il controllo automatico, ad esempio perché richiede l&#39;accesso (`Status 401` o `Status 403`), limita le richieste automatizzate (`Status 429`) o blocca i bot, come fanno alcuni social network. In questo modo viene segnalato anche un collegamento che reindirizza troppe volte da seguire. Questi collegamenti molto probabilmente funzionano in un browser, quindi la verifica preliminare non li segnala come interrotti. Ti chiede invece di aprire il collegamento, confermarlo autonomamente e segnalarlo con un impatto ridotto.

Un collegamento può essere sia non sicuro che interrotto, oppure non sicuro e non verificato, nel qual caso vengono segnalate entrambe le opportunità. Un collegamento che si risolve correttamente non viene contrassegnato, anche quando ci sono reindirizzamenti in arrivo.

## Controllo dei collegamenti

Un collegamento esterno è qualsiasi collegamento il cui host è diverso dalla pagina che si sta modificando. L&#39;host è il nome di dominio più qualsiasi porta non standard, ad esempio `:8443`. I sottodomini vengono conteggiati come host diversi, pertanto `blog.example.com` e `example.com` sono entrambi esterni a `www.example.com`. Non importa se il collegamento utilizza `http://` o `https://`. I collegamenti allo stesso host, inclusi `http://` collegamenti al tuo sito, sono invece coperti dal controllo di [Collegamenti interni](./internal-links.md). Collegamenti come `mailto:`, `tel:` e `javascript:` vengono ignorati.

Poiché il browser non è in grado di leggere lo stato di un collegamento presente in un altro sito, la verifica preliminare controlla i collegamenti esterni dai server di Adobe anziché dalla sessione di authoring. Ogni collegamento viene controllato una volta, anche se appare più volte sulla pagina o con ancoraggi diversi, ad esempio `#pricing` e `#features`. L’opportunità evidenzia la prima posizione in cui viene visualizzato il collegamento.

I collegamenti che AEM Link Checker ha già contrassegnato come non validi vengono inclusi nel controllo di audit, anche se l’editor rimuove il collegamento cliccabile dalla pagina. Vengono quindi ricontrollate anziché considerate attendibili, pertanto non viene segnalato un collegamento che da allora ha iniziato a funzionare.

## Limitazioni note

* **Numero di collegamenti:** vengono controllati fino a 50 collegamenti esterni distinti per pagina. I collegamenti oltre tale limite non vengono controllati.
* **Limite di tempo:** ogni collegamento ha un timeout di 10 secondi e l&#39;intero controllo ha un limite di tempo in modo che la verifica preliminare rimanga reattiva. Un sito che non risponde entro il timeout viene segnalato come interrotto. Nelle pagine con molti siti lenti, alcuni collegamenti potrebbero non essere sottoposti a check-in in una determinata esecuzione.
* **Indirizzi privati:** i collegamenti che vengono risolti in indirizzi di rete privati o interni, ad esempio un sito Intranet, non vengono controllati e non vengono segnalati.
* **Visualizzazione lato server:** poiché i collegamenti sono controllati dai server di Adobe, un sito che si comporta in modo diverso in base alla posizione, all&#39;accesso o al rilevamento di bot potrebbe restituire un risultato diverso da quello visualizzato nel browser. Tali collegamenti vengono in genere segnalati come **Collegamento non verificato** anziché interrotto.

## Come risolvere

Quando il controllo di audit individua le opportunità, ciascuna di esse descrive il problema e la modifica consigliata e identifica il collegamento coinvolto. Utilizza **Evidenzia a pagina** per passare direttamente al collegamento nel contenuto e aprire l&#39;URL in una nuova scheda per confermare il problema. Se il collegamento non funziona, aggiornalo nella nuova posizione della pagina o rimuovilo. Per un collegamento non verificato, verifica che si apra correttamente nel browser. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

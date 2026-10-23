---
title: Verifica preliminare dei collegamenti esterni
description: Scopri il controllo dei collegamenti esterni in Verifica preliminare per AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 59c097682899889aa2a5d76333f80cc58e28ff1e
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%
---
# Audit dei collegamenti esterni

Il controllo di **Collegamenti esterni** esamina i collegamenti presenti nella pagina che puntano ad altri siti. Il controllo di audit controlla ogni collegamento esterno dalla pagina che stai modificando e contrassegna quelli interrotti, non sicuri o che non è stato possibile verificare automaticamente.

## Perché è importante

Un collegamento esterno interrotto è un vicolo cieco per il lettore e un segnale ai motori di ricerca che la pagina non è ben mantenuta. I collegamenti esterni sono anche quelli sui quali si ha il minore controllo: l’altro sito può spostare, rinominare o rimuovere una pagina in qualsiasi momento e il collegamento smette di funzionare. Selezionandoli prima della pubblicazione, vengono rilevati i collegamenti che sono diventati obsoleti dalla prima aggiunta.

## Controlli dell’audit

L’audit segnala un’opportunità per ogni collegamento esterno che presenta uno dei seguenti problemi:

* **Collegamento interrotto:** il collegamento restituisce `Status 404` o `Status 410` oppure non è possibile raggiungere il relativo sito, ad esempio perché il dominio non esiste più. Un collegamento che raggiunge l’errore dopo un reindirizzamento viene segnalato nello stesso modo.
* **Collegamento non sicuro:** il collegamento utilizza `http://` e il sito non lo reindirizza a `https://`. Un collegamento che inizia come `http://` ma viene reindirizzato a una pagina `https://` protetta non è contrassegnato. Aggiornare il collegamento per utilizzare `https://`.
* **Collegamento non verificato:** Impossibile confermare il funzionamento del collegamento, ad esempio perché il sito richiede l&#39;accesso, blocca i controlli automatici, continua a restituire un errore del server, non risponde in tempo o reindirizza un numero eccessivo di volte. Alcuni social network, come LinkedIn e Instagram, segnalano le pagine mancanti ai controlli automatizzati, quindi anche gli errori di pagina mancanti da tali siti vengono segnalati come non verificati. Questi collegamenti molto probabilmente funzionano in un browser, quindi la verifica preliminare non li segnala come interrotti. Ti chiede invece di aprire il collegamento e di confermarlo tu stesso.

Un collegamento può essere sia non sicuro che interrotto, oppure non sicuro e non verificato, nel qual caso vengono segnalate entrambe le opportunità. Un collegamento che si risolve correttamente non viene contrassegnato, anche quando ci sono reindirizzamenti in arrivo.

## Collegamenti selezionati

Ogni collegamento esterno sulla pagina viene controllato. Un collegamento esterno è qualsiasi collegamento il cui host è diverso dalla pagina che si sta modificando. L&#39;host è il nome di dominio più qualsiasi porta non standard, ad esempio `:8443`. I sottodomini vengono conteggiati come host diversi, pertanto `blog.example.com` e `example.com` sono entrambi esterni a `www.example.com`. I collegamenti allo stesso host, inclusi `http://` collegamenti al tuo sito, sono invece coperti dal controllo di [Collegamenti interni](./internal-links.md). I collegamenti nella navigazione del sito sono sempre inclusi, perché l&#39;impostazione **Mostra collegamenti di navigazione del sito** si applica solo al controllo dei collegamenti interni. Collegamenti come `mailto:`, `tel:` e `javascript:` vengono ignorati.

Ogni collegamento viene segnalato una volta, anche se appare più volte sulla pagina o con ancoraggi diversi, ad esempio `#pricing` e `#features`. L’opportunità evidenzia la prima posizione in cui viene visualizzato il collegamento.

I collegamenti che AEM Link Checker ha già contrassegnato come non validi vengono inclusi nel controllo di audit, anche se l’editor rimuove il collegamento cliccabile dalla pagina. Vengono ricontrollate anziché considerate attendibili, pertanto non viene segnalato un collegamento che da allora ha iniziato a funzionare.

## Filtrare i risultati

Nella pagina dei dettagli, utilizza il filtro accanto all&#39;intestazione **Istanze** per mostrare solo alcune delle opportunità:

| Filtro | Opportunità visualizzate |
|---|---|
| **Tutti** (impostazione predefinita) | Ogni opportunità |
| **Interrotto** | Collegamenti interrotti |
| **Verifica necessaria** | Collegamenti non verificati e non sicuri |

Se un collegamento include più di un’opportunità, ad esempio un collegamento non sicuro anch’esso interrotto, ogni opportunità viene visualizzata sotto il proprio filtro. Per ulteriori informazioni, vedere [Istanze filtro](../../audit-results.md#filter-instances).

## Limitazioni note

* **Indirizzi privati:** i collegamenti a indirizzi di rete privati o interni, ad esempio un sito Intranet, non vengono controllati e non vengono segnalati.
* **Vista lato server:** Verifica preliminare controlla i collegamenti esterni dai server di Adobe anziché dal browser. Un sito che si comporta in modo diverso in base alla posizione, all’accesso o al rilevamento di bot può restituire un risultato diverso da quello visualizzato nel browser. Tali collegamenti vengono in genere segnalati come **Collegamento non verificato** anziché interrotto.

## Come risolvere

Quando il controllo di audit individua le opportunità, ciascuna di esse descrive il problema e la modifica consigliata e identifica il collegamento coinvolto. Utilizza **Evidenzia a pagina** per passare direttamente al collegamento nel contenuto e aprire l&#39;URL in una nuova scheda per confermare il problema. Se il collegamento non funziona, aggiornalo nella nuova posizione della pagina o rimuovilo. Per un collegamento non verificato, verifica che si apra correttamente nel browser. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

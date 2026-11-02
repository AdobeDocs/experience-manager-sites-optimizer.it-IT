---
title: Verifica preliminare dei collegamenti esterni
description: Scopri il controllo dei collegamenti esterni in Verifica preliminare per AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 12279cd1468a3442709cb73a8691922598a33dab
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%
---
# Audit dei collegamenti esterni

Il controllo di **Collegamenti esterni** esamina i collegamenti presenti nella pagina che puntano ad altri siti. Il controllo di audit controlla ogni collegamento esterno dalla pagina che stai modificando e contrassegna quelli interrotti, non sicuri o che non possono essere verificati automaticamente.

## Perché è importante

Un collegamento esterno interrotto è un vicolo cieco per il lettore e un segnale ai motori di ricerca che la pagina non è ben mantenuta. I collegamenti esterni sono anche quelli sui quali si ha il minore controllo: l’altro sito può spostare, rinominare o rimuovere una pagina in qualsiasi momento e il collegamento smette di funzionare. Selezionandoli prima della pubblicazione, vengono rilevati i collegamenti che sono diventati obsoleti dalla prima aggiunta.

## Controlli dell’audit

Il controllo di audit suddivide i problemi in tre gruppi:

* **Interrotto:** il collegamento non riesce per ogni visitatore al momento e non è previsto il ripristino.
* **Non verificato:** il collegamento non riesce per alcuni visitatori, potrebbe non riuscire solo temporaneamente o non può essere controllato.
* **Best practice:** il collegamento funziona, ma non deve essere creato in questo modo, ad esempio un collegamento `http://` non sicuro.

L’audit segnala un’opportunità per ogni collegamento esterno che presenta uno dei seguenti problemi:

* **Collegamento interrotto:** il collegamento non funziona per gli utenti che lo aprono. Verifica preliminare segnala un collegamento come interrotto quando:
  * impossibile raggiungere il sito, ad esempio perché il dominio non esiste più.
  * restituisce `Status 404` o `Status 410`.
  * restituisce `Status 405`, il che significa che il sito rifiuta le normali richieste di pagina.
  * reindirizza in loop o più di 20 volte. I browser utilizzano lo stesso limite e visualizzano un errore &quot;troppi reindirizzamenti&quot;.

  Un collegamento che raggiunge uno di questi errori dopo un reindirizzamento viene segnalato nello stesso modo.
* **Collegamento non sicuro:** il collegamento utilizza `http://` e la verifica preliminare non ha rilevato il reindirizzamento a `https://`, anche quando il sito non ha risposto. Un collegamento che inizia come `http://` ma viene reindirizzato a una pagina `https://` protetta non è contrassegnato. Aggiornare il collegamento per utilizzare `https://`.
* **Collegamento non verificato:** La verifica preliminare non è in grado di verificare se il collegamento funziona, pertanto richiede di aprire il collegamento e di controllarlo personalmente. L’opportunità spiega quale caso si applica:
  * **È necessario accedere:** il collegamento restituisce `Status 401`. I visitatori senza un account non possono aprirlo, quindi conferma che ciò è previsto.
  * **Blocca i controlli automatici:** il collegamento restituisce `Status 403` o `Status 429` oppure il sito blocca le richieste automatizzate in un altro modo, come fa LinkedIn. Verifica che il collegamento si apra in un browser.
  * **I siti social e con accesso limitato:** LinkedIn, Instagram, Facebook, X (Twitter), TikTok e Threads restituiscono errori fuorvianti a richieste anonime, pertanto un ciclo di `Status 404`, `Status 410`, `Status 405` o di reindirizzamento da questi siti viene segnalato come non verificato anziché interrotto.
  * **Errore del server:** il collegamento restituisce un errore del server (`Status 5xx`) che persiste quando la verifica preliminare lo verifica di nuovo. Prima di eseguire la verifica preliminare, esegue un nuovo tentativo prima di eseguire la segnalazione. L’errore può essere temporaneo, quindi conferma che il collegamento funzioni prima di pubblicarlo.
  * **Non disponibile per motivi legali:** il collegamento restituisce `Status 451` nell&#39;area Verifica preliminare da. Verifica che funzioni per il tuo pubblico.
  * **Nessuna risposta in tempo:** il sito non ha risposto in tempo, anche dopo un nuovo tentativo di verifica preliminare. Il sito potrebbe essere lento o temporaneamente inattivo.

Un collegamento può essere sia non sicuro che interrotto, oppure non sicuro e non verificato, nel qual caso vengono segnalate entrambe le opportunità. Una catena di reindirizzamento da sola non viene contrassegnata se raggiunge una pagina di lavoro entro 20 reindirizzamenti.

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
* **Limiti di tempo:** ogni collegamento ha un proprio limite di tempo, pertanto un sito lento non impedisce la verifica di altri collegamenti. Ogni collegamento sulla pagina ottiene un risultato. Un collegamento che non risponde in tempo, anche dopo un nuovo tentativo, viene segnalato come **Collegamento non verificato** anziché interrotto.
* **Domini esclusi:** la configurazione del sito può escludere dalla verifica domini specifici. I collegamenti a un dominio escluso o a uno dei suoi sottodomini non vengono controllati e non vengono segnalati.
* **Vista lato server:** Verifica preliminare controlla i collegamenti esterni dai server di Adobe anziché dal browser. Un sito che si comporta in modo diverso in base alla posizione, all’accesso o al rilevamento di bot può restituire un risultato diverso da quello visualizzato nel browser. Tali collegamenti vengono in genere segnalati come **Collegamento non verificato** anziché interrotto.

## Come risolvere

Quando il controllo di audit individua le opportunità, ciascuna di esse descrive il problema e la modifica consigliata e identifica il collegamento coinvolto. Utilizza **Evidenzia a pagina** per passare direttamente al collegamento nel contenuto e aprire l&#39;URL in una nuova scheda per confermare il problema. Quindi valuta l’opportunità:

* **Collegamento interrotto:** aggiorna il collegamento alla nuova posizione della pagina, oppure sostituiscilo o rimuovilo. Per un ciclo di reindirizzamento, contatta il proprietario dell’altro sito o collega a un’altra sorgente.
* **Collegamento non sicuro:** modifica il collegamento in modo da utilizzare `https://`, dopo aver confermato che la versione protetta funziona.
* **Collegamento non verificato:** apri il collegamento nel browser e conferma che venga visualizzata la pagina prevista. Per un collegamento che richiede l&#39;accesso, verifica che i lettori abbiano un account. Per un errore del server, controlla nuovamente il collegamento prima di pubblicarlo. Se il collegamento non funziona, consideralo come interrotto.

Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

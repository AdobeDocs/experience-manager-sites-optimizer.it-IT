---
title: Documentazione sull’opportunità Backlink interrotti
description: Scopri l’opportunità da cogliere in caso di backlink interrotti e come utilizzarla per migliorare l’acquisizione del traffico.
badgeTrafficAcquisition: label="Acquisizione traffico" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="Acquisizione traffico"
source-git-commit: 97e61d3061fb68225eece98ba0f94affb08be9e3
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 30%

---


# Opportunità Backlink interrotti

<!--![Broken backlinks opportunity](./assets/broken-backlinks/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483261/?captions=ita&learn=on&enablevpops)

L’opportunità di collegamenti interrotti identifica collegamenti esterni che indicano pagine inesistenti (404) sul sito. Questi collegamenti comportano una perdita di traffico da referral e un valore SEO ridotto, in quanto i motori di ricerca si basano su collegamenti retroversi per valutare la rilevanza e l’autorità. Questi problemi si verificano quando gli URL vengono modificati, il contenuto viene rimosso o le pagine non sono più disponibili senza reindirizzamenti appropriati. AEM Sites Optimizer identifica tutti i backlink interrotti, fornisce raccomandazioni IA specifiche e consente l’implementazione con un solo clic per correggerli, il tutto in un’unica vista centralizzata.

## Identificazione automatica

<!--![Auto-identify broken backlinks](./assets/broken-backlinks/auto-identify.png){align="center"}-->

AEM Sites Optimizer esegue una scansione continua delle origini dati esterne per rilevare i collegamenti retroversi che indicano pagine 404 inesistenti sul sito. I dati vengono aggregati da più origini, tra cui Google Search Console, [Telemetria operativa](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service) e piattaforme SEO di terze parti. L’opportunità di identificazione automatica identifica i domini esterni che si collegano agli URL interrotti e assegna loro una priorità in base all’impatto, inclusa l’autorità di dominio e le perdite previste di traffico e capitale netto di collegamento.

Questa opportunità elenca tutti i problemi identificati, inclusi i seguenti dettagli:

* **Dominio di riferimento e pagina** - La pagina o il dominio esterno che contiene il collegamento interrotto.
* **Priorità** - Alta, media o bassa che indica l&#39;impatto del collegamento interrotto sul processo SEO.
* **URL di destinazione interrotto**: l&#39;URL inesistente nel sito a cui si sta effettuando il collegamento.

## Suggerimento automatico

<!--![Auto-suggest broken backlinks](./assets/broken-backlinks/auto-suggest.png){align="center"}-->

Per ogni backlink danneggiato identificato, AEM Sites Optimizer consiglia la destinazione più appropriata per ripristinare il traffico e il valore SEO (Search Engine Optimization). Determina l’intento del backlink analizzando:

* Struttura URL e token
* Ancoraggio testo
* Titolo e contesto della pagina di riferimento

Questo intento viene confrontato con il contenuto del sito esistente per identificare la pagina di destinazione più rilevante. Ogni URL interrotto viene mappato su una pagina di sostituzione esatta o su una pertinente più vicina. Se non è possibile determinare una destinazione adatta, il problema viene evidenziato per la revisione manuale.

>[!BEGINTABS]

>[!TAB Base logica dell’intelligenza artificiale]

<!--![AI rationale on autosuggestion of broken backlinks](./assets/broken-backlinks/auto-suggest-ai-rationale.png){align="center"}-->

Seleziona l’icona **informazioni** per visualizzare la base logica usata dall’IA per l’URL suggerito. La logica spiega perché l’IA ritiene che l’URL suggerito sia il più adatto al collegamento interrotto. Questo può aiutarti a comprendere il processo decisionale dell’IA e a decidere in modo consapevole se accettare o meno il suggerimento.

>[!TAB Modifica URL di destinazione]

<!--![Edit suggested URL of broken backlinks](./assets/broken-backlinks/edit-target-url.png){align="center"}-->

Se non sei d’accordo con il suggerimento generato dall’IA, puoi modificare l’URL suggerito selezionando l’**icona di modifica**. La modifica consente di inserire manualmente l’URL che ritieni più adatto al collegamento interrotto. Sites Optimizer elenca anche eventuali altri URL sul sito che potrebbero essere adatti per il collegamento interrotto.

>[!TAB Ignorare le voci]

<!--![Ignore broken backlinks](./assets/broken-backlinks/ignore.png){align="center"}-->

Puoi scegliere di ignorare le voci con gli URL di destinazione interrotti. La selezione dell’![icona Elimina o Ignora](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg) rimuove il backlink interrotto dall’elenco delle opportunità. I backlink interrotti ignorati possono essere riattivati dalla scheda **Ignorate** nella parte superiore della pagina dell’opportunità.

>[!ENDTABS]

## Ottimizzazione automatica

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

Dopo aver esaminato e approvato i suggerimenti, è possibile fare clic su **Distribuisci ottimizzazione**. AEM Sites Optimizer applica quindi le correzioni nell’ambiente di authoring, in base al modo in cui i reindirizzamenti vengono gestiti all’interno dell’implementazione. L’autore di AEM può quindi pubblicare le modifiche da Content Management System (CMS).

A seconda della configurazione, le correzioni vengono applicate come modifiche al contenuto o al codice all’interno dei flussi di lavoro di distribuzione esistenti. Il processo di ottimizzazione include i seguenti passaggi:

* **Convalida** - Assicura che le modifiche funzionino come previsto e non introducano regressioni prima della distribuzione.
* **Distribuzione** - Applica le modifiche tramite i processi esistenti, ad esempio gli aggiornamenti del contenuto in AEM o la distribuzione del codice tramite pipeline CI/CD.
* **Controllo autorizzazioni** - Verifica che l&#39;utente disponga delle autorizzazioni appropriate per distribuire le modifiche. In caso contrario, vengono forniti output alternativi come elenchi di reindirizzamento scaricabili o patch di codice.

Questo processo garantisce che i reindirizzamenti siano implementati in modo accurato, convalidati prima del rilascio e allineati alle configurazioni e ai processi di governance esistenti.

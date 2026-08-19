---
title: Distribuzione nella documentazione di Author
description: Scopri come AEM Sites Optimizer distribuisce le ottimizzazioni selezionate nell’ambiente di authoring e come tracciarle successivamente.
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 1d55c607aab6c820d014b9a57bfae20b8170c672
workflow-type: tm+mt
source-wordcount: 245
ht-degree: 6%

---

# Distribuzione nella documentazione di authoring

<!--![Deploying to author](./assets/deploying-to-author/hero.png){align="center"}-->

Dopo che AEM Sites Optimizer identifica un’opportunità e consiglia le ottimizzazioni, puoi rivedere e distribuire le ottimizzazioni selezionate per ulteriori azioni.

## Implementa nell’istanza di authoring

Seleziona uno o più suggerimenti dall&#39;elenco di un&#39;opportunità, quindi fai clic su **Distribuisci all&#39;autore** per distribuire la selezione oppure su **Distribuisci tutto all&#39;autore** per distribuire tutti i suggerimenti disponibili contemporaneamente. AEM Sites Optimizer applica le ottimizzazioni selezionate solo nell’ambiente di authoring, non pubblica le modifiche al sito live. L&#39;autore di AEM può quindi rivedere e pubblicare le modifiche dal sistema di gestione dei contenuti (CMS), in linea con il flusso di lavoro [Ottimizzazione automatica](/help/documentation/opportunities/missing-alt-text.md#auto-optimize) di ogni opportunità.

Questa azione è disabilitata quando non disponi dell’autorizzazione per la distribuzione o quando il sito non è completamente configurato per la distribuzione (ad esempio, un archivio del codice non è ancora stato connesso). In entrambi i casi, Sites Optimizer spiega perché accanto al pulsante disabilitato.

## Tracciare le ottimizzazioni implementate

<!--![Deployed tab](./assets/deploying-to-author/deployed-tab.png){align="center"}-->

Dopo aver distribuito le ottimizzazioni selezionate, puoi gestirle e intraprendere i passaggi successivi dalla scheda **Implementato** nella pagina dei dettagli dell&#39;opportunità, insieme alle schede **Corrente** e **Ignorato**.

I meccanismi di implementazione specifici, tra cui il modo in cui gli aggiornamenti vengono applicati per Edge Delivery Services, AEM as a Cloud Service o Digital Asset Management, variano in base al tipo di opportunità. Per ulteriori dettagli, consulta la sezione **Ottimizzazione automatica** dell&#39;opportunità.

## Consulta anche

* [Opportunità Testo alternativo mancante](/help/documentation/opportunities/missing-alt-text.md#auto-optimize)
* [Opportunità dei web vitals di base](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [Opportunità Backlink interrotti](/help/documentation/opportunities/broken-backlinks.md#auto-optimize)

---
title: Documentazione sulla preparazione delle patch del codice
description: Scopri come AEM Sites Optimizer prepara le patch di codice per le correzioni Core Web Vitals e come tracciarle successivamente.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: a86d83ee226055e6401b13fd421b40d449b96fa8
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 2%

---

# Preparazione della documentazione delle patch del codice

<!--![Preparing code patches](./assets/preparing-code-patches/hero.png){align="center"}-->

Per l&#39;opportunità [Core Web Vitals](/help/documentation/opportunities/core-web-vitals.md), AEM Sites Optimizer genera correzioni a livello di codice per i problemi di prestazioni identificati. Queste correzioni vengono esaminate e preparate come patch di codice, anziché essere distribuite direttamente.

## Preparare le patch del codice

Seleziona uno o più problemi dall&#39;elenco di Core Web Vitals, quindi fai clic su **Prepara la patch del codice** per preparare la selezione oppure su **Prepara tutte le patch del codice** per preparare tutte le patch disponibili contemporaneamente. AEM Sites Optimizer crea un problema GitHub con etichetta per ciascuna correzione e apre automaticamente una richiesta di pull collegata con la modifica del codice, pronta per essere rivista, testata e unita dal team.

Questa azione viene disabilitata quando non si dispone dell&#39;autorizzazione per la preparazione delle patch del codice o quando il sito non è completamente configurato, ad esempio quando non è connesso alcun archivio del codice o la generazione delle patch è ancora in corso. In ogni caso, Sites Optimizer spiega perché accanto al pulsante disabilitato.

## Tracciare le patch del codice preparato

Dopo aver preparato le patch di codice, puoi gestirle e intraprendere i passaggi successivi dalla scheda **Implementato** nella pagina dei dettagli di Core Web Vitals, insieme alle schede **Corrente** e **Ignorato**. Lo stato di una patch indica se la richiesta pull è stata unita, non solo generata. Un problema si sposta su **Distribuito** solo dopo l&#39;effettiva unione della correzione alla base di codice.

## Consulta anche

* [Opportunità dei web vitals di base](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [Distribuzione nella documentazione di authoring](/help/documentation/opportunities/deploying-to-author.md)

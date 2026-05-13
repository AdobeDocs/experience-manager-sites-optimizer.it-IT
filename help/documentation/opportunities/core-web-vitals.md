---
title: Documentazione sull’opportunità Web vitals di base
description: Scopri l’opportunità da cogliere in caso di web vitals di base e come utilizzarla per migliorare l’acquisizione del traffico.
badgeSiteHealth: label="Integrità del sito" type="Caution" url="../../opportunity-types/site-health.md" tooltip="Integrità del sito"
TQID: https://experienceleague.adobe.com/3h-Xas767zUk-Sod7JEr9Lh767r5S3LKpbwJZFZU2kg
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 100%

---

# Opportunità dei web vitals di base

<!--![core web vitals opportunity](./assets/core-web-vitals/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483371/?learn=on&enablevpops)

L’opportunità relativa ai Core Web Vitals identifica le pagine del sito web con prestazioni inferiori, che influiscono sull’esperienza utente e sulle prestazioni della ricerca organica. Questi problemi possono derivare da fattori quali font personalizzati, dipendenze JavaScript non ottimizzate e script di terze parti. Core Web Vitals misura la velocità di caricamento dei contenuti, la stabilità del layout della pagina e la reattività della pagina alle interazioni dell’utente.

AEM Sites Optimizer rileva le pagine interessate da questi problemi, fornisce consigli IA specifici a livello di codice e applica le correzioni tramite i flussi di lavoro di sviluppo esistenti. Puoi analizzare solo le pagine che hanno almeno 1000 visualizzazioni.

## Identificazione automatica

<!--![Auto-identify core web vitals](./assets/core-web-vitals/auto-identify.png){align="center"}-->

AEM Sites Optimizer monitora continuamente le prestazioni del sito utilizzando la [Telemetria operativa](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service) per rilevare le regressioni nelle metriche di Core Web Vitals, ad esempio LCP (Largest Contentful Paint), CLS (Cumulative Layout Shift) e INP (Interaction to Next Paint). Utilizza i dati utente reali per identificare le regressioni delle prestazioni e assegnare la priorità ai problemi in base al relativo impatto sull’esperienza utente.

AEM Sites Optimizer visualizza l’elenco di tutti i problemi correnti, dettagliati per dispositivi mobili e desktop. La colonna **Pagina** indica la voce di pagina interessata e i problemi sono suddivisi per categoria in LCP, INP e CLS.

## Suggerimento automatico

<!--![Auto-suggest core web vitals opportunity](./assets/core-web-vitals/auto-suggest.png){align="center"}-->

Per ogni problema identificato, AEM Sites Optimizer genera consigli prescrittivi a livello di codice per migliorare le prestazioni di Core Web Vitals. Valuta l’implementazione sottostante accedendo all’archivio del codice. Questo consente al sistema di analizzare il modo in cui i componenti, gli script e gli stili vengono implementati e di identificare la causa principale dei problemi di prestazioni. In base a questa analisi, il sistema fornisce consigli mirati e genera patch di codice che specificano le modifiche necessarie per migliorare le prestazioni. Puoi rivedere ogni consiglio prima di essere applicato.

Quando fai clic sul pulsante dei suggerimenti, viene visualizzata una nuova finestra contenente le metriche delle prestazioni LCP, INP e CLS come categorie. Puoi passare da una categoria all’altra per visualizzare un elenco di problemi specifici. Ogni categoria può contenere diversi problemi, quindi assicurati di scorrere verso il basso per visualizzare l’elenco completo dei problemi e dei consigli. Inoltre, per ogni metrica sono disponibili due misuratori di prestazioni: per dispositivi mobili e per desktop.

## Ottimizzazione automatica

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

Una volta aver rivisto e approvato i consigli, puoi fare clic su **Implementa ottimizzazione**. AEM Sites Optimizer genera patch di codice in base ai problemi identificati e le rende disponibili tramite i processi di controllo delle versioni. Il processo di ottimizzazione include i seguenti passaggi:

* **Creazione del problema**: crea un problema GitHub con etichetta per ogni correzione, inclusa una descrizione chiara e l’URL interessato per la visibilità.
* **Consegna richiesta pull**: apre automaticamente una richiesta pull collegata con la correzione del codice esatta, pronta per la revisione, il test e l’unione.
* **Tracciamento dello stato**: tiene traccia di ogni correzione fino al completamento, contrassegnando i tentativi parziali o non riusciti per il follow-up.

Prima di rendere disponibili questi aggiornamenti, AEM Sites Optimizer esegue la convalida per garantire che le correzioni risolvano il problema di base e non introducano regressioni. Tutti gli aggiornamenti seguono le procedure di sviluppo standard, che richiedono revisione e approvazione prima di essere uniti alla produzione.

In questo modo le ottimizzazioni delle prestazioni sono accurate, convalidate e integrate nei processi di sviluppo e governance esistenti.

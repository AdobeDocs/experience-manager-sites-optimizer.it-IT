---
title: Documentazione sull’opportunità Web vitals di base
description: Scopri l’opportunità da cogliere in caso di web vitals di base e come utilizzarla per migliorare l’acquisizione del traffico.
badgeSiteHealth: label="Integrità del sito" type="Caution" url="../../opportunity-types/site-health.md" tooltip="Integrità del sito"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 99%

---


# Opportunità dei web vitals di base

![opportunità web vitals di base](./assets/core-web-vitals/hero.png){align="center"}

L’opportunità dei web vitals di base identifica i problemi che possono compromettere l’esperienza utente e le prestazioni di ricerca organica delle pagine web. Questi problemi derivano da un’ampia gamma di fattori come: font personalizzati, dipendenze JavaScript non ottimizzate, script di terze parti e così via. L’opportunità dei web vitals di base indica questi elementi difettosi e suggerisce correzioni che possono aumentare le prestazioni della pagina web. È possibile analizzare solo le pagine che hanno almeno 1000 visualizzazioni.

Per iniziare, l’opportunità dei web vitals di base mostra un riepilogo nella parte superiore della pagina, inclusa una sintesi del problema e il relativo impatto sul sito e sull’azienda.

* **Perdita traffico prevista**: perdita di traffico stimata a causa di web vitals di base al di sotto delle soglie di prestazioni.
* **Valore traffico previsto**: valore stimato del traffico perso.

## Identificazione automatica

![Identificazione automatica dei web vitals di base](./assets/core-web-vitals/auto-identify.png){align="center"}

Nella parte inferiore della pagina è disponibile un elenco di tutti i problemi correnti raggruppati come:

* **Problemi relativi ai dispositivi mobili**: elenco di problemi che interessano la versione per dispositivi mobili della pagina.
* **Problemi relativi al desktop**: elenco di problemi relativi alla versione desktop della pagina.

Ogni problema viene visualizzato in una tabella, con la colonna **Pagina** che identifica la voce della pagina interessata.

Inoltre, questi problemi sono raggruppati anche in base alle metriche standard delle prestazioni del rapporto Web vitals di base: Largest Contentful Paint **LCP**, Interazione con l’elemento successivo **INP** e Spostamento layout cumulativo **CLS**.

## Suggerimento automatico

![Suggerimento automatico per l’opportunità Web vitals di base](./assets/core-web-vitals/auto-suggest.png){align="center"}

L’opportunità dei web vitals di base fornisce suggerimenti di correzione generati dall’intelligenza artificiale. Quando fai clic sul pulsante dei suggerimenti, viene visualizzata una nuova finestra contenente le metriche delle prestazioni **LCP**, **INP** e **CLS** come categorie. Puoi passare da una categoria all’altra per visualizzare un elenco di problemi specifici.

Ogni categoria può contenere diversi problemi, quindi accertati di scorrere verso il basso per visualizzare l’elenco completo dei problemi e dei consigli.  Inoltre, per ogni metrica sono disponibili due misuratori di prestazioni: per dispositivi mobili e per desktop.

## Ottimizzazione automatica

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Ottimizzazione automatica dell’opportunità dei web vitals di base](./assets/core-web-vitals/auto-optimize.png){align="center"}

Sites Optimizer Ultimate offre la possibilità di distribuire l’ottimizzazione automatica per i problemi rilevati dall’opportunità dei web vitals di base. <!--- TBD-need more in-depth and opportunity specific information here. What does the auto-optimization do?-->

>[!BEGINTABS]

>[!TAB Distribuisci ottimizzazione]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Richiedi approvazione]

{{auto-optimize-request-approval}}

>[!ENDTABS]


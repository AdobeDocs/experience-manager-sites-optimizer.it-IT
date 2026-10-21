---
title: Eseguire audit nella verifica preliminare
description: Scopri come avviare un audit di verifica preliminare sulla pagina.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: ae16300fdfd525dc5efead2f165d5a238b5ea6e1
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 17%
---

# Audit nella verifica preliminare

La verifica preliminare esegue l’audit della pagina per identificare le opportunità di miglioramento dei contenuti prima della pubblicazione. A differenza di una scansione automatica, puoi scegliere quando eseguire i controlli di audit, in modo da poter analizzare una pagina ogni volta che sei pronto.

![La schermata di destinazione della verifica preliminare con il pulsante Analizza pagina](./assets/audits/hero.png){align="center"}

Per eseguire gli audit di verifica preliminare per una pagina:

1. Apri la pagina di cui eseguire l’audit nell’[ambiente di authoring](./access-preflight.md) (editor universale, authoring basato su documenti o Editor pagina per AEM Sites).
1. Apri il [pannello Verifica preliminare](./access-preflight.md). Verrà visualizzata la schermata di destinazione **Esegui verifica di preparazione alle prestazioni**.
1. Se necessario, apri **Impostazioni** (icona a forma di ingranaggio) per includere i collegamenti di navigazione del sito nel controllo dei collegamenti interni. Questa impostazione è disattivata per impostazione predefinita e non è disponibile nell’Editor universale. A seconda dell&#39;ambiente, **Impostazioni** viene visualizzato nell&#39;intestazione o in **Altre azioni** (**...**). Vedi [Includi collegamenti di navigazione del sito](./opportunities/seo/internal-links.md#include-site-navigation-links).
1. Selezionare **Analizza pagina**. Verifica preliminare esegue tutti i controlli di audit nella pagina corrente e apre il dashboard di preparazione, in cui viene visualizzata la percentuale di controlli superati e le opportunità trovate, raggruppate per categoria.

Per comprendere i risultati dell&#39;anteprima e identificare le opportunità di ottimizzazione, vedere [Risultati dell&#39;audit in Verifica preliminare](./audit-results.md).

## Utilizzare il pulsante Verifica preliminare integrato

Se nell&#39;ambiente di authoring è in esecuzione [AEM 2026.7.0 (versione 27083)](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/release-notes/maintenance/2026/2026-7-0#release-27083) o successiva, la verifica preliminare è incorporata nella barra degli strumenti dell&#39;Editor pagine di AEM Sites. Seleziona l&#39;icona **Verifica preliminare** (pulsante Riproduci) per aprire il pannello per la pagina corrente, quindi seleziona **Analizza pagina** per eseguire i controlli di audit.

>[!VIDEO](https://video.tv.adobe.com/v/3496629?learn=on&enablevpops)

## Continua una sessione precedente

La verifica preliminare ricorda l&#39;esecuzione più recente, quindi non è necessario eseguire nuovamente i controlli se si esce e si torna indietro.

* Se riapri il pannello Verifica preliminare nella **stessa scheda del browser**, anche dopo un aggiornamento, la verifica preliminare carica automaticamente i risultati dell&#39;ultima esecuzione.
* Se si restituisce **in una nuova scheda o dopo aver chiuso il browser**, nella schermata di destinazione viene visualizzato un pulsante **Continua ultima sessione** accanto a **Analizza pagina**. Seleziona **Continua ultima sessione** per ricaricare i risultati più recenti, oppure seleziona **Analizza pagina** per avviare una nuova esecuzione.

La verifica preliminare tiene traccia separatamente dell&#39;ultima esecuzione per ogni pagina, quindi **Continua ultima sessione** ricarica sempre l&#39;ultima esecuzione per la pagina in cui ti trovi.

Quando ricarichi un&#39;esecuzione precedente, l&#39;intestazione mostra quanto tempo è trascorso dall&#39;esecuzione, ad esempio *2 minuti fa* o *ieri*, in modo da poter verificare immediatamente l&#39;attualità dei risultati. L’etichetta viene aggiornata con il passare del tempo e rimane visibile mentre ci si sposta tra la dashboard di preparazione e le pagine di dettaglio del controllo di audit.

Al termine della visualizzazione dei controlli e dei risultati, selezionare **Rianalizza** nella barra degli strumenti per ignorare i risultati ed eseguire di nuovo ogni controllo di audit. Vedi [Risultati dell&#39;audit in Verifica preliminare](./audit-results.md#toolbar).

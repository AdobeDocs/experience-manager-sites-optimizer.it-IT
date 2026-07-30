---
title: Risultati dell’audit della verifica preliminare
description: Scopri come interpretare i risultati dell’audit della verifica preliminare, il misuratore di fattibilità e le categorie di audit e come passare alle opportunità nell’anteprima.
source-git-commit: 9989144c429da97e3ea303c0c8caf5a9b38e2634
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 4%

---


# Risultati dell’audit della verifica preliminare

Al termine dei controlli, Verifica preliminare visualizza i risultati nel dashboard di preparazione. Il dashboard mostra un misuratore di fattibilità complessivo e le opportunità trovate, raggruppate per categoria di audit. All’interno di ciascuna categoria, i singoli audit identificano elementi specifici da esaminare o correggere.

## Barra degli strumenti

La barra degli strumenti nella parte superiore del dashboard di preparazione fornisce le azioni per l’esecuzione corrente. Le **altre azioni** (**...**) offerte di menu:

* **Rianalizza** - Avvia una nuova esecuzione di controllo nella pagina corrente. La funzione Rianalizza elimina sempre i risultati visualizzati ed esegue di nuovo ogni controllo di audit, quindi utilizzala ogni volta che desideri ottenere nuovi risultati, ad esempio dopo aver modificato la pagina.
* **Esporta (CSV)** - Scarica i risultati correnti come file CSV, incluse le opportunità e i metadati dell&#39;esecuzione di controllo corrente.

## Misuratore di fattibilità

Nella parte superiore del dashboard, il misuratore di prontezza riflette i risultati complessivi del controllo di audit. Mostra un punteggio di preparazione in percentuale, basato sulla percentuale di audit conclusi senza opportunità, insieme al numero totale di opportunità trovate in tutti gli audit. Il misuratore di prontezza consente di misurare lo stato complessivo della pagina in una panoramica.

![Misuratore di fattibilità e categorie di controllo nel dashboard Verifica preliminare](./assets/overview/hero.png){align="center"}

Mentre i controlli sono ancora in corso, il misuratore di prontezza mostra una barra di avanzamento con uno stato breve sotto di esso che mostra il passaggio corrente. Al termine degli audit, il contatore mostra la percentuale finale di preparazione e il conteggio delle opportunità.

## Categorie di audit

Verifica preliminare raggruppa i controlli di audit correlati in categorie, ad esempio **SEO** e **Accessibilità**. Ogni categoria viene visualizzata come una scheda che mostra il numero di opportunità trovate o indica che tutti i controlli di audit sono stati superati senza opportunità.

Espandi una categoria per visualizzare i singoli controlli di audit. Ogni audit mostra se ha superato o trovato le opportunità, una breve descrizione e un conteggio delle opportunità trovate. Seleziona un controllo di audit che ha trovato opportunità per aprire la relativa pagina di dettagli.

Per l&#39;elenco completo delle categorie di controllo e dei controlli di audit in ognuna, vedere [Categorie di controllo verifica preliminare](./overview.md#preflight-audit-categories).

## Dettagli dell’opportunità

La pagina dei dettagli mostra le opportunità trovate dal controllo di audit selezionato. Quando lo stesso problema si verifica in più posizioni, ogni occorrenza viene definita istanza. Utilizza il Navigator (**Istanza precedente** e **Istanza successiva**) per esaminarle; mostra la tua posizione, ad esempio *1 di 5 istanze trovate*.

![Pagina dei dettagli per un controllo di audit, che mostra un&#39;opportunità e il relativo suggerimento](./assets/audit-results/audit-detail.png){align="center"}

Ogni opportunità include:

* Un badge di gravità o di impatto che indica l’importanza dell’opportunità.
* Dettagli sull’opportunità, ad esempio una descrizione del problema, un consiglio e, per l’accessibilità, la regola WCAG correlata e il livello di conformità.
* Sezione **Element** che mostra l&#39;elemento interessato nella pagina, con un pulsante **Evidenzia a pagina**.
* Una sezione **Suggestion** con una correzione consigliata. Quando il suggerimento è generato dall’intelligenza artificiale, viene contrassegnato come suggerimento generato dall’intelligenza artificiale e può includere una breve motivazione che spiega la correzione suggerita.

## Evidenziazione sulla pagina

Al termine dei controlli di audit, puoi individuare e comprendere rapidamente un’opportunità evidenziandola direttamente sulla pagina.

La verifica preliminare evidenzia l’elemento interessato nel contesto, collegando il risultato nel pannello alla posizione esatta nel contenuto. In questo modo puoi rivedere e risolvere con semplicità le opportunità senza effettuare ricerche manuali nella pagina.

1. Aprire il pannello Verifica preliminare nel contesto della pagina da controllare e selezionare **Analizza pagina** per eseguire i controlli di audit.
1. Seleziona un controllo di audit dal dashboard di preparazione, quindi seleziona un’opportunità da rivedere.
1. Seleziona **Evidenzia a pagina**. L’anteprima scorre automaticamente fino all’area rilevante ed evidenzia l’elemento corrispondente, in modo da poter identificare e ottimizzare facilmente l’opportunità nel contesto.

## ID processo

Ogni esecuzione di verifica preliminare ha un ID di processo univoco, visualizzato nella parte inferiore del pannello. Questa funzione è utile soprattutto quando un amministratore risolve un problema relativo a un’esecuzione specifica. Passa il puntatore del mouse sull’ID e seleziona l’icona Copia a destra; l’ID viene copiato negli Appunti e viene visualizzato un messaggio di conferma. Includi questo ID quando segnali un problema.

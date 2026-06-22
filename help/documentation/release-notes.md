---
title: Note sulla versione
description: Scopri le nuove funzioni, i miglioramenti e le correzioni di bug più recenti in Adobe Experience Manager Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: d5cc34fd40395fc13ce3554a0b80c0216d859157
workflow-type: tm+mt
source-wordcount: 1471
ht-degree: 2%

---


# Note sulla versione

In questa pagina sono documentati gli ultimi aggiornamenti, le nuove funzioni e i miglioramenti introdotti in Adobe Experience Manager Sites Optimizer.

## 11-22 maggio 2026

### Nuove funzioni

- **Rapporto avvisi sito**: un nuovo rapporto di 90 giorni sugli avvisi sito fornisce una visualizzazione trimestrale dello stato del sito, utilizzando blocchi giornalieri codificati a colori per evidenziare periodi di avvisi elevati in modo da poter identificare e analizzare rapidamente le tendenze nel tempo.
- **Onboarding della telemetria operativa**: i siti che non hanno ancora connesso i dati di telemetria operativa ora ricevono un banner permanente nella home page e una finestra di dialogo di onboarding guidata per completare la configurazione, garantendo la piena visibilità delle prestazioni dell&#39;utente reale.
- **Testo alt.: Consapevolezza di Multi-Site Manager**: durante la generazione di correzioni di testo alt per i siti che utilizzano AEM Multi-Site Manager o Copia per lingua, Sites Optimizer ora controlla se le correzioni possono essere applicate in modo sicuro a ogni variante di lingua prima di suggerirle.

### Miglioramenti

- **Precisione testo alternativo**: i suggerimenti di testo alternativo ora derivano dal segnale di controllo più recente e i problemi rilevati nuovamente vengono evidenziati sia nelle schede Problemi correnti che Distribuiti per ottenere un quadro completo.

### Correzioni di bug

- Lo stato del pulsante Distribuisci ora riflette correttamente la possibilità di distribuire una correzione.
- Il tema scuro viene ora applicato correttamente all’aggiornamento della pagina.
- I report mostrano le date nelle impostazioni internazionali dell&#39;utente.
- È ora possibile configurare in modo indipendente le preferenze internazionali per la lingua e il formato numero/data.
- Il testo alternativo immagine interrotto è ora accessibile agli assistenti vocali.

## 21 aprile - 10 maggio 2026

### Nuove funzioni

- **Nessuno stato di onboarding del sito**: i clienti che non hanno ancora aggiunto un sito ricevono ora un prompt chiaro e actionable nella home page per iniziare rapidamente.
- **Documentazione nel Centro assistenza**: la documentazione di AEM Sites Optimizer su Experience League è ora accessibile direttamente dal Centro assistenza in-app, senza uscire dal prodotto.

### Correzioni di bug

- Nei siti senza suggerimenti attivi viene ora visualizzata correttamente la finestra di dialogo Azione richiesta.
- I suggerimenti saltati vengono ora visualizzati come previsto nella scheda Ignorato.
- I menu a discesa del selettore del traffico a pagamento non troncano più il testo tradotto.
- Il selettore pagina mappa del sito ora è ridimensionato correttamente.

## 13 marzo - 20 aprile 2026

### Nuove funzioni

- **Onboarding delle versioni di prova**: i nuovi utenti delle versioni di prova hanno ora un flusso di configurazione guidato: immetti il dominio, attendi l&#39;analisi, quindi esplora le prime opportunità, nessuna configurazione necessaria per iniziare.
- **Pagina Opportunità di prova** - Gli utenti di prova possono cercare, ordinare e filtrare le opportunità, con tre suggerimenti sbloccati e rimanenti visualizzati in un&#39;anteprima bloccata con un prompt di aggiornamento.
- **Avanzamento ottimizzazione mensile**: una barra di avanzamento nella home page tiene traccia di quante azioni di ottimizzazione sono state eseguite in questo mese, consentendoti di mantenere gli obiettivi di integrità del sito.
- **Controlla URL di destinazione**: in Impostazioni è ora possibile specificare fino a 100 URL personalizzati per garantire che tali pagine siano sempre incluse nei controlli di audit.
- **Configurazione tipo di consegna**: le impostazioni ora consentono di specificare il tipo di consegna del sito (Edge Delivery Services, AEM Cloud Service o AEM Managed Services) e di connettere il provider di contenuti.
- **Core Web Vitals Redesign**: l&#39;opportunità Core Web Vitals è stata riprogettata con il collegamento Jira, il download CSV e il supporto a selezione multipla per le azioni batch.
- **Tabella unificata backlink interrotti**: i backlink interrotti da tutte le origini ora vengono visualizzati in un&#39;unica tabella unificata, con la possibilità di esportare direttamente le regole di reindirizzamento CDN.
- **Nessun CTA sopra il Piega: distribuisci all&#39;autore** — Correzioni per l&#39;opportunità No CTA sopra il Piega ora può essere distribuita direttamente all&#39;autore AEM.
- **Distribuzione automatica Forms**: le correzioni delle opportunità Forms possono ora essere distribuite direttamente in AEM Author.
- **Supporto di AEM Multi-Site Manager**: le opportunità che interessano più copie in lingua di un sito ora indicano il sito principale in cui è stata applicata la correzione, utilizzando una colonna &quot;Corretto a&quot;.
- **Ignora correzioni non riuscite** - È ora possibile ignorare singole correzioni che non sono riuscite a distribuire, mantenendo il flusso di lavoro sbloccato.
- **Apri in AEM Editor**: i suggerimenti di opportunità ora includono un collegamento diretto per aprire la pagina interessata nell&#39;editor visivo di AEM per le modifiche in linea rapide.

## 28 febbraio - 13 marzo 2026

### Nuove funzioni

- **Opportunità di mancata corrispondenza intento annuncio**: un nuovo tipo di opportunità identifica le pagine di destinazione del traffico a pagamento che non vengono convertite, presentando il tasso di mancato recapito, il costo per clic e le metriche del traffico per dare priorità ai miglioramenti della pagina di destinazione.
- **Nessun CTA sopra il riquadro**: questa opportunità è ora un tipo di prima classe dedicato con la propria pagina dei dettagli e i filtri, facilitando il tracciamento e l&#39;assegnazione di priorità ai miglioramenti delle conversioni.
- **Suggerimenti URL sitemap**. L&#39;opportunità Sitemap ora suggerisce URL sostitutivi per le pagine che restituiscono errori 404, semplificando la correzione delle voci di sitemap interrotte.
- **Backlink interrotti riprogettati**: la pagina dei dettagli Backlink interrotti è stata riprogettata per migliorarne la chiarezza e l&#39;usabilità.

### Miglioramenti

- **Pagine principali per la ricerca organica V2**: i dati sul traffico organico ora provengono da un set di dati Ahrefs di 30 giorni, che fornisce informazioni più complete e actionable sulle prestazioni della ricerca.
- **Vulnerabilità sicurezza: albero delle dipendenze** — I dettagli delle vulnerabilità di sicurezza ora includono una visualizzazione ad albero delle dipendenze che consente di comprendere l&#39;impatto completo di una vulnerabilità nel progetto.

## 14-27 febbraio 2026

### Nuove funzioni

- **Pagine principali per la ricerca organica**: Site Health Monitor ora include una scheda dedicata che mostra le pagine principali del traffico organico del sito, fornendo visibilità su quale contenuto determina il maggior traffico di ricerca.
- **Correzione automatica testo alternativo V2**: prima di distribuire una correzione di testo alternativo, è possibile eseguire una valutazione preliminare di &quot;Correggibilità del controllo&quot; per verificare che la correzione possa essere applicata correttamente al contenuto.
- **Visualizzazione distribuita per testo alternativo**: le correzioni di testo alternativo vengono ora visualizzate in una scheda Distribuito, fornendo una cronologia completa dei miglioramenti dell&#39;accessibilità e dei problemi in sospeso.
- **Gate di distribuzione organizzazione esterna**: durante la distribuzione di correzioni in un sito gestito esternamente, è ora necessario un passaggio di conferma esplicito per evitare modifiche accidentali.

### Miglioramenti

- **Esenzioni URL tag Meta**: è ora possibile escludere URL specifici dalla convalida dei tag Meta tramite la configurazione, riducendo i falsi positivi per titoli intenzionalmente brevi o non standard.
- **Filtro URL avanzato**: gli elenchi di opportunità ora supportano la corrispondenza dei prefissi di route secondaria quando si filtra per URL, semplificando l&#39;attivazione di sezioni specifiche del sito.
- **Grafici di tendenza migliorati** — I grafici di tendenza del traffico ora gestiscono correttamente i dati su base annua, rimuovendo i cali fuorvianti ai limiti dell&#39;anno.

## 6-13 febbraio 2026

### Nuove funzioni

- **Modalità manutenzione**: Sites Optimizer gestisce le finestre di manutenzione pianificate in modo corretto, visualizzando un messaggio di stato chiaro anziché dati incompleti o fuorvianti durante i periodi di inattività.
- **Visualizzazione distribuita per i collegamenti interrotti** — I collegamenti fissi vengono ora tracciati in una scheda Distribuito, raggruppati per data in modo da poter visualizzare immediatamente la cronologia degli aggiornamenti.
- **Nessun CTA al di sopra dell&#39;opportunità di piegatura**: un nuovo tipo di opportunità espone le pagine in cui non è visibile un call-to-action chiaro al di sopra della piega, consentendo di identificare e migliorare le pagine con un basso potenziale di conversione.
- **Integrazione Jira per l&#39;accessibilità e il contrasto dei colori**: le opportunità di accessibilità per Forms e il contrasto dei colori possono ora essere collegate direttamente ai ticket Jira per il tracciamento semplificato dei problemi all&#39;interno del flusso di lavoro esistente.

### Miglioramenti

- **Visualizzazioni distribuite per tag e sicurezza di Meta**: i tag di Meta e le opportunità di sicurezza ora includono schede distribuite con raggruppamenti di date, coerenti con altri tipi di opportunità.
- **Tracciamento distribuzione testo alternativo**: &quot;Contrassegna come distribuito&quot; è ora disponibile per le correzioni di testo alternativo e il testo alternativo modificato manualmente viene mantenuto durante le esecuzioni di rianalisi.

## 26 gennaio - 6 febbraio 2026

### Nuove funzioni

- **Visualizzazione distribuita per Canonical e Hreflang** — Le modifiche alle opportunità Canonical e Hreflang ora sono raggruppate per data di distribuzione in una scheda Distribuito, che fornisce una chiara cronologia di ciò che è stato corretto e quando.
- **Esportazione CSV**: è ora possibile esportare i dati delle opportunità per High Organic Low CTR e Forms in CSV per l&#39;analisi offline e il reporting.
- **Opportunità preferite**: avvia qualsiasi opportunità dalla relativa intestazione per aggiungerla ai preferiti, velocizzando il passaggio alle opportunità su cui stai lavorando attivamente.
- **Visualizzazione distribuita per le catene di reindirizzamento** — Le correzioni apportate alle catene di reindirizzamento ora possono essere contrassegnate come distribuite direttamente dalla pagina dei dettagli.

### Miglioramenti

- **Stime di costo migliorate per il banner dei cookie** — I calcoli dei costi per l&#39;opportunità del banner dei cookie sono stati perfezionati per una maggiore precisione.

## 16-23 gennaio 2026

### Nuove funzioni

- **Monitoraggio integrità sito (disponibilità generale)**: Monitoraggio integrità sito è ora disponibile per tutti i clienti, fornendo una visualizzazione continua dell&#39;integrità delle prestazioni del sito. I nuovi siti vengono configurati automaticamente al momento dell’onboarding.
- **Supporto del sito secondario**: i siti con ambito di percorsi secondari URL specifici sono ora completamente supportati in Monitoraggio integrità sito.

### Miglioramenti

- **Avvisi di disponibilità dei dati**: le opportunità di traffico a pagamento con meno di 1.000 pagine visualizzano ora un avviso di sufficienza dei dati, che consente di concentrare le attività di ottimizzazione laddove i dati sul traffico sono statisticamente significativi.
- **Convalida titolo Meta flessibile**: il requisito minimo di caratteri per i metatitoli è stato ridotto, offrendo maggiore flessibilità nella creazione di titoli di pagina concisi.
- **Finestra di dialogo Novità localizzata**: la finestra di dialogo degli annunci delle funzionalità in-app ora viene visualizzata nella lingua preferita.
- **Badge pubblicato** — Le varianti nell&#39;opportunità High Organic Low CTR distribuite ora mostrano un badge &quot;Published&quot;, che semplifica la distinzione tra modifiche attive e in sospeso.
- **Collegamenti richiesta pull in Accesso facilitato**: la scheda Distribuito dell&#39;opportunità di accesso facilitato ora mostra l&#39;URL della richiesta pull associato per ogni correzione, semplificando la traccia delle modifiche alla cronologia del controllo del codice sorgente.

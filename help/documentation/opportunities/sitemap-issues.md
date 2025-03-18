---
title: Documentazione sull’opportunità dei problemi di Sitemap
description: Scopri l’opportunità di problemi con sitemap e come utilizzarla per migliorare l’acquisizione del traffico.
badgeTrafficAcquisition: label="Acquisizione traffico" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="Acquisizione traffico"
source-git-commit: d812a49e4b49d329717586b9f3c7a235aff3e69a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---


# Opportunità problemi Sitemap

![Opportunità problemi mappa del sito](./assets/sitemap-issues/hero.png){align="center"}

Una mappa del sito completa e accurata consente ai motori di ricerca di esaminare e indicizzare in modo efficiente le pagine del sito web, garantendo una migliore visibilità nei risultati di ricerca. L’opportunità di sitemap identifica potenziali problemi con la sitemap. La risoluzione di questo problema può migliorare notevolmente l’indicizzazione dei motori di ricerca e la reperibilità dei contenuti sul sito.

Nella parte superiore della pagina viene visualizzato un riepilogo che include una sintesi del problema e del relativo impatto sul sito e sull’azienda.

* **Traffico previsto perso** - Perdita di traffico stimata a causa di problemi di sitemap.
* **Valore traffico previsto** - Valore stimato del traffico perso.

## Identificazione automatica

I problemi di Sitemap possono essere filtrati utilizzando i seguenti criteri:

* **Mappa del sito con problemi** - L&#39;URL della mappa del sito analizzato contiene potenziali problemi.
* **Tipo di problema** - Tipo di problema identificato in sitemap:
   * **Errori client** - Voci che non restituiscono una risposta `200 Success`.
   * **Reindirizzamenti** - Reindirizzamenti errati o non configurati correttamente.

>[!BEGINTABS]

>[!TAB Errori client]

![Errori client di sitemap con identificazione automatica](./assets/sitemap-issues/auto-identify-client-errors.png){align="center"}

Se gli URL nella mappa del sito restituiscono questi, i motori di ricerca potrebbero presumere che la mappa del sito sia obsoleta o che le pagine siano state rimosse per errore. Il client indica che la richiesta del client (browser o crawler) non è valida. Quelli comuni includono:

* **404 Non trovato** - La pagina richiesta non esiste.
* **403 Non consentito** - Il server nega l&#39;accesso alla pagina richiesta.
* **410 Non più disponibile** - La pagina è stata rimossa intenzionalmente e non verrà restituita.
* **401 Non autorizzato** - L&#39;autenticazione è obbligatoria ma non è stata specificata.

Questi errori possono danneggiare l&#39;ottimizzazione SEO, soprattutto se le pagine importanti restituiscono **404 o 410**, in quanto i motori di ricerca potrebbero deindicizzarle.

Ogni problema viene visualizzato in una tabella, con la colonna **Pagina** che identifica la voce di sitemap interessata:

* **Pagina** - URL della voce sitemap con un problema.

>[!TAB Reindirizzamenti]

![Errori client di sitemap con identificazione automatica](./assets/sitemap-issues/auto-identify-redirects.png){align="center"}

Le mappe del sito devono includere solo URL di destinazione finali, non URL di reindirizzamento. I reindirizzamenti hanno lo scopo di guidare gli utenti e i crawler alla posizione corretta, ma possono causare problemi se non configurati correttamente:

* **302 trovato (reindirizzamento temporaneo)** - Può causare problemi SEO se utilizzato per errore al posto di **301**.
* **307 Reindirizzamento temporaneo** - Simile a 302 ma che mantiene il metodo HTTP.
* **Cicli di reindirizzamento**: quando una pagina torna a se stessa o crea un ciclo infinito.
* **Reindirizzamenti interrotti** - Quando un reindirizzamento conduce a una pagina inesistente o 4xx.

Ogni problema viene visualizzato in una tabella, con la colonna **Pagina** che identifica la voce di sitemap interessata:

* **Pagina** - URL della voce sitemap con un problema.

>[!ENDTABS]

## Suggerimento automatico

Ogni problema di sitemap [ che soddisfa i criteri di filtro](#auto-identify) è elencato in una tabella con le colonne seguenti:

* **Pagina** - URL della voce sitemap con un problema.
* **Suggerimento**: la correzione consigliata per il problema.

I suggerimenti in genere includono un percorso del sito aggiornato per correggere la voce sitemap. In alcuni casi, possono anche fornire istruzioni più dettagliate, come ad esempio specificare il target di reindirizzamento corretto.

## Ottimizza automaticamente [!BADGE Ultimate]{type=Positive tooltip="Ultimate"}


![Problemi relativi all&#39;ottimizzazione automatica di Sitemap](./assets/sitemap-issues/auto-optimize.png){align="center"}

Sites Optimizer Ultimate aggiunge la possibilità di distribuire ottimizzazioni automatiche delle sitemap.

>[!BEGINTABS]

>[!TAB Ottimizzazione distribuzione]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Richiedi approvazione]

{{auto-optimize-request-approval}}

>[!ENDTABS]

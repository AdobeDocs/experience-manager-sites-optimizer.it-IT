---
title: Documentazione sull’opportunità di configurazione CORS
description: Scopri l’opportunità di configurazione CORS e come identificare e correggere le vulnerabilità di sicurezza del sito.
badgeSecurityPosture: label="Livello di sicurezza" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Livello di sicurezza"
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---


# Opportunità di configurazione CORS

![opportunità di configurazione CORS](./assets/cors-configuration/hero.png){align="center"}

La corretta configurazione di Cross-Origin Resource Sharing (CORS) è essenziale per proteggere le applicazioni web dall’accesso non autorizzato ai dati. Quando l&#39;intestazione `Access-Control-Allow-Origin` è impostata su `*`, qualsiasi dominio può richiedere e ricevere risposte, esponendo potenzialmente informazioni riservate ad attacchi. Ciò offre l’opportunità di rafforzare la sicurezza implementando un inserisco nell&#39;elenco Consentiti controllato di domini affidabili o disabilitando CORS laddove non sia richiesto. Garantire una configurazione CORS sicura aiuta a proteggere i contenuti privati mantenendo al contempo l’accesso senza soluzione di continuità per gli utenti autorizzati.

## Identificazione automatica

![Identificazione automatica opportunità di configurazione CORS](./assets/cors-configuration/auto-identify.png){align="center"}

L’identificazione automatica ricerca nel sito web eventuali configurazioni non cors e rileva gli URL che potrebbero essere soggetti ad accesso non autorizzato. Questi URL sono elencati nella tabella superiore, insieme ai seguenti dettagli:

* **Prefisso pagina** - Prefisso del percorso URL vulnerabile a errori di configurazione CORS.
* **Esempio di pagina** - URL di esempio suscettibile di accesso non autorizzato.

## Suggerimento automatico

![Suggerisci automaticamente l&#39;opportunità di configurazione CORS](./assets/cors-configuration/auto-suggest.png){align="center"}

Suggerimento automatico fornisce **file di codice applicazione** e le relative **righe** da rivedere che potrebbero impostare criteri CORS lassisti.


## Ottimizza automaticamente [!BADGE Ultimate]{type=Positive tooltip="Ultimate"}



>[!BEGINTABS]

>[!TAB Ottimizzazione distribuzione]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Richiedi approvazione]

{{auto-optimize-request-approval}}

>[!ENDTABS]

---
title: Documentazione sull’opportunità Configurazione CORS
description: Scopri l’opportunità da cogliere in caso di configurazione CORS e come identificare e correggere le vulnerabilità di sicurezza del sito.
badgeSecurityPosture: label="Livello di sicurezza" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Livello di sicurezza"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: ht
source-wordcount: '192'
ht-degree: 100%

---


# Opportunità configurazione CORS

![Opportunità configurazione CORS](./assets/cors-configuration/hero.png){align="center"}

La corretta configurazione CORS (Cross-Origin Resource Sharing) è essenziale per proteggere le applicazioni web dall’accesso non autorizzato ai dati. Quando l’intestazione `Access-Control-Allow-Origin` è impostata su `*`, qualsiasi dominio può richiedere e ricevere risposte, esponendo potenzialmente informazioni riservate ad attacchi. Questo offre la possibilità di rafforzare la sicurezza implementando un elenco Consentiti controllato di domini affidabili o disabilitando CORS laddove non sia richiesto. Garantire una configurazione CORS sicura aiuta a proteggere i contenuti privati mantenendone al contempo l’accesso semplice per gli utenti autorizzati.

## Identificazione automatica

![Identificazione automatica opportunità configurazione CORS](./assets/cors-configuration/auto-identify.png){align="center"}

L’identificazione automatica analizza il sito web per rilevare eventuali configurazioni CORS errate e URL che potrebbero essere suscettibili ad accesso non autorizzato. Questi URL sono elencati nella tabella nella parte superiore, insieme ai seguenti dettagli:

* **Prefisso pagina**: prefisso del percorso URL vulnerabile alla configurazione CORS errata.
* **Esempio di pagina**: URL di esempio suscettibile all’accesso non autorizzato.

## Suggerimento automatico

![Suggerimento automatico per opportunità configurazione CORS](./assets/cors-configuration/auto-suggest.png){align="center"}

Il suggerimento automatico fornisce **file di codice applicazione** e le relative **righe** da rivedere che potrebbero impostare criteri CORS deboli.


## Ottimizzazione automatica

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

>[!BEGINTABS]

>[!TAB Distribuisci ottimizzazione]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Richiedi approvazione]

{{auto-optimize-request-approval}}

>[!ENDTABS]

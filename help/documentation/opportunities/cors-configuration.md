---
title: Documentazione sull’opportunità Configurazione CORS
description: Scopri l’opportunità da cogliere in caso di configurazione CORS e come identificare e correggere le vulnerabilità di sicurezza del sito.
badgeSecurityPosture: label="Livello di sicurezza" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Livello di sicurezza"
TQID: https://experienceleague.adobe.com/z-8fvRSLN71AnJ4Y6n9TnHGHoOEAAjt8AbVJY9RG-C0
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 252f5292d6dc62711b4ebeb8ce5a2707857fd674
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 100%

---

# Opportunità configurazione CORS

![Opportunità configurazione CORS](./assets/cors-configuration/hero.png){align="center"}

La corretta configurazione CORS (Cross-Origin Resource Sharing) è essenziale per proteggere le applicazioni web dall’accesso non autorizzato ai dati. Quando l’intestazione `Access-Control-Allow-Origin` è impostata su `*`, qualsiasi dominio può richiedere e ricevere risposte, esponendo potenzialmente informazioni riservate ad attacchi. Questa funzionalità offre la possibilità di rafforzare la sicurezza implementando un elenco Consentiti controllato di domini affidabili o disabilitando CORS laddove non sia richiesto. Garantire una configurazione CORS sicura aiuta a proteggere i contenuti privati mantenendone al contempo l’accesso semplice per gli utenti autorizzati.

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

---
title: Documentazione sull’opportunità delle autorizzazioni per il sito web
description: Scopri l’opportunità di autorizzazioni del sito web e come utilizzarla per aumentare la sicurezza di sul sito web.
badgeSecurityPosture: label="Livello di sicurezza" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Livello di sicurezza"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 2%

---


# Opportunità di autorizzazioni per il sito Web

![Opportunità autorizzazioni sito Web](./assets/website-permissions/hero.png){align="center"}

L’opportunità di autorizzazioni del sito web ottimizza le autorizzazioni del sito web, essenziali per mantenere un ambiente AEM sicuro e gestibile. Questa opportunità consente di perfezionare i controlli di accesso rimuovendo le autorizzazioni eccessivamente ampie, ad esempio `jcr:all` su percorsi generici come `/` o `/content`, e allineando l&#39;accesso degli utenti al principio del privilegio minimo. Semplificando le autorizzazioni ed eliminando le ridondanze, è possibile ridurre i rischi per la sicurezza, migliorare la manutenzione ed evitare configurazioni errate in futuro. Rivedi e aggiorna le autorizzazioni nella console Autorizzazioni di sicurezza di AEM o nell’archivio del codice, assicurandoti che gli utenti del servizio abbiano solo l’accesso di cui hanno realmente bisogno.

## Identificazione automatica

![Autorizzazione dell&#39;identificazione automatica del sito Web](./assets/website-permissions/auto-identify.png){align="center"}

La funzionalità **Opportunità autorizzazioni sito Web** identifica ed elenca automaticamente

* **Utente** - L&#39;account utente con l&#39;autorizzazione sospetta.
* **Percorso**: il percorso in AEM interessato dall&#39;autorizzazione.
* **Autorizzazione** - Autorizzazione sospetta.
* **Problema** - Indica il tipo di problema che influisce sull&#39;autorizzazione.

## Suggerimento automatico

![Suggerisci automaticamente le vulnerabilità del sito Web](./assets/website-permissions/auto-suggest.png){align="center"}

La funzione di suggerimento automatico fornisce consigli generati dall&#39;intelligenza artificiale nel campo **Autorizzazioni suggerite**, consentendoti di sostituire eventuali autorizzazioni contrassegnate con alternative sicure.

## Ottimizzazione automatica

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Ottimizzazione automatica autorizzazioni sito Web](./assets/website-permissions/auto-optimize.png){align="center"}

Sites Optimizer Ultimate consente inoltre di distribuire l’ottimizzazione automatica per le vulnerabilità rilevate.

>[!BEGINTABS]

>[!TAB Ottimizzazione distribuzione]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Richiedi approvazione]

{{auto-optimize-request-approval}}

>[!ENDTABS]

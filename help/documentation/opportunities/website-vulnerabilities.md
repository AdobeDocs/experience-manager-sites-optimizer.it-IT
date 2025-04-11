---
title: Documentazione sull’opportunità Vulnerabilità del sito web
description: Scopri l’opportunità da cogliere in caso di vulnerabilità dei siti web e come utilizzarla per aumentare la sicurezza del sito web.
badgeSecurityPosture: label="Livello di sicurezza" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="Livello di sicurezza"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: ht
source-wordcount: '371'
ht-degree: 100%

---


# Opportunità Vulnerabilità del siti web

![Opportunità Vulnerabilità del siti web](./assets/website-vulnerabilities/hero.png){align="center"}

L’opportunità Vulnerabilità del siti web identifica le vulnerabilità di sicurezza nelle librerie di terze parti utilizzate dal codice applicazione. Queste vulnerabilità potrebbero essere sfruttate da utenti malintenzionati, aumentando il rischio e riducendo ol livello di sicurezza del sito web.

L’opportunità Vulnerabilità del sito web presenta un riepilogo nella parte superiore della pagina, che include quanto segue:

* **Problemi rilevati**: numero di vulnerabilità rilevate, classificate in base al rischio di sicurezza che rappresentano (basso, medio, alto).
* **Rischio di sicurezza aggregato**: il rischio di sicurezza complessivo per il sito web in base alle vulnerabilità rilevate dall’opportunità.

## Identificazione automatica

![Identificazione automatica di vulnerabilità del sito web](./assets/website-vulnerabilities/auto-identify.png){align="center"}

L’**opportunità Vulnerabilità del siti web** identifica ed elenca automaticamente le vulnerabilità rilevate nelle librerie di terze parti e utilizzate dal codice applicazione. Fornisce i seguenti dettagli:

* **Libreria**: libreria di terze parti contenente la vulnerabilità. Una singola libreria può avere più vulnerabilità.
* **Versione corrente**: versione della libreria attualmente in uso.
* **Versione consigliata**: versione suggerita che risolve la vulnerabilità.
* **Punteggio**: livello di gravità della vulnerabilità, riassunto anche nella parte superiore della pagina.
* **Vulnerabilità**: identificatore della vulnerabilità, breve descrizione e collegamento al database NVD (National Vulnerability Database) per ulteriori dettagli. Per acceder al collegamento NVD, fai clic sull’identificatore o sul collegamento accanto alla descrizione.

## Suggerimento automatico

![Suggerimento automatico per vulnerabilità del sito web](./assets/website-vulnerabilities/auto-suggest.png){align="center"}

Il suggerimento automatico fornisce suggerimenti generati dall’IA relativi alla **versione consigliata** a cui aggiornare la libreria vulnerabile. Ogni voce ha un **Punteggio** che ne indica la gravità complessiva, utile per dare priorità alle vulnerabilità più critiche.

>[!BEGINTABS]

>[!TAB Dettagli delle vulnerabilità]

Ogni vulnerabilità contiene un collegamento alle informazioni dettagliate riportate nel [National Vulnerability Database (NVD)](https://nvd.nist.gov/). Quando fai clic sull’identificatore della vulnerabilità o sul collegamento a destra della descrizione, puoi passare alla pagina NVD relativa a tale vulnerabilità.

>[!TAB Ignorare le voci]

Puoi scegliere di ignorare le voci dall’elenco delle vulnerabilità. Se selezioni l’**icona Ignora**, la voce corrispondente verrà rimossa dall’elenco. Le voci ignorate possono essere riattivate dalla scheda **Ignorate** nella parte superiore della pagina dell’opportunità.<!---right now it does not seem to be implemented, but the page description mentions this functionality-->

>[!ENDTABS]


## Ottimizzazione automatica

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Ottimizzazione automatica delle vulnerabilità dei siti web](./assets/website-vulnerabilities/auto-optimize.png){align="center"}

Sites Optimizer Ultimate aggiunge la possibilità di distribuire l’ottimizzazione automatica per le vulnerabilità rilevate.

>[!BEGINTABS]

>[!TAB Implementa ottimizzazione]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB Richiedi approvazione]

{{auto-optimize-request-approval}}

>[!ENDTABS]
---
title: Versione di prova di Sites Optimizer
description: Introduzione alla versione di prova di AEM Sites Optimizer per clienti di AEM Sites esistenti.
source-git-commit: 5bd55dcc380f0721fb9818413207c22e21e8299b
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 59%

---


# Versione di prova di Sites Optimizer

Inizia a usare Sites Optimizer utilizzando questa versione di prova per **clienti AEM Sites esistenti (Edge Delivery Services, Cloud Services e Managed Services)**. L’onboarding dei dati del tuo dominio è già stato effettuato, pertanto puoi iniziare l’ottimizzazione fin da subito. Il video seguente illustra l’esperienza della versione di prova e mostra come iniziare.

>[!IMPORTANT]
>
>Prima di iniziare, assicurati che il sito soddisfi i seguenti requisiti:
>
>* È basato su AEM Sites (Edge Delivery Services, Cloud Service o Managed Services).
>* Si tratta di un sito di produzione, non di un ambiente di sviluppo, di controllo qualità, di staging, di authoring o di anteprima.
>* È accessibile al pubblico e non dietro un accesso.
>* Utilizza la distribuzione front-end in AEM Sites. La distribuzione headless non è attualmente supportata.

>[!VIDEO](https://video.tv.adobe.com/v/3483253/?learn=on&enablevpops)

>[!TIP]
>
> Contatta [siteoptimizer-now@adobe.com](mailto:siteoptimizer-now@adobe.com) per qualsiasi domanda o richiesta.

## Inizia subito la versione di prova.

Per iniziare a utilizzare la versione di prova, segui i passaggi riportati di seguito:

1. Accedi con il tuo ID organizzazione IMS per AEM Sites su [www.sitesoptimizer.live](http://www.sitesoptimizer.live/).
2. Visualizza metriche chiave quali visualizzazioni di pagina, tempo di caricamento e tasso di coinvolgimento, oltre alle principali opportunità di ottimizzazione prioritarie in base all’impatto.
3. Esplora i tre tipi di opportunità disponibili: [backlink interrotti](./opportunities/broken-backlinks.md), [Core Web Vitals](./opportunities/core-web-vitals.md) e [testo alternativo mancante](./opportunities/missing-alt-text.md).
4. Per ogni opportunità, rivedi fino a tre problemi identificati. Utilizza i suggerimenti generati dall’IA e, quando è il momento, implementa le ottimizzazioni direttamente nell’ambiente AEM.
5. In qualsiasi momento, puoi sbloccare più opportunità effettuando l’aggiornamento alla licenza completa.

## Cosa è disponibile nella versione di prova

La versione di prova include quanto segue:

* Tre tipi di opportunità: [backlink interrotti](./opportunities/broken-backlinks.md), [Core Web Vitals](./opportunities/core-web-vitals.md) e [testo alternativo mancante](./opportunities/missing-alt-text.md).
* Fino a tre problemi per opportunità ogni mese.
* Flusso di lavoro completo per problema: identificazione automatica, suggerimento automatico e ottimizzazione automatica.
  * **Identificazione automatica**: rileva i problemi nel sito utilizzando più origini dati.
  * **Suggerimento automatico**: fornisce consigli prescrittivi e generati dall’IA per ogni problema.
  * **Ottimizzazione automatica**: dopo l’approvazione, implementa le correzioni direttamente nell’ambiente di authoring. Gli aggiornamenti seguono i flussi di lavoro esistenti e consentono al team di rivedere e pubblicare tramite AEM.

## Abilita correzione automatica per i siti di prova di Edge Delivery

Scopri come i clienti di prova abilitano l&#39;azione **Distribuisci per l&#39;authoring** per suggerimenti di correzione automatica sui siti Edge Delivery Services (EDS) creati in Google Drive o SharePoint.

>[!NOTE]
>
>Questo requisito si applica solo alle organizzazioni di valutazione i cui siti sono creati in Google Drive o SharePoint. I clienti pagati e i siti creati in Crosswalk o Dark Alley non sono interessati.

I clienti di prova devono far parte del gruppo IMS **ASO-EDS-Autofix-Users**. Se il gruppo non esiste, l’amministratore della tua organizzazione può crearlo e aggiungerti.

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/).
1. Selezionare **Utenti** > **Gruppi di utenti**.
1. Selezionare **Aggiungi gruppo utenti**.
1. Per **Nome gruppo utenti**, immettere esattamente:

   ```
   ASO-EDS-Autofix-Users
   ```

   >[!IMPORTANT]
   >
   > Il nome del gruppo deve corrispondere esattamente, comprese le iniziali maiuscole. La corrispondenza è sensibile a maiuscole e minuscole, pertanto non funziona un&#39;ortografia o una combinazione di maiuscole e minuscole diversa, ad esempio `ASO-EDS-Autofix-users`. Non rinominare il gruppo dopo averlo creato.

1. Seleziona **Salva**.

   ![Crea una finestra di dialogo per un nuovo gruppo utenti in Adobe Admin Console, con il campo Nome gruppo utenti impostato su ASO-EDS-Autofix-Users](./assets/trial/create-user-group.png){align="center"}

1. Apri il nuovo gruppo e seleziona **Aggiungi utenti**.
1. Inserisci l&#39;indirizzo e-mail o il nome utente di ogni persona che dovrebbe essere in grado di distribuire correzioni automatiche, quindi seleziona **Salva**.

   ![Finestra di dialogo Aggiungi utenti a questo gruppo di utenti in Adobe Admin Console](./assets/trial/add-users-to-group.png){align="center"}

Se sei membro del gruppo, il pulsante **Distribuisci all&#39;autore** è abilitato. Se non sei ancora membro, **Distribuisci all&#39;autore** è disabilitato con una descrizione comando che ti chiede di contattare l&#39;amministratore per aggiungerti al gruppo. Dopo che l’amministratore ti ha aggiunto al gruppo, esci e accedi di nuovo a Sites Optimizer in modo che la tua sessione possa scegliere la nuova iscrizione al gruppo.

## Domande frequenti

Leggi le risposte alle domande più frequenti sulla versione di prova di AEM Sites Optimizer.

+++Che cos’è AEM Sites Optimizer?

[AEM Sites Optimizer](/help/home.md) è un’applicazione basata sull’intelligenza artificiale che identifica i problemi nel sito web, fornisce consigli prescrittivi e ti aiuta a risolverli per aumentare l’acquisizione, il coinvolgimento e la conversione del traffico.

+++
+++Chi può partecipare a questa versione di prova?

Clienti AEM Sites esistenti (Edge Delivery Services, Cloud Services e Managed Services).

+++
+++Come posso accedere alla versione di prova?

Passa a [www.sitesoptimizer.live](http://www.sitesoptimizer.live/) e accedi con il tuo ID organizzazione IMS per AEM Sites.

+++
+++La versione di prova ha un costo?

No. Questa versione di prova è disponibile gratuitamente per clienti AEM Sites esistenti.

+++
+++La versione di prova ha una data di scadenza?

No. La versione di prova non è basata sul tempo. L’utilizzo è limitato in base al numero di tipi di opportunità e problemi disponibili.
+++
+++Cosa succede dopo che tutti i problemi sono stati risolti?

Sites Optimizer identifica continuamente i problemi che influiscono sulle prestazioni. Nella versione di prova gratuita, i problemi vengono aggiunti solo mensilmente. Esegui l’aggiornamento per l’auditing e l’ottimizzazione continui.

+++
+++Come posso accedere a più opportunità?

Utilizza le CTA di aggiornamento o di contatto vendite disponibili tramite l’esperienza del prodotto oppure invia un’e-mail a [siteoptimizer-now@adobe.com](mailto:siteoptimizer-now@adobe.com).

+++
+++Sono nel gruppo ASO-EDS-Autofix-Users, ma la funzione Distribuisci all’authoring è ancora disabilitata. Cosa devo controllare?

Esci e accedi di nuovo — l&#39;iscrizione al gruppo viene letta all&#39;accesso. Confermare inoltre che il nome del gruppo sia scritto e scritto esattamente in maiuscolo `ASO-EDS-Autofix-Users` e che sia stato creato nella stessa organizzazione a cui appartiene il sito.

+++
+++Il requisito di gruppo ASO-EDS-Autofix-Users si applica a tutti i siti Edge Delivery Services?

No. Si applica solo ai siti di prova creati in **Google Drive** o **SharePoint**. I siti creati in **Crosswalk** o **Dark Alley** e tutti i **siti a pagamento** non sono interessati.

+++

<!--
CARDS
* ./opportunities/core-web-vitals.md
  {title=Core web vitals}
  {image=../assets/common/card-performance.png}
* ./opportunities/missing-alt-text.md
  {title=Missing alt text}
  {image=../assets/common/card-arrows.png}
* ./opportunities/broken-backlinks.md
  {title=Broken backlinks}
  {image=../assets/common/card-arrows.png}
-->

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Core web vitals">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/core-web-vitals.md" title="Web vitals di base" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-performance.png" alt="Web vitals di base"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/core-web-vitals.md" target="_blank" rel="referrer" title="Web vitals di base">Web vitals di base</a>
                    </p>
                    <p class="is-size-6">Scopri l’opportunità relativa ai Core Web Vitals e come utilizzarla per migliorare l’acquisizione del traffico.</p>
                </div>
                <a href="./opportunities/core-web-vitals.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    Ulteriori informazioni<span class="spectrum-Button-label has-no-wrap has-text-weight-bold"></span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Missing alt text">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/missing-alt-text.md" title="Testo alternativo mancante" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-arrows.png" alt="Testo alternativo mancante"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/missing-alt-text.md" target="_blank" rel="referrer" title="Testo alternativo mancante">Testo alternativo mancante</a>
                    </p>
                    <p class="is-size-6">Scopri l’opportunità da cogliere in caso di testo alternativo mancante e come utilizzarla per migliorare il coinvolgimento sul tuo sito web.</p>
                </div>
                <a href="./opportunities/missing-alt-text.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    Ulteriori informazioni<span class="spectrum-Button-label has-no-wrap has-text-weight-bold"></span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Broken backlinks">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/broken-backlinks.md" title="Backlink interrotti" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-arrows.png" alt="Backlink interrotti"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/broken-backlinks.md" target="_blank" rel="referrer" title="Backlink interrotti">Backlink interrotti</a>
                    </p>
                    <p class="is-size-6">Scopri l’opportunità da cogliere in caso di backlink interrotti e come utilizzarla per migliorare l’acquisizione del traffico.</p>
                </div>
                <a href="./opportunities/broken-backlinks.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    Ulteriori informazioni<span class="spectrum-Button-label has-no-wrap has-text-weight-bold"></span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

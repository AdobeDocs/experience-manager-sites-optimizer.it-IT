---
title: Configurazione della verifica preliminare
description: Scopri come impostare la verifica preliminare per AEM Sites Optimizer.
TQID: https://experienceleague.adobe.com/GfLmEEBoSP2481ZZUjRyyfMjExGgI0l9yMAqTF8ObcY
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
source-git-commit: f19dd2eec5cef95f406111d2250ff1101a4fd430
workflow-type: tm+mt
source-wordcount: 577
ht-degree: 72%

---

# Configurazione della verifica preliminare

Per eseguire la verifica preliminare è necessario configurarla nell&#39;ambiente di authoring. È possibile impostare la verifica preliminare per l’editor universale, l’authoring basato su documenti, l’editor pagina di AEM Sites o Adobe Managed Services, in modo da poter eseguire i controlli di verifica preliminare sulle pagine prima che vengano pubblicate.

## Abilitare l’accesso degli utenti

Per utilizzare Verifica preliminare, accertati che l&#39;utente sia assegnato ad almeno uno dei seguenti profili di prodotto AEM Sites Optimizer in [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer - Suggerimento automatico utente
* AEM Sites Optimizer - Ottimizzazione automatica utente

## Abilita verifica preliminare

>[!BEGINTABS]

>[!TAB Editor universale]

Per impostare la verifica preliminare nell’editor universale, segui questi passaggi:

1. Apri **Extension Manager** in:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Individua l’estensione **Verifica preliminare per AEM Sites Optimizer**.
1. L’amministratore di sistema dell’organizzazione dovrà abilitare questa estensione.
1. Dopo aver abilitato l’estensione, apri una pagina nell’**editor universale**, ad esempio:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. L’estensione **Verifica preliminare** viene visualizzata nella **barra laterale**.
1. Selezionare l&#39;estensione **Verifica preliminare** dalla barra laterale per aprire Verifica preliminare per la pagina corrente.

>[!TAB Authoring basato su documenti]

Per impostare la verifica preliminare per l’authoring basato su documenti, segui questi passaggi:

1. Aggiungi la seguente configurazione a `/tools/sidekick/config.json` nell’archivio GitHub del progetto Edge Delivery Services:

   ```json
   {
     "plugins": [
       {
         "id": "preflight",
         "titleI18n": {
           "en": "Preflight"
         },
         "environments": ["preview"],
         "event": "preflight"
       }
     ]
   }
   ```

1. Crea un nuovo file `/tools/sidekick/aem-sites-optimizer-preflight.js` e aggiungi il contenuto seguente:

   ```javascript
   (function () {
     let isAEMSitesOptimizerPreflightAppLoaded = false;
     function loadAEMSitesOptimizerPreflightApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMSitesOptimizerPreflightAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMSitesOptimizerPreflightApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMSitesOptimizerPreflightAppLoaded) {
         loadAEMSitesOptimizerPreflightApp();
       }
     }
   
     // Sidekick V1 extension support
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       sidekick.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   
     // Sidekick V2 extension support
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       sidekickV2.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. Aggiorna la funzione `loadLazy()` in `/scripts/scripts.js` per importare lo script di verifica preliminare per gli URL di anteprima:

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. Apri l’URL di anteprima (`*.aem.page`) della pagina di cui eseguire l’audit.
1. In **Sidekick**, fare clic sul pulsante **Verifica preliminare** per aprire Verifica preliminare per la pagina corrente.

>[!TAB Editor pagina per AEM Sites]

Per utilizzare Verifica preliminare nell’editor di pagina di AEM Sites, puoi creare un bookmarklet nel browser web. Segui questi passaggi:

1. Mostra la **Barra Segnalibri** nel browser web:

   * Premi **Ctrl+Maiusc+B** (Windows) o **Comando+Maiusc+B** (Mac).

1. Crea un nuovo segnalibro nel browser:

   * Fai clic con il pulsante destro del mouse sulla barra dei segnalibri e seleziona **Nuova pagina** o **Aggiungi segnalibro**.
   * Nel campo **Indirizzo (URL)**, incolla il seguente codice:

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
   ```

1. Assegna al segnalibro il nome **Verifica preliminare** (o un nome qualsiasi).
1. Apri l’URL di anteprima (`*.aem.page`) della pagina di cui eseguire l’audit nell’**Editor pagina per AEM Sites**.
1. Fare clic sul segnalibro **Verifica preliminare** nella barra Segnalibri per aprire Verifica preliminare per la pagina corrente.

>[!TAB Adobe Managed Services]

>[!IMPORTANT]
>
>Sono supportati solo gli ambienti Adobe Managed Services (AMS) che utilizzano il provider di identità di Adobe (IMS) per l’autenticazione in AEM Author. La verifica preliminare non funziona se l’organizzazione utilizza un altro provider di identità per l’autenticazione AMS.

Per utilizzare la verifica preliminare nell’Editor pagina di AEM Sites in un ambiente AMS, crea un bookmarklet nel browser web, seguendo la procedura riportata di seguito:

1. Mostra **Barra Segnalibri** nel browser web:

   * Premi **Ctrl+Maiusc+B** (Windows) o **Comando+Maiusc+B** (Mac).

1. Crea un nuovo segnalibro nel browser:

   * Fai clic con il pulsante destro del mouse sulla barra dei segnalibri e seleziona **Nuova pagina** o **Aggiungi segnalibro**.
   * Nel campo **Indirizzo (URL)**, incolla il seguente codice:

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=ams';document.head.appendChild(script);})();
   ```

1. Assegna al segnalibro il nome **Verifica preliminare** (o un nome qualsiasi).
1. Apri la pagina di cui eseguire l’audit nell’**Editor pagina per AEM Sites**.
1. Fare clic sul segnalibro **Verifica preliminare** nella barra Segnalibri per aprire Verifica preliminare per la pagina corrente.

>[!ENDTABS]

## Best practice

Quando esegui gli audit di verifica preliminare, tieni presenti le seguenti linee guida:

* Esegui sempre gli audit sulle **pagine di staging o anteprima** prima di pubblicarle in produzione.
* Assegna priorità alla risoluzione di **problemi ad alto impatto** quali collegamenti interrotti, tag H1 mancanti o collegamenti non sicuri.
* Prima di eseguire l’audit, verifica che **l’autenticazione sia abilitata** per gli ambienti di staging protetti.
* Rivedi e applica **consigli sui tag meta** per migliorare le prestazioni SEO (Search Engine Optimization).

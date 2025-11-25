---
title: Configurazione della verifica preliminare
description: Scopri come impostare l’estensione Verifica preliminare per AEM Sites Optimizer.
source-git-commit: 2f4ef1c6f44d602bfe365a52eb692fe7faa7f05f
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 67%

---


# Configurazione della verifica preliminare

L&#39;identificazione dell&#39;opportunità di verifica preliminare di AEM Sites Optimizer richiede la configurazione dell&#39;estensione di verifica preliminare. Puoi configurarlo in Universal Editor, Document-Based Preview o AEM Cloud Service, in modo da poter eseguire controlli di verifica preliminare sulle pagine prima che vengano pubblicate.

## Abilitare l’accesso degli utenti

Per utilizzare l&#39;estensione Verifica preliminare, accertati che l&#39;utente sia assegnato ad almeno uno dei seguenti profili di prodotto AEM Sites Optimizer in [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer - Suggerimento automatico utente
* AEM Sites Optimizer - Ottimizzazione automatica utente

## Abilitare l’estensione Verifica preliminare

>[!BEGINTABS]

>[!TAB Editor universale]

Per impostare la verifica preliminare nell’editor universale, segui questi passaggi:

1. Apri **Extension Manager** in:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Individua l’**estensione Verifica preliminare AEM Sites Optimizer** e invia una richiesta per abilitarla.
1. **Adobe AEM team** rivede e abilita l&#39;estensione per la tua organizzazione.
1. Dopo aver abilitato l’estensione, apri una pagina nell’**editor universale**, ad esempio:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. L&#39;estensione **Verifica preliminare** viene visualizzata nella **barra laterale**.
1. Seleziona l’**estensione Verifica preliminare** dalla barra laterale, per avviare l’**audit della verifica preliminare** per la pagina corrente.

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

1. Aprire l&#39;URL di anteprima (`*.aem.page`) della pagina che si desidera controllare.
1. In **Sidekick**, fai clic sul pulsante **Verifica preliminare** per avviare il controllo di audit per la pagina corrente.

>[!TAB Editor pagina per AEM Sites]

Per utilizzare Verifica preliminare nell’editor di pagina di AEM Sites, puoi creare un bookmarklet nel browser web. Segui questi passaggi:

1. Mostra **Barra Segnalibri** nel browser Web:

   * Premi **Ctrl+Maiusc+B** (Windows) o **Comando+Maiusc+B** (Mac).

1. Crea un nuovo segnalibro nel browser:

   * Fai clic con il pulsante destro del mouse sulla barra dei segnalibri e seleziona **Nuova pagina** o **Aggiungi segnalibro**.
   * Nel campo **Indirizzo (URL)**, incolla il seguente codice:

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
   ```

1. Assegna al segnalibro il nome **Verifica preliminare** (o un nome qualsiasi).
1. Aprire l&#39;URL di anteprima (`*.aem.page`) della pagina che si desidera controllare nell&#39;**Editor pagina AEM Sites**.
1. Fai clic sul segnalibro **Verifica preliminare** nella barra Segnalibri per avviare il controllo di audit per la pagina corrente.

>[!ENDTABS]

## Best practice

Quando esegui gli audit di verifica preliminare, tieni presenti le seguenti linee guida:

* Esegui sempre gli audit sulle **pagine di staging o anteprima** prima di pubblicarle in produzione.
* Assegna priorità alla risoluzione di **problemi ad alto impatto** quali collegamenti interrotti, tag H1 mancanti o collegamenti non sicuri.
* Prima di eseguire i controlli, verificare che l&#39;autenticazione **sia abilitata** per gli ambienti di gestione temporanea protetti.
* Rivedi e applica **consigli sui tag meta** per migliorare le prestazioni SEO (Search Engine Optimization).

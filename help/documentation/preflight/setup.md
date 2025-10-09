---
title: Configurazione della verifica preliminare
description: Scopri come impostare l’estensione Verifica preliminare per AEM Sites Optimizer.
source-git-commit: 6e177ef6b9d121ac7484ae118037c7e542f981d8
workflow-type: ht
source-wordcount: '424'
ht-degree: 100%

---


# Configurazione della verifica preliminare

Per identificare l’opportunità di verifica preliminare di AEM Sites Optimizer è necessario configurare l’estensione Verifica preliminare nell’editor universale, nell’anteprima basata su documenti o in AEM Cloud Service, al fine di eseguire audit di verifica preliminare sulle pagine prima che vengano pubblicate.

## Abilitare l’accesso degli utenti

Per utilizzare l’estensione Verifica preliminare, accertati che l’utente sia assegnato ad almeno uno dei seguenti profili di prodotto AEM Sites Optimizer in [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer - Suggerimento automatico utente
* AEM Sites Optimizer - Ottimizzazione automatica utente

## Abilitare l’estensione Verifica preliminare

>[!BEGINTABS]

>[!TAB Editor universale]

Per impostare la verifica preliminare nell’editor universale, segui questi passaggi:

1. Apri **Extension Manager** in:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Individua l’**estensione Verifica preliminare AEM Sites Optimizer** e invia una richiesta per abilitarla.
1. Il **team Adobe AEM** rivedrà e abiliterà l’estensione per la tua organizzazione.
1. Dopo aver abilitato l’estensione, apri una pagina nell’**editor universale**, ad esempio:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. L’**estensione Verifica preliminare** sarà visibile nella **barra laterale**.
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

1. Apri l’URL di anteprima (`*.aem.page`) della pagina di cui desideri eseguire l’audit.
1. In **Sidekick**, fai clic sul pulsante **Verifica preliminare** per avviare il controllo di audit per la pagina corrente.

>[!TAB Editor pagina per AEM Sites]

Per utilizzare Verifica preliminare nell’editor di pagina di AEM Sites, puoi creare un bookmarklet nel browser web. Segui questi passaggi:

1. Mostra **Barra Segnalibri** nel browser web:

   * Premi **Ctrl+Maiusc+B** (Windows) o **Comando+Maiusc+B** (Mac).

!. Crea un nuovo segnalibro nel browser:

* Fai clic con il pulsante destro del mouse sulla barra dei segnalibri e seleziona **Nuova pagina** o **Aggiungi segnalibro**.
* Nel campo **Indirizzo (URL)**, incolla il seguente codice:

```javascript
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

1. Assegna al segnalibro il nome **Verifica preliminare** (o un nome qualsiasi).
1. Apri l’URL di anteprima (`*.aem.page`) della pagina di cui desideri eseguire l’audit nell’**editor pagina AEM Sites**.
1. Fai clic sul segnalibro **Verifica preliminare** nella barra Segnalibri per avviare il controllo di audit per la pagina corrente.

>[!ENDTABS]

## Best practice

Quando esegui gli audit di verifica preliminare, tieni presenti le seguenti linee guida:

* Esegui sempre gli audit sulle **pagine di staging o anteprima** prima di pubblicarle in produzione.
* Assegna priorità alla risoluzione di **problemi ad alto impatto** quali collegamenti interrotti, tag H1 mancanti o collegamenti non sicuri.
* Prima di eseguire gli audit, assicurati che l’**autenticazione sia abilitata** per gli ambienti di staging protetti.
* Rivedi e applica **consigli sui tag meta** per migliorare le prestazioni SEO (Search Engine Optimization).

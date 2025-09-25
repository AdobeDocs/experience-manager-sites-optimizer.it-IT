---
title: Configurazione verifica preliminare
description: Scopri come impostare l’estensione Verifica preliminare per AEM Sites Optimizer.
source-git-commit: 6e177ef6b9d121ac7484ae118037c7e542f981d8
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---


# Configurazione verifica preliminare

Per identificare l’opportunità di verifica preliminare di AEM Sites Optimizer è necessario configurare l’estensione Verifica preliminare in Universal Editor, Document-Based Preview o AEM Cloud Service per eseguire controlli di verifica preliminare sulle pagine prima che vengano pubblicate.

## Abilita accesso utente

Per utilizzare l&#39;estensione Verifica preliminare, accertati che l&#39;utente sia assegnato ad almeno uno dei seguenti profili di prodotto AEM Sites Optimizer in [Adobe Admin Console](https://adminconsole.adobe.com):

* AEM Sites Optimizer - Suggerimento automatico utente
* AEM Sites Optimizer - Ottimizzazione automatica utente

## Abilita l&#39;estensione Verifica preliminare

>[!BEGINTABS]

>[!TAB Editor universale]

Per impostare la verifica preliminare in Universal Editor, effettuare le seguenti operazioni:

1. Apri **Extension Manager** in:
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. Individua l&#39;**estensione Verifica preliminare AEM Sites Optimizer** e invia una richiesta per abilitarla.
1. Il **team AEM di Adobe** esaminerà e abiliterà l&#39;estensione per la tua organizzazione.
1. Dopo aver abilitato l&#39;estensione, aprire una pagina in **Universal Editor**, ad esempio:
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. L&#39;estensione **Verifica preliminare** verrà visualizzata nella **barra laterale**.
1. Seleziona l&#39;**Estensione verifica preliminare** dalla barra laterale per avviare un **Audit verifica preliminare** della pagina corrente.

>[!TAB Authoring basato su documenti]

Per impostare la verifica preliminare per l&#39;authoring basato su documenti, eseguire la procedura seguente:

1. Aggiungi la seguente configurazione a `/tools/sidekick/config.json` nell&#39;archivio GitHub del progetto Edge Delivery Services:

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

1. Creare un nuovo file `/tools/sidekick/aem-sites-optimizer-preflight.js` e aggiungere il contenuto seguente:

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

1. Aggiornare la funzione `loadLazy()` in `/scripts/scripts.js` per importare lo script di verifica preliminare per gli URL di anteprima:

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. Aprire l&#39;URL di anteprima (`*.aem.page`) della pagina che si desidera controllare.
1. In **Sidekick**, fai clic sul pulsante **Verifica preliminare** per avviare il controllo di audit per la pagina corrente.

>[!TAB Editor pagina AEM Sites]

Per utilizzare Verifica preliminare nell’Editor pagina di AEM Sites, puoi creare un bookmarklet nel browser web. Segui questi passaggi:

1. Mostra **Barra Segnalibri** nel browser Web:

   * Premere **Ctrl+Maiusc+B** (Windows) o **Cmd+Maiusc+B** (Mac).

! Crea un nuovo segnalibro nel browser:

* Fare clic con il pulsante destro del mouse sulla barra Segnalibri e selezionare **Nuova pagina** o **Aggiungi segnalibro**.
* Nel campo **Indirizzo (URL)**, incolla il seguente codice:

```javascript
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

1. Assegna al segnalibro **Verifica preliminare** (o un nome qualsiasi).
1. Aprire l&#39;URL di anteprima (`*.aem.page`) della pagina che si desidera controllare nell&#39;**Editor pagine AEM Sites**.
1. Fare clic sul segnalibro **Verifica preliminare** nella barra Segnalibri per avviare il controllo di audit per la pagina corrente.

>[!ENDTABS]

## Best practice

Quando esegui i controlli di verifica preliminare, tieni presenti le seguenti linee guida:

* Esegui sempre i controlli sulle **pagine di staging o anteprima** prima di pubblicarle in produzione.
* Assegna priorità alla risoluzione di **problemi ad alto impatto** quali collegamenti interrotti, tag H1 mancanti o collegamenti non sicuri.
* Prima di eseguire i controlli, verificare che l&#39;autenticazione **sia abilitata** per gli ambienti di gestione temporanea protetti.
* Rivedi e applica **consigli sui tag meta** per migliorare le prestazioni SEO (Search Engine Optimization).

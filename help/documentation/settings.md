---
title: Impostazioni di Sites Optimizer
description: Scopri come configurare le impostazioni di Sites Optimizer e integrarle con altri strumenti.
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 12%

---

# Impostazioni di Sites Optimizer

![Impostazioni di Sites Optimizer](./assets/settings/hero.png){align="center"}

Le impostazioni di Sites Optimizer sono l’hub centrale per la configurazione dell’esperienza Sites Optimizer.

## Google Search Console

![Impostazioni Sites Optimizer per la console Google Search](./assets/settings/google-search-console.png){align="center"}

Il connettore di impostazioni di Google Search Console in AEM Sites Optimizer consente di analizzare le metriche SEO (Search Engine Optimization) chiave quali classificazione nei risultati di ricerca, tassi di click-through e Core Web Vitals. Mantenendo la connessione con Google Search Console, puoi sfruttare l’analisi JSON per individuare opportunità di ottimizzazione e migliorare le prestazioni del sito.

Per configurare questo connettore, è necessario disporre di credenziali con accesso amministrativo a Google Search Console per il dominio.

## Connessione ad AEM Sites

Questa guida spiega come collegare il sito Edge Delivery Services (EDS) esistente ad AEM Sites Optimizer. Prima di iniziare, verificare che il sito EDS sia già configurato e funzionante. Questa connessione è specifica per AEM Sites Optimizer per l&#39;accesso al contenuto.

La connessione richiede due passaggi:

1. Specifica l’URL dell’archivio del codice e l’URL dell’origine del contenuto.
2. Concedi ad AEM Sites Optimizer l’accesso alla tua origine di contenuto.

### Passaggio 1: collegare l’archivio del codice e l’origine del contenuto

In AEM Sites Optimizer, vai a **Impostazioni → Connetti ad AEM Sites** e immetti quanto segue:

- **URL archivio codici**: l&#39;URL GitHub del sito EDS, ad esempio:
  `https://github.com/owner/repo`

- **URL Source contenuto**: l&#39;URL della cartella SharePoint o della cartella Unità Google che supporta il sito EDS, ad esempio:
  `https://drive.google.com/drive/folders/...` oppure `https://myorg.sharepoint.com/...`

Dopo aver inserito l’URL del Source di contenuto, AEM Sites Optimizer rileverà il tipo di origine di contenuto e mostrerà le istruzioni di accesso pertinenti di seguito.

### Passaggio 2: concedere l&#39;accesso all&#39;origine di contenuto

Segui la sezione che corrisponde all’origine di contenuto.

#### SharePoint — Dominio Adobe

![Connessione alla finestra di dialogo di AEM Sites che non mostra alcuna azione richiesta per il dominio Adobe SharePoint](./assets/settings/connect-content-and-drive.png){align="center"}

Se l’URL del Source dei contenuti utilizza il dominio Adobe SharePoint, non è necessaria alcuna ulteriore azione. L&#39;accesso è già configurato. Fai clic su **Salva** per completare la connessione.

#### SharePoint — Dominio personalizzato

Se l’URL del Source dei contenuti utilizza il dominio SharePoint della tua organizzazione, devi registrare un’applicazione Azure e fornire le relative credenziali ad AEM Sites Optimizer.

##### Cosa ti servirà

- Autorizzazione a registrare applicazioni nel portale Azure o un contatto che può registrare applicazioni per tuo conto.
- I diritti di amministratore tenant per concedere il consenso API o un amministratore che può approvare il consenso API per te.

##### Passaggio 2a — Registrazione di un&#39;applicazione in Azure

1. Vai a **Azure Portal → Microsoft Entra ID → Registrazioni app → Nuova registrazione**.
2. Assegnare un nome, ad esempio: `AEM Sites Optimizer`.
3. Lascia tutte le altre impostazioni predefinite e fai clic su **Registra**.
4. Nella pagina **Panoramica**, annota in basso:
   - **ID applicazione (client)**
   - **ID directory (tenant)**

##### Passaggio 2b — Aggiungere le autorizzazioni API

1. Vai a **Autorizzazioni API → Aggiungi un&#39;autorizzazione → autorizzazioni dell&#39;applicazione → di Microsoft Graph**.
2. Aggiungi entrambe le opzioni seguenti:
   - `Sites.Selected` - Accesso con ambito a raccolte siti di SharePoint specifiche.
   - `Files.SelectedOperations.Selected` - accesso ai file senza un utente connesso.
3. Fai clic su **Concedi il consenso dell&#39;amministratore** per entrambi.

![Autorizzazioni API di Azure che mostrano Sites.Selected e Files.SelectedOperations.Selected concesse](./assets/settings/app-permissions.png){align="center"}

>[!NOTE]
>
>La concessione del consenso dell’amministratore richiede i diritti di amministratore del tenant. In caso contrario, chiedi all’amministratore IT o Azure di completare questo passaggio prima di procedere.

##### Passaggio 2c — Creare un segreto client

![Pagina certificati e segreti Azure per la registrazione dell&#39;app](./assets/settings/create-credentials.png){align="center"}

1. Vai a **Certificati e segreti → nuovo segreto client**.
2. Imposta una descrizione e una scadenza, quindi fai clic su **Aggiungi**.
3. Copia immediatamente il valore segreto, che viene visualizzato una sola volta.

##### Passaggio 2d — Concedere all’app l’accesso al sito SharePoint

Puoi concedere l’accesso all’app utilizzando le chiamate API di Microsoft Graph Explorer, PowerShell o Graph dirette.

Passa a [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), accedi con il tuo account Microsoft ed esegui le seguenti richieste:

1. Ricerca dell&#39;ID sito:

```
GET https://graph.microsoft.com/v1.0/sites/{tenant}.sharepoint.com:/sites/{site-name}
```

1. Copia `id` dalla risposta, quindi concedi l&#39;accesso a livello di sito:

```
POST https://graph.microsoft.com/v1.0/sites/{siteId}/permissions
```

Corpo:

```json
{
  "roles": ["write"],
  "grantedToIdentities": [{
    "application": {
      "id": "{your-client-id}",
      "displayName": "{Your app name}"
    }
  }]
}
```

##### Passaggio 2e — Immettere le credenziali in AEM Sites Optimizer

![Finestra di dialogo Connetti ad AEM Sites con i campi delle credenziali di SharePoint](./assets/settings/add-sharepoint-credentials.png){align="center"}

Tornando nella finestra di dialogo **Connetti ad AEM Sites**, immetti quanto segue in **Connessione all&#39;archivio dei contenuti tramite SharePoint**:

- **ID tenant (Azure AD)** - da Panoramica → registrazione app.
- **ID client (registrazione app)** - da Panoramica → registrazione app.
- **Segreto client** — creato nel passaggio 2c.

Fai clic su **Convalida connessione** per confermare l&#39;accesso, quindi fai clic su **Salva**.

#### Google Drive

![Finestra di dialogo Connetti ad AEM Sites che mostra l&#39;account del servizio Google Drive per l&#39;accesso condiviso](./assets/settings/validate-eds-google.png){align="center"}

1. In Google Drive, fai clic con il pulsante destro del mouse sulla cartella che supporta il sito EDS e seleziona **Condividi**.
2. Nel campo **Aggiungi persone e gruppi**, immetti l&#39;e-mail dell&#39;account del servizio visualizzata nella finestra di dialogo **Connetti ad AEM Sites**:
   `experience-success-studio@helix-225321.iam.gserviceaccount.com`
3. Imposta il livello di autorizzazione su **Editor**.
4. Deseleziona **Notifica agli utenti** e fai clic su **Condividi**.

Al termine della condivisione, fare clic su **Convalida connessione** nella finestra di dialogo, quindi fare clic su **Salva**.

---
title: Impostazioni di Sites Optimizer
description: Scopri come configurare le impostazioni di Sites Optimizer e integrarle con altri strumenti.
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
source-git-commit: 37d90154e6868ee392bf1b779b2bf3697112b7ce
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 39%
---
# Impostazioni di Sites Optimizer

![Impostazioni di Sites Optimizer](./assets/settings/hero.png){align="center"}

Le impostazioni di Sites Optimizer rappresentano l’hub centrale per configurare l’esperienza di Sites Optimizer.

## Google Search Console

![Impostazioni di Sites Optimizer per Google Search Console](./assets/settings/google-search-console.png){align="center"}

Il connettore di impostazioni di Google Search Console in AEM Sites Optimizer consente di analizzare le metriche SEO (Search Engine Optimization) chiave quali ranking nei risultati di ricerca, tassi di click-through e Core Web Vitals. Mantenendo la connessione con Google Search Console, puoi sfruttare l’analisi JSON per individuare opportunità di ottimizzazione e migliorare le prestazioni del sito.

Per configurare questo connettore, è necessario disporre di credenziali con accesso amministrativo a Google Search Console per il dominio.

## Connessione ad AEM Sites

Questa guida spiega come connettere il sito Edge Delivery Services (EDS) esistente ad AEM Sites Optimizer. Prima di iniziare, verifica che il sito EDS sia già configurato e funzionante. Questa connessione serve specificatamente a consentire ad AEM Sites Optimizer di accedere ai tuoi contenuti.

La connessione richiede due passaggi:

1. Specificare l’URL dell’archivio del codice e l’URL dell’origine dei contenuti.
2. Concedere ad AEM Sites Optimizer l’accesso all’origine contenuto.

### Passaggio 1: collegare l’archivio del codice e l’origine contenuto

In AEM Sites Optimizer, passa a **Impostazioni → Connetti ad AEM Sites** e inserisci quanto segue:

- **URL archivio codice**: l’URL GitHub del sito EDS, ad esempio:
  `https://github.com/owner/repo`

- **URL origine contenuto**: l’URL della cartella SharePoint o della cartella Google Drive che supporta il sito EDS, ad esempio:
  `https://drive.google.com/drive/folders/...` oppure `https://myorg.sharepoint.com/...`

Dopo aver inserito l’URL dell’origine contenuto, AEM Sites Optimizer rileverà il tipo di origine contenuto e mostrerà le istruzioni di accesso pertinenti di seguito.

### Passaggio 2: concedere l’accesso all’origine contenuto

Segui la sezione che corrisponde all’origine contenuto.

#### SharePoint — Dominio Adobe

![Connessione alla finestra di dialogo di AEM Sites che non mostra alcuna azione richiesta per il dominio Adobe SharePoint](./assets/settings/connect-content-and-drive.png){align="center"}

Se l’URL dell’origine contenuto utilizza il dominio Adobe SharePoint, non è necessaria alcuna ulteriore azione. L’accesso è già configurato. Fai clic su **Salva** per completare la connessione.

#### SharePoint — Dominio personalizzato

Se l’URL dell’origine contenuto utilizza il dominio SharePoint della tua organizzazione, devi registrare un’applicazione Azure e fornire le relative credenziali ad AEM Sites Optimizer.

##### Di cosa avrai bisogno

- Autorizzazione a registrare applicazioni nel portale di Azure o un contatto che può registrare applicazioni per tuo conto.
- I diritti di amministratore tenant per concedere il consenso API o un amministratore che può approvare il consenso API per tuo conto.

##### Passaggio 2a: registrare un’applicazione in Azure

1. Passa a **Portale di Azure → Microsoft Entra ID → Registrazioni app → Nuova registrazione**.
2. Assegna un nome, ad esempio: `AEM Sites Optimizer`.
3. Lascia tutte le altre impostazioni predefinite e fai clic su **Registra**.
4. Nella pagina **Panoramica**, annota:
   - **ID applicazione (client)**
   - **ID directory (tenant)**

##### Passaggio 2b: aggiungere le autorizzazioni API

1. Passa a **Autorizzazioni API → Aggiungi autorizzazione → Microsoft Graph → Autorizzazioni applicazione**.
2. Aggiungi entrambe le opzioni seguenti:
   - `Sites.Selected`: accesso con ambito a raccolte siti di SharePoint specifiche.
   - `Files.SelectedOperations.Selected`: accesso ai file senza un utente connesso.
3. Fai clic su **Concedi consenso amministratore** per entrambi.

![Autorizzazioni API di Azure che mostrano Sites.Selected e Files.SelectedOperations.Selected concesse](./assets/settings/app-permissions.png){align="center"}

>[!NOTE]
>
>La concessione del consenso amministratore richiede i diritti di amministratore tenant. In caso contrario, chiedi all’amministratore IT o di Azure di completare questo passaggio prima di procedere.

##### Passaggio 2c: creare un segreto client

![Pagina certificati e segreti Azure per la registrazione dell’app](./assets/settings/create-credentials.png){align="center"}

1. Pass a **Certificati e segreti → Nuovo segreto client**.
2. Imposta una descrizione e una scadenza, quindi fai clic su **Aggiungi**.
3. Copia immediatamente il valore del segreto perché viene visualizzato una sola volta.

##### Passaggio 2d: concedere all’app l’accesso al sito SharePoint

Puoi concedere l’accesso all’app utilizzando le chiamate API di Microsoft Graph Explorer, PowerShell o Graph dirette.

Passa a [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), accedi con il tuo account Microsoft ed esegui queste richieste:

1. Ricerca l’ID del sito:

```
GET https://graph.microsoft.com/v1.0/sites/{tenant}.sharepoint.com:/sites/{site-name}
```

1. Copia `id` dalla risposta, quindi concedi l’accesso a livello di sito:

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

##### Passaggio 2e: inserire le credenziali in AEM Sites Optimizer

![Finestra di dialogo Connetti ad AEM Sites con i campi delle credenziali di SharePoint](./assets/settings/add-sharepoint-credentials.png){align="center"}

Torna nella finestra di dialogo **Connetti ad AEM Sites**, inserisci quanto segue in **Connessione all’archivio dei contenuti tramite SharePoint**:

- **ID tenant (Azure AD)**: da Registrazione app → Panoramica.
- **ID client (registrazione app)**: da Registrazione app → Panoramica.
- **Segreto client**: creato nel passaggio 2c.

Fai clic su **Convalida connessione** per confermare l’accesso, quindi fai clic su **Salva**.

#### Google Drive

![Finestra di dialogo Connetti ad AEM Sites che mostra l’account del servizio Google Drive per l’accesso condiviso](./assets/settings/validate-eds-google.png){align="center"}

1. In Google Drive, fai clic con il pulsante destro del mouse sulla cartella che supporta il sito EDS e seleziona **Condividi**.
2. Nel campo **Aggiungi persone e gruppi**, inserisci l’e-mail dell’account del servizio visualizzata nella finestra di dialogo **Connetti ad AEM Sites**:
   `aem-sites-optimizer@adbe-gcp0843.iam.gserviceaccount.com`
3. Imposta il livello di autorizzazione su **Editor**.
4. Deseleziona **Notifica alle persone** e fai clic su **Condividi**.

Al termine della condivisione, fai clic su **Convalida connessione** nella finestra di dialogo, quindi fai clic su **Salva**.

## Gestire le autorizzazioni utente

Controlla chi può accedere a un sito in Sites Optimizer e cosa può farci. L&#39;accesso è basato su un piccolo insieme di *funzionalità indipendenti*, ovvero visualizzazione, modifica, distribuzione, configurazione e gestione degli utenti, concesse a ogni utente.

L&#39;accesso è **additivo**: le autorizzazioni di una persona sono la somma di tutto ciò che le è stato concesso. Non c&#39;è &quot;negazione&quot;, quindi le sovvenzioni non entrano mai in conflitto o si annullano a vicenda. Per concedere a un utente un accesso inferiore, rimuovi una sovvenzione anziché tentare di sovrascriverla.

### Come viene concesso l’accesso

Ci sono due modi in cui una persona può accedere, e lavorano insieme:

- **Accesso a livello di organizzazione** — assegnato dall&#39;amministratore dell&#39;organizzazione Adobe in [Adobe Admin Console](https://adminconsole.adobe.com/). Si applica a tutti i siti dell’organizzazione. Utilizzalo per le persone che hanno bisogno dello stesso accesso ovunque.
- **Accesso a livello di sito** — assegnato all&#39;interno di Sites Optimizer, nella pagina **Impostazioni → autorizzazioni**. Si applica a un singolo sito e può essere ampio o stretto come è necessario. Non è richiesto alcun accesso ad Admin Console.

>[!NOTE]
>
>I due livelli si sommano. Un utente con un accesso di visualizzazione a livello di organizzazione che dispone anche della possibilità di modificare le modifiche in un sito può visualizzare tutti i siti e modificarli. Per limitare una persona a un singolo sito, accertati che non svolga anche un ruolo a livello di organizzazione.

#### Ruoli a livello di organizzazione (Admin Console)

L&#39;accesso a livello di organizzazione proviene da uno dei due ruoli di prodotto **AEM Sites Optimizer**, assegnati in [Adobe Admin Console](https://adminconsole.adobe.com/):

- **ASO Manager**: accesso completo a ogni sito, inclusi **Gestione utenti**. Un manager può aprire la pagina **Autorizzazioni** per qualsiasi sito e assegnare l&#39;accesso ad altri.
- **Utente ASO**: accesso in sola visualizzazione a ogni sito. Nessuna modifica e nessuna gestione degli utenti.

Per assegnare un ruolo, devi essere un **amministratore di sistema** per l&#39;organizzazione o un **amministratore di prodotto** per AEM Sites Optimizer.

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/).
1. Vai a **Prodotti** e seleziona **AEM Sites Optimizer**.
1. Apri la scheda **Utenti** e aggiungi l&#39;utente tramite e-mail (o seleziona un utente esistente).
1. Fai clic sull&#39;icona **+** (aggiungi) per aggiungere un profilo di prodotto, quindi scegli il profilo di prodotto.

   ![Scelta del profilo di prodotto per un utente in Adobe Admin Console](./assets/settings/permissions-admin-console-product-profile.png){align="center"}

1. Fai clic su **Avanti**.
1. Scegliere il ruolo **ASO Manager** per l&#39;accesso completo o **ASO Utente** per l&#39;accesso in sola visualizzazione, quindi fare clic su **Applica**.

   ![Selezione del ruolo Responsabile ASO in Adobe Admin Console](./assets/settings/permissions-admin-console-aso-manager-role.png){align="center"}

   ![Selezione del ruolo utente ASO in Adobe Admin Console](./assets/settings/permissions-admin-console-aso-user-role.png){align="center"}

Per ulteriori informazioni sull&#39;aggiunta di utenti, vedere [Utenti integrati](setup/onboard-users.md).

>[!IMPORTANT]
>
>Solo un amministratore dell&#39;organizzazione può concedere **Gestione utenti** a livello di organizzazione. Un membro con **Gestione utenti** in un sito può assegnare l&#39;accesso a tale sito, ma non può creare un **ASO Manager** a livello di organizzazione.

### Livelli di funzionalità

Ogni funzionalità controlla un tipo di azione. Sono indipendenti: ad esempio, è possibile concedere la distribuzione senza modificarla.

| Funzionalità | Cosa consente | Cosa non consente |
|---|---|---|
| Visualizzazione | Visualizzare i dati del sito, ovvero opportunità, suggerimenti, correzioni, rapporti e configurazioni, senza apportare alcuna modifica. | Qualsiasi cambiamento. |
| Modifica | Creare e modificare opportunità e suggerimenti (cosa dovrebbe cambiare). | Pubblicazione delle modifiche, modifica delle impostazioni o gestione degli utenti. |
| Distribuzione | Pubblicare le correzioni sul sito in tempo reale e riportarle indietro. | Gestione degli utenti. |
| Configurare | Modificare le impostazioni e le connessioni del sito. | Pubblicazione delle correzioni o gestione degli utenti. |
| Gestisci utenti | Concedere o revocare l&#39;accesso al sito ad altri membri. | Gestione di un sito a cui la persona non ha già accesso. |

>[!NOTE]
>
>**Visualizzazione sempre inclusa.** Ogni sovvenzione include la visualizzazione automatica: non è possibile gestire, configurare, modificare o distribuire qualcosa che non è possibile visualizzare. Per questo motivo, non è possibile rimuovere la visualizzazione da sola. Per rimuovere completamente l&#39;accesso di un utente, rimuovere il membro (vedere [Modificare o rimuovere un membro](#edit-or-remove-a-member) di seguito) invece di deselezionare ogni funzionalità.

### Limitare l’accesso ai tipi di opportunità

In un singolo sito è possibile concedere la visualizzazione, la modifica e la distribuzione per **tipi di opportunità specifici** (ad esempio, Core Web Vitals o collegamenti interni interrotti) anziché per l&#39;intero sito. Ciò consente a una persona di modificare Core Web Vitals visualizzando solo tutto il resto.

- **Visualizza**, **Modifica** e **Distribuisci** possono avere ambito su uno o più tipi di opportunità o su **Tutti** tipi di opportunità.
- **Configura** e **Gestisci utenti** si applicano sempre all&#39;intero sito, non possono essere limitati a un tipo di opportunità.

Ogni concessione con ambito viene visualizzata come riga del membro, con una colonna **Si applica a** che mostra il tipo di opportunità, **Tutti**, o **A livello di sito**.

>[!CAUTION]
>
>L&#39;ambito limita solo ciò che la concessione *che* concede, non rimuove mai l&#39;accesso fornito da un&#39;altra concessione. Se una persona dispone anche di un accesso a livello di organizzazione o di una concessione di **Tutti** i tipi sono ancora validi. Quindi, per limitare realmente qualcuno a specifici tipi di opportunità, assicurati che non abbiano anche un ruolo più ampio o una sovvenzione di **Tutti** i tipi.

### Aggiungi un membro

1. Vai a **Impostazioni → autorizzazioni** e seleziona il sito.
1. Fare clic su **Aggiungi membri**.
1. Cerca per nome o e-mail e seleziona una o più persone.
1. Scegli i **tipi di opportunità** a cui si applica l&#39;accesso (o **Tutti**), quindi seleziona le funzionalità da concedere.
1. Fai clic su **Aggiungi**.

<!-- MEDIA PENDING: Site Manager / Site User walkthrough videos are being re-recorded with demo data to remove PII, then re-uploaded to video.tv.adobe.com and embedded here with >[!VIDEO]. The earlier uploads v/3503767 and v/3503768 (KT-22672 / KT-22673) contain PII and must not be used. -->

### Modificare o rimuovere un membro

Nella tabella **Membri**:

- Fai clic su **Modifica funzionalità** nella riga di un membro per modificare le operazioni che è in grado di eseguire. Quando si modifica una sovvenzione esistente, il relativo tipo di opportunità rimane fisso: vengono modificate solo le funzionalità e almeno una funzionalità deve rimanere selezionata.
- Fare clic su **Rimuovi** per revocare completamente l&#39;accesso del membro al sito.

>[!NOTE]
>
>La modifica delle funzionalità e la rimozione di un membro sono azioni diverse. Per rimuovere tutti gli accessi, utilizzare **Rimuovi**. Non è possibile deselezionare le funzionalità, perché una sovvenzione deve mantenere almeno una funzionalità (e la visualizzazione rimane sempre).

### Chi può gestire le autorizzazioni

La pagina **Autorizzazioni** per un sito è disponibile per:

- Membri con la funzionalità **Gestione utenti** nel sito e
- Amministratori dell’organizzazione (un responsabile ASO).

I membri senza **Gestione utenti** visualizzano un messaggio che indica che non dispongono delle autorizzazioni necessarie per gestire l&#39;accesso al sito.

### Attivare la gestione degli utenti e degli accessi

La gestione degli utenti e degli accessi è controllata da un’impostazione per la tua organizzazione. Puoi assegnare l&#39;accesso prima che sia attivato, ma solo **imposto** una volta che l&#39;impostazione è attiva.

Se non è ancora abilitata, nella pagina **Autorizzazioni** viene visualizzato un banner in cui viene richiesto di contattare il team dell&#39;account. Rivolgiti al team del tuo account Sites Optimizer per accenderlo.

>[!NOTE]
>
>Fino a quando la gestione degli utenti e degli accessi non viene attivata, le autorizzazioni assegnate vengono salvate ma non applicate.

### Domande frequenti

**I membri a livello di sito hanno bisogno di un ruolo Admin Console?**

No. L&#39;accesso a livello di sito viene concesso interamente in Sites Optimizer, nella pagina **Autorizzazioni**. In Admin Console vengono assegnati solo ruoli a livello di organizzazione.

**Cosa succede se un utente dispone di accesso sia a livello di organizzazione che a livello di sito?**

Si applicano entrambi. Il loro accesso effettivo è la combinazione dei due. Le concessioni non entrano mai in conflitto, poiché nessuna di esse può negare l’accesso.

**Perché un membro con utenti Manage non può creare un manager a livello di organizzazione?**

La creazione di un ruolo a livello di organizzazione è un’azione di Admin Console. Un membro con **Gestione utenti** può assegnare l&#39;accesso al proprio sito, ma solo un amministratore dell&#39;organizzazione può concedere ruoli a livello di organizzazione.

**Come posso revocare l&#39;accesso di un utente a un sito?**

Rimuovi la loro concessione sulla pagina **Autorizzazioni**. Questa funzione è diversa dalle funzionalità di editing, che devono sempre lasciare almeno una funzionalità.

**È possibile limitare una persona a tipi di opportunità specifici?**

Sì: concedere la visualizzazione, la modifica o la distribuzione con ambito a tipi di opportunità specifici anziché **Tutti**. Poiché l&#39;accesso è additivo, ha effetto solo se la persona non dispone anche di un accesso a livello di organizzazione o di una concessione di tipo **Tutti**.

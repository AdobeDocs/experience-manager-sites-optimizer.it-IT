---
name: experience-league-video-upload
description: Utilizza quando un utente desidera inviare/caricare un video in Experience League (video.tv.adobe.com / Invio video KT) per incorporarlo tramite >[!VIDEO] nel markdown di questo archivio; copre la compilazione del modulo di invio con l’automazione del browser, le impostazioni predefinite di questo archivio e ciò che non deve mai essere automatizzato.
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# Caricamento video Experience League

## Panoramica

I video Experience League non sono ospitati in questo archivio. Un `.mp4` locale viene caricato tramite un modulo di invio separato, che restituisce un URL `video.tv.adobe.com` da incorporare con `>[!VIDEO](...)` (vedi [[experience-league-markdown]]). Questa abilità riempie il modulo tramite automazione del browser, fino a (non incluso) allegare il file e inviare.

Modulo: https://81368-exlmpcvideoupload.adobeio-static.net/#/

## Raccomandazioni per file video

Prima che l&#39;utente registri o selezioni un clip, consiglia di usare le proporzioni **16:9** con una risoluzione massima di **1920 x 1080 pixel**: questo è il requisito dichiarato del modulo, non solo una preferenza di stile. Menzionalo in modo proattivo (ad es. quando un utente dice che sta per acquisire una registrazione dello schermo per questo), non solo su richiesta.

## Regola rigida: non allegare mai il file o inviare

L&#39;invio crea un vero e proprio ticket KT Jira e carica sulla piattaforma video di produzione: un&#39;azione rivolta verso l&#39;esterno, difficile da invertire. **Interrompi sempre** una volta compilato ogni altro campo e riconsegna all&#39;utente il file video e il clic finale per l&#39;invio, anche se non ripetono l&#39;istruzione la prossima volta. Questa è l’impostazione predefinita per questa abilità, non è un elemento che deve essere riconfermato per richiesta; salta questa interruzione solo se l’utente dice esplicitamente di inviarli per la stessa richiesta.

## Prerequisiti

Richiede il server MCP `chrome-devtools`, che è **not** impegnato in questo repository (un MCP di automazione browser non deve essere forzato su ogni collaboratore). Se non è caricato:

1. Crea `.mcp.json` nella directory principale dell&#39;archivio:

   ```json
   {
     "mcpServers": {
       "chrome-devtools": {
         "command": "npx",
         "args": ["-y", "chrome-devtools-mcp@latest", "--accept-insecure-certs", "--no-usage-statistics"]
       }
     }
   }
   ```

2. Aggiungi `.mcp.json` a `.gitignore` (strumenti personali, non condivisi).
3. In `.claude/settings.local.json`, aggiungere `"enableAllProjectMcpServers": true` e `"enabledMcpjsonServers": ["chrome-devtools"]`.
4. Chiedere all&#39;utente di riavviare Claude Code (o di eseguire `/mcp`). I server MCP vengono caricati solo all&#39;avvio. Questa operazione non può essere eseguita a metà sessione.

## Valori predefiniti dell’archivio

A meno che l’utente non dica diversamente, utilizza:

| Campo | Predefiniti | Perché |
|---|---|---|
| Cloud | `Experience Cloud` | - |
| Prodotto | `AEM` | Impostazione predefinita specificata dall&#39;utente per questo repository (il modulo elenca anche `AEM as a Cloud Service` — non sostituirlo a meno che non venga richiesto) |
| Sottoprodotto | `AEM Sites` | Corrispondenza più vicina; il modulo non contiene alcuna voce &quot;Sites Optimizer&quot; |
| Ruoli | `User` | I contenuti di verifica preliminare/Sites Optimizer sono destinati agli autori/esperti di marketing, non agli amministratori/sviluppatori, a meno che il video non sia chiaramente destinato a un pubblico tecnico |
| Livelli abilità | `Beginner` | A meno che il flusso di lavoro mostrato non presenti prerequisiti reali |
| Genere voce/e video | `No voices` | Solo per le registrazioni con schermo silenzioso: chiedere se la clip contiene narrazioni |
| Tipo di video | Chiedi o deduci dal contenuto | Le opzioni live sono `Event` / `Feature` / `Technical` / `Value`. La procedura dettagliata dell&#39;interfaccia utente è in genere `Feature` |
| E-mail | qualunque cosa sia preriempita | Il modulo compila automaticamente l’e-mail Adobe dell’utente connesso; non sovrascriverla |

## Passaggi

1. `mcp__chrome-devtools__new_page` all&#39;URL del modulo.
2. `mcp__chrome-devtools__take_snapshot` e attendi (`mcp__chrome-devtools__wait_for` il `"Title"`) il completamento del caricamento dei dati del modulo. Verrà avviato il &quot;Caricamento dei dati del modulo...&quot; girare.
3. Riempi **Titolo** e **Descrizione** — La descrizione è una casella di testo RTF contenteditable, non un `<textarea>` semplice. `fill`/`fill_form` su di esso silenziosamente no-ops (il valore non prende e l&#39;errore &quot;obbligatorio&quot; rimane). Invece: `click` deve mettere a fuoco, quindi `mcp__chrome-devtools__type_text` con il testo.
4. I menu a discesa (**Tipo video**, **Genere voci video**, **Cloud**, **Prodotto**, **Sottoprodotto**, **Nome evento**) sono pulsanti listbox personalizzati, non `<select>` nativi. Per ogni: `click` il pulsante per aprirlo, leggere le opzioni reali dallo snapshot (sono caricate dall&#39;API — non presumere che l&#39;ortografia esatta delle opzioni della tabella predefinita sia ancora corrente), quindi `click` il `option` corrispondente.
5. **Prodotto** e **Sottoprodotto** sono disattivati finché non viene impostato il relativo campo padre (prodotto necessario per il cloud; prodotto richiesto per il sottoprodotto). Compilarli in tale ordine.
6. **I ruoli** e **i livelli di abilità** sono gruppi di caselle di controllo. `fill_form` con `"value": "true"` nella casella di controllo `uid` funziona correttamente qui (a differenza del campo di descrizione).
7. Fermatevi. Acquisisci una schermata, riepiloga cosa è stato impostato e perché (in particolare eventuali impostazioni predefinite sostituite, come Prodotto/Sottoprodotto), e indica all’utente di allegare il video e inviarsi.
8. Dopo che l&#39;utente ha dichiarato di aver inviato, chiedere l&#39;URL video MPC di Adobe risultante (visualizzato nel modulo dopo il caricamento, ad esempio `https://video.tv.adobe.com/v/3496629?learn=on`). Utilizzalo per compilare il codice breve `>[!VIDEO](...)` ovunque questo video debba andare, non fabbricare o indovinare l&#39;URL/ID.

## Convalida di un URL video restituito

Ogni volta che un utente ti consegna un URL video da incorporare (passaggio 8 qui sopra o in qualsiasi altro momento):

- **Rifiuta qualsiasi elemento non presente in `video.tv.adobe.com`.** I video devono essere ospitati per [[experience-league-markdown]] — un collegamento ad YouTube, un host di file o qualsiasi altro dominio non è una destinazione `>[!VIDEO]` valida. Indica all’utente di dover passare prima attraverso il flusso di caricamento di questo archivio; non incorporarlo.
- **Se l&#39;URL `video.tv.adobe.com` è valido e manca `&enablevpops`, aggiungilo** prima di incorporarlo (corrisponde alla convenzione già utilizzata da ogni altro `>[!VIDEO]` in questo repository — vedi `help/home.md`, `help/documentation/trial.md`, ecc.). Aggiungi `&enablevpops` se esiste già un `?`, altrimenti `?enablevpops`.

## Errori comuni

- Tentativo di `fill`/`fill_form` nel campo Descrizione e spostamento in corso quando il banner di errore visualizza ancora &quot;È richiesta una descrizione&quot;. — controlla l&#39;elenco degli errori dopo ogni passaggio, non solo alla fine.
- Tentativo di estrarre il testo dell&#39;opzione dal menu a discesa dalla memoria invece di aprirlo — i valori effettivi (ad esempio `No voices` per il sesso della voce, `Feature`/`Technical`/`Value` per il tipo di video, la suddivisione AEM/AEM-as-a-Cloud-Service in Prodotto) non sono indovinabili e cambiano indipendentemente da questo documento.
- Fare clic su **Carica video** / allegare un file &quot;per salvare un passaggio all&#39;utente.&quot; Non — vedi Regola rigida qui sopra.

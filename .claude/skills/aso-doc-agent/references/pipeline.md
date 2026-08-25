---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 0%

---
# Agente documento ASO - Pipeline

Con riferimento da `SKILL.md`. Questa è la fonte di verità per l&#39;ordine di esecuzione; SKILL.md è
il riepilogo. Leggi `config.yml` prima di iniziare. Ogni valore in `{braces}` di seguito è un
config.

**Gestione degli errori (si applica a ogni passaggio seguente).** Chiamata strumento/API per errori (autenticazione)
errore, timeout, query non valida, schema imprevisto) non è mai la stessa cosa di un
risultato vuoto legittimo, e non deve mai cadere silenziosamente in un
Ramo &quot;vuoto&quot; o &quot;niente da fare&quot; (ad esempio, &quot;niente da fare qui&quot; del passaggio 1.2, passaggio 3.3
&quot;backlog epico completamente coperto o tutto in volo&quot;). Quando si verificano errori in una chiamata, arresta e registra
errore effettivo nel riepilogo dell’esecuzione invece di continuare come se restituisse correttamente.

## Passaggio 0 — Verifica preliminare

1. `pwd` e il controllo `guidelines.md` + `.claude/skills/aso-doc-agent/config.yml` esistono entrambi. In caso contrario, stop — directory errata.
2. `gh auth status` — confermare che l&#39;account `sandsinh_adobe` disponga di un token valido su questo host. **Non eseguire mai`gh auth switch`**. L&#39;account `gh` attivo a livello di computer viene capovolto come effetto collaterale. In questo modo, qualsiasi altro terminale/processo sul computer verrà automaticamente bloccato sull&#39;account errato per un&#39;esecuzione giornaliera automatica. Eseguire solo l&#39;ambito di questa esecuzione: `export GH_TOKEN=$(gh auth token --user sandsinh_adobe)` una volta all&#39;inizio, quindi ogni chiamata `gh` di seguito utilizza tale token tramite l&#39;env var `GH_TOKEN` indipendentemente dall&#39;account globalmente attivo.
3. `mkdir -p {state_dir}` se mancante.
4. Leggere `{state_dir}/run-state.json` se esiste (altrimenti trattare come `{"runs_completed": 0, "tracked_prs": []}`). `tracked_prs` è l&#39;elenco di `{number, headRefName, key}` di questo agente per le PR aperte, utilizzato solo per rilevare una PR chiusa senza unione (passaggio 1.5), poiché `gh pr list --state open` da solo non può visualizzarla una volta terminata. La tempistica delle richieste multimediali risiede in un file separato, `{state_dir}/media-requests.json` (Passaggio 5) — GitHub e Jira rimangono la fonte di verità per tutto il resto (stato PR, stato del ticket).
5. `--ticket KEY` presente -> salta la selezione automatica del passaggio 3, utilizza direttamente KEY (esegue comunque i passaggi 4-7). In caso contrario, eseguire il prelievo automatico nel passo 3.

## Passaggio 1: riconciliare le esecuzioni precedenti

Esegui questa operazione ogni volta, anche su un’esecuzione con limite impostato o altrimenti vuota.

1. `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json number,url,isDraft,headRefName,title,reviewDecision`
2. **Verifica: ogni PR aperto, ogni esecuzione** (`pr.check_reviews_every_run`):
   - `gh pr view <number> --repo {github.repo} --json reviewDecision,reviews,comments`
   - `reviewDecision == "APPROVED"` -> unisci ora: `gh pr merge <number> --repo {github.repo} --merge`. Verificare che l&#39;unione sia effettivamente arrivata (`gh pr view <number> --json state,mergedAt` — `state == "MERGED"`) prima di trattarla come completata; un rifiuto di ramo protetto o un controllo obbligatorio ancora in sospeso possono lasciare aperta la PR anche dopo la chiamata di `gh pr merge` e che deve essere registrata come errore, non segnalata a Jira come unione (si tratta di una normale unione approvata dall&#39;utente, non basata sul timeout). Al momento dell&#39;unione confermata: commento sul ticket Jira collegato che ha unito, rilascia la PR da `tracked_prs`.
   - `reviewDecision == "CHANGES_REQUESTED"` -> **not** corregge automaticamente la PR in questa versione. Leggi i commenti di revisione (`gh api repos/{github.repo}/pulls/<number>/comments` per i commenti in linea, più il corpo di revisione di livello superiore dal campo `reviews`) ed esegui **Scopri dai commenti** di seguito. Nel riepilogo dell’esecuzione, registra PR come in attesa dell’azione di authoring. Se questa PR è stata `CHANGES_REQUESTED` per più di `pr.stale_after_hours` senza aggiornamento, contrassegnarla come non aggiornata per il gate del cap del passaggio 2: rimane aperta per un utente, ma non occupa più uno slot del cap.
   - Qualsiasi altra operazione (ancora nessuna revisione, `REVIEW_REQUIRED` senza revisione inviata) -> nessuna operazione da eseguire qui.
3. **Impara dai feedback.** Per ogni commento di revisione o corpo di revisione che recita come una nota *generalizzabile* su tono, struttura o contenuto, non una correzione una tantum specifica per tale PR (confronta &quot;menziona sempre la scheda Ignorato per le opportunità con ignora supporto&quot; rispetto a &quot;digita sulla riga 12&quot;), aggiungi una voce datata collegata a un ticket a `references/review-learnings.md`. Salta il feedback puramente meccanico (errori di battitura, collegamenti interrotti, lint) — correggi questi nella PR stessa, non hanno bisogno di una lezione duratura. Il formato di voce esatto è documentato in tale file.
4. Per ogni **bozza** PR nell&#39;elenco, estrarre la chiave Jira dal nome del ramo (`{github.branch_prefix}<KEY>-...`).
   - `mcp__Corp-Jira__list_attachments` + `mcp__Corp-Jira__get_jira_comments` su quella chiave.
   - Cerca: un nuovo allegato immagine che corrisponde all&#39;acquisizione richiesta, OPPURE un commento contenente un URL `video.tv.adobe.com`.
   - Se viene trovato: `git fetch`/`checkout` il ramo, aggiungere l&#39;immagine a `help/**/assets/` (se si tratta di un allegato immagine, scaricare tramite `download_attachment`) o riempire il segnaposto `>[!VIDEO](...)` (se un commento URL video), convalidare rispetto a `experience-league-markdown`, eseguire il commit, inviare il messaggio push, `gh pr ready <number>`, commento sulla PR &quot;Contenuto multimediale aggiunto — pronto per la revisione.&quot;, aggiornare la voce `{state_dir}/media-requests.json` a `resolved`.
   - Se non viene trovato: controllare il tempo trascorso dalla richiesta in `{state_dir}/media-requests.json`. Applica la logica di escalate/Give-up anche qui dal passaggio 5 (una bozza di PR lasciata aperta in più esecuzioni necessita ancora dei suoi media chased) — inclusa la chiamata `gh pr ready` del percorso rinunciato, in modo che una bozza data-up diventa ancora rivedibile invece di rimanere bloccato.
5. **Rileva PR chiusi senza unire.** Confrontare l&#39;elenco Open-PR di questa esecuzione (passaggio 1) con `tracked_prs` di `run-state.json`. Qualsiasi PR tracciato mancante dall&#39;elenco aperto e non confermato unito nel passaggio 2, è stato chiuso senza unire. Prima di eliminarlo, recuperane lo stato finale (`gh pr view <number> --repo {github.repo} --json reviews,comments`) ed esegui **Scopri dal feedback** su di esso un&#39;ultima volta, in modo che il ragionamento di rifiuto di un utente non vada perduto. Quindi rilascialo dal tracciamento. Non sono necessarie ulteriori azioni sul ticket stesso: poiché l’etichetta della richiesta di rimborso è applicata solo al momento della pubblicazione (passaggio 6.10), un ticket chiuso non unito non ha già un’etichetta e gli assegni della fase 3.2 (nessuna PR aperta/unita) lo rendono naturalmente idoneo per essere scelto di nuovo in una esecuzione futura.
6. Impostare `tracked_prs` in `run-state.json` sull&#39;elenco Open-PR corrente (`number`, `headRefName` e la chiave Jira analizzata dal nome del ramo) per il passaggio 5 dell&#39;esecuzione successiva su diff.

## Passaggio 2 — cancello del cappuccio PR

1. Conta PR aperte dall&#39;output `gh pr list` del passaggio 1, escludendo qualsiasi PR contrassegnato nel passaggio 1.2 come non aggiornato-`CHANGES_REQUESTED` (aperto più di `pr.stale_after_hours` senza aggiornamento). Tali PR rimangono aperte per un utente umano ma non occupano più uno slot di chiusura.
2. Se count >= `{pr.max_open}` (3): log `"cap reached ({count}/{pr.max_open} open) — skipping new ticket this run"`, passare al passaggio 7.
3. Altrimenti, continuare con il passaggio 3.

## Passaggio 3 — Scegliere un ticket

Ignora completamente se `--ticket KEY` è stato passato (usa KEY).

```
JQL: "Epic Link" = {jira.epic} AND status = "{jira.open_status}"
     ORDER BY priority DESC, created ASC
```

1. Eseguire la ricerca (`mcp__Corp-Jira__search_jira_issues`, `minimizeOutput: true`, campi limitati a `key,summary,priority,status,labels`).
2. Camminare risulta in ordine. Ignora qualsiasi ticket che:
   - ha già l&#39;etichetta `{jira.picked_label}`, OPPURE
   - ha già un ramo `{github.branch_prefix}<KEY>-*` esistente sul remoto (`git ls-remote --heads origin '{github.branch_prefix}<KEY>-*'`), OPPURE
   - ha già un PR aperto o unito (verifica incrociata con l&#39;elenco del passaggio 1 / `gh pr list --state all --search <KEY>`).
3. Il primo biglietto che supera tutti e tre i controlli è la scelta. Se nessuno passa **perché la ricerca ha effettivamente restituito zero ticket idonei**, registra `"epic backlog fully covered or all in flight"` e passa al passaggio 7. Se la ricerca stessa non è riuscita (errore di autenticazione, timeout, JQL in formato non valido), in questo caso non si verifica alcun errore, registrare l’errore effettivo (vedi Gestione degli errori sopra).
4. **non** ancora etichettare il ticket. L&#39;etichetta di attestazione viene applicata al passaggio 6.10 solo una volta che esistono effettivamente un ramo e una PR. I passaggi 4-5 (ricerca/bozza/media) possono fallire o bloccarsi senza lasciare alcuna traccia sul ticket; gli unici segnali in corso prima del passaggio 6 sono i controlli di esistenza/PR di cui sopra, che è sufficiente dato che si esegue da una singola macchina senza alcuna concorrenza reale da evitare.

## Fase 4 — Ricerca + bozza

La ricerca viene prima ed è **multi-source** — mai bozza da un singolo input (Jira
biglietto da solo, o solo leggere documenti di pari livello). Ogni sorgente qui sotto conferma o
corregge gli altri; le contraddizioni si risolvono fidandosi del codice sorgente > documenti Wiki/PR >
Discussione su Slack > l’inferenza dello stesso autore della documentazione, in tale ordine, e contrassegnati in linea
come `<!-- CONFIRM -->` quando non possono essere risolti.

&#x200B;0. **Lezioni di revisione accumulate.** Leggi prima `references/review-learnings.md`. Applica tutto ciò che è rilevante per l’argomento di questo ticket prima della stesura: in questo modo il feedback dalle passate revisioni di PR migliora le bozze future invece di ripetere la stessa correzione.

### Ricerca (fare tutto ciò che si applica — non saltare direttamente alla stesura)

1. **Codice Source (verità di fondo per il funzionamento effettivo).** Cercare nell&#39;archivio primario dell&#39;interfaccia utente (`research.code_repos` in config.yml) l&#39;adapter/handler della funzionalità (`*OpportunityAdapter.tsx`, `*SuggestionAdapter.tsx`), il relativo hook dati (`use*Data.ts`) e le stringhe titolo/descrizione `.l10n.ts`/`.I10n.ts`. Questa è l&#39;autorità per i nomi dei campi, la forma dei dati, la categoria e la copia esatta del prodotto, preferendola a qualsiasi altra cosa quando le fonti non sono d&#39;accordo.
2. **Wiki (finalità di progettazione, specifiche, decisioni).** `mcp__Adobe-Wiki__search_wiki_content` con il nome della funzionalità/opportunità e la chiave epic/ticket. Leggi le pagine corrispondenti (`get_wiki_content`) per: perché la funzione esiste, terminologia utilizzata dal team di prodotto, eventuali casi documentati di flusso UX o edge case ed eventuali schermate incorporate che stabiliscono l&#39;aspetto dell&#39;interfaccia utente reale (informa la specifica di acquisizione dei contenuti multimediali nel passaggio 5, non sostituisce una nuova schermata effettiva a meno che la pagina non sia corrente).
3. **Slack (informazioni sul team, domande aperte, modifiche recenti).** `mcp__Slack__slack_search_messages` con il nome della funzionalità/opportunità e la chiave del ticket, senza restrizioni per canale, a meno che `research.slack_channels` non la riduca in config.yml. Cerca: messaggi di annuncio (spesso con la cornice pulita per il cliente), thread di discussione di progettazione e qualsiasi cosa indichi che la funzione è stata modificata di recente in modo che i documenti di pari livello o i commenti al codice non riflettano ancora.
4. **Cronologia PR su GitHub (logica di implementazione, schermate, discussione sulla revisione).** `gh search prs --repo <repo> "<feature name>"` o `gh pr list --repo <repo> --search "<ticket key OR feature name>" --state all` in `research.code_repos`. Leggi le descrizioni PR unite per motivazioni, documenti di progettazione collegati e schermate che chiariscono il comportamento che il codice da solo non spiega (ad esempio perché viene assegnato un tipo di correzione, come si presenta una maiuscola/minuscola nell’interfaccia utente).
5. **Analoghi tono.** In base al riepilogo dei ticket, individua le pagine esistenti più vicine tra 2 e 3:
   - &quot;... ticket di apprendimento opportunità -> leggi 2 file di pari livello in `help/documentation/opportunities/` (l&#39;effettivo percorso di apprendimento per opportunità - `help/opportunity-types/*.md` sono le pagine di destinazione della categoria con griglie di schede collegate a queste, non il contenuto di apprendimento stesso).
   - Impostazioni/flusso di lavoro/ticket di connessione -> lettura di 1-2 file di pari livello in `help/documentation/` (verifica la corrispondenza più simile in `setup/`, `opportunities/`, `settings.md`, `basics.md`).
     Struttura del titolo dello specchio, utilizzo della casella delle note, lunghezza della frase, livello di dettaglio tecnico.
6. **Formatta regole.** Rileggi la Guida di riferimento rapido dell&#39;abilità `experience-league-markdown` prima di scrivere. Ogni intestazione/nota/immagine/collegamento deve corrispondere esattamente alla relativa sintassi.

### Bozza

&#x200B;7. **Decisione sul file di destinazione.** Preferisci estendere la sezione pertinente di una pagina esistente anziché creare un nuovo file, A MENO che il ticket non corrisponda alla granularità delle pagine autonome esistenti (ad esempio, ogni opportunità ottiene il proprio file in `help/documentation/opportunities/`, un nuovo file segue esattamente la struttura di un pari livello esistente). Quando estendi una pagina esistente, tocca solo una sezione per questo ticket: non modificare le sezioni non correlate anche se sembrano obsolete. Se si tratta di una nuova pagina autonoma, aggiungere anche la relativa scheda alla relativa pagina di destinazione `help/opportunity-types/*.md` (elenco dei commenti di origine + blocco HTML generato, corrispondente al pattern esatto delle schede esistenti) e registrarla in `help/main-toc/TOC.md`.
&#x200B;8. **Bozza v1.** Scrivere il contenuto ora (in memoria/scratch, non ancora nel file repo), come avviene nel passaggio 6 dopo la decisione relativa al supporto, in modo che un documento in attesa di supporto e un documento risolto dal supporto passino attraverso lo stesso percorso di scrittura. Sintetizza tutti i passaggi da 1 a 6: non aggiornare solo la descrizione del ticket Jira.
&#x200B;9. **Itera.** Rilegga il draft v1 contro ogni risultato di ricerca dei passaggi 1-4: il draft ha saltato qualcosa che è emerso in Slack o Wiki? Non contraddice quello che fa il codice sorgente? Corrisponde il più possibile al tono di parentela? Rivedi prima di andare avanti — questo è un vero secondo passaggio, non una formalità. Qualsiasi cosa ancora genuinamente non confermata dopo questo passaggio (non trovata in nessuna delle quattro sorgenti) ottiene un commento `<!-- CONFIRM -->` in linea piuttosto che una supposizione.
&#x200B;10. **Decisione sui contenuti multimediali.** Decidere `mediaNeeded: true|false`.
    - `true` se la funzionalità è un flusso di lavoro dell&#39;interfaccia utente in più passaggi in cui una sola descrizione testuale sarebbe materialmente più difficile da seguire (corrisponde a &quot;utilizzata in modo giudizioso... quando una descrizione testuale è insufficiente&quot; di `guidelines.md`).
    - Se `true`, produrre: `mediaType` (`screenshot` o `video`), `captureSteps` (passaggi esatti per riprodurre lo stato da acquisire), `urls` (URL dell&#39;app rivolti al cliente e/o URL della pagina interna necessari per raggiungere tale stato — richiamare URL reali dalla descrizione/commenti del ticket Jira, Wiki o `open-aso-devmode-url` convenzioni se vi si fa riferimento; non creare mai un URL).
    - Se `false`, salta il passaggio 5 per questo ticket.

## Passaggio 5 — Media gate

Viene eseguito solo quando il passaggio 4 imposta `mediaNeeded: true`. Tutti i timestamp in
`{state_dir}/media-requests.json` sono UTC ISO-8601 (`date -u +%Y-%m-%dT%H:%M:%SZ`) —
scrivi e confronta sempre in questo formato, in modo che i dati matematici relativi al tempo trascorso riportati di seguito non siano ambigui
tra le esecuzioni.

1. Selezionare `{state_dir}/media-requests.json` per una voce esistente per questa chiave ticket. In caso contrario, si tratta di una nuova richiesta.
2. **Nuova richiesta:**
   - `mcp__Slack__slack_lookup_user` il `media.contacts_in_order[0].email` (sandsinh) per ottenere l&#39;ID utente di Slack.
   - `mcp__Slack__slack_send_dm` con un messaggio contenente: la chiave del ticket Jira + il collegamento, esattamente cosa acquisire (`captureSteps`), gli URL da utilizzare e dove la risposta dovrebbe andare (&quot;rispondi sul ticket Jira — allega direttamente la schermata oppure, per un video, carica tramite il solito modulo video Experience League e incolla il collegamento `video.tv.adobe.com` risultante come commento&quot;).
   - Scrivi `{state_dir}/media-requests.json[KEY] = {requestedTo: "sandsinh", requestedAt: <UTC ISO-8601 now>, escalated: false}`.
3. **Richiesta esistente:** entrambe le soglie seguenti sono misurate dall&#39;originale `requestedAt`. L&#39;escalation non reimposta l&#39;orologio:
   - `now - requestedAt` &lt; `media.escalate_after_hours` -> non eseguire questa esecuzione, procedere alla pubblicazione con i file multimediali ancora in sospeso (bozza PR).
   - `now - requestedAt` >= `media.escalate_after_hours` e non ancora inoltrato -> DM `media.contacts_in_order[1]` (kanishka), è già stato chiesto alle note del messaggio sandsinh N ore fa senza risposta. Voce di aggiornamento: `escalated: true, escalatedAt: <UTC ISO-8601 now>`.
   - `now - requestedAt` >= `media.give_up_after_hours` (indipendentemente dallo stato di escalation) -> imposta `mediaNeeded: false` a scopo di pubblicazione, inserisci una nota in linea nella bozza: `>[!TIP]\n>\n>A screenshot for this step is being added in a follow-up update.` Se per questo ticket esiste già una PR ed è ancora una bozza (raggiunta qui tramite il passaggio 1.4, non una nuova pubblicazione del passaggio 6), `git fetch`/estrai il ramo, applica la nota, esegui il commit, invia e chiama `gh pr ready <number>` — una bozza specificata deve ancora diventare revisionabile, non rimanere bloccata a tempo indefinito. Contrassegna voce `gaveUp: true`.

## Passaggio 6 — Pubblicazione

Ignora se il ticket è stato completamente ignorato nel passaggio 3 (niente da pubblicare).

1. `git fetch origin` e `git checkout -B {github.branch_prefix}<KEY>-<short-slug> origin/main` — `-B` (non `-b`) in modo che un ramo locale rimanente da un&#39;esecuzione precedente in arresto anomalo venga reimpostato anziché bloccare l&#39;estrazione; il ramo direttamente da `origin/main` elimina inoltre qualsiasi stato locale sporco da un arresto anomalo precedente invece di non riuscire su di esso.
2. Scrivere la bozza del passaggio 4 nel file di destinazione deciso nel passaggio 4.3. Ricontrolla riga per riga l&#39;elenco di controllo &quot;Prima di confermare le modifiche Markdown&quot; di `experience-league-markdown`.
3. Se è configurato un linter markdown (`markdownlint_custom.json` nella directory principale dell&#39;archivio) e `markdownlint-cli`/`npx markdownlint` è disponibile, eseguilo in base ai file modificati e correggi eventuali violazioni prima di eseguire il commit.
4. Commit: `docs(aso): <ticket summary, lowercase, no trailing period>\n\nSITES-XXXXX`.
5. `git push -u origin <branch>`.
6. Selezione revisore: `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json reviewRequests` — conteggia quanti revisori attualmente elencano ciascuno dei due revisori configurati; assegna quello che ha meno (cravatta -> `sandsinh_adobe`).
7. Organismo PR:

   ```
   ## Summary
   [1-2 sentence description of the feature now documented]
   
   ## Source
   Closes documentation gap tracked in [SITES-XXXXX](https://jira.corp.adobe.com/browse/SITES-XXXXX)
   
   ## Media
   [either "No media needed for this update." OR "Screenshot/video requested from {contact} on {date} — PR opened as draft until resolved." OR "Media follow-up pending — shipped without it; see inline note."]
   
   > 🤖 Drafted by aso-doc-agent
   ```

8. `gh pr create --repo {github.repo} --title "<ticket summary>" --body "<above>" --label {github.pr_label} --reviewer <chosen-github-handle> --draft` se il supporto è ancora in sospeso, altrimenti omettere `--draft`.
9. `gh pr edit <number> --add-label {github.pr_label}` se il contrassegno dell&#39;etichetta non è stato accettato (cintura e sospensioni, corrisponde al modello utilizzato in un&#39;altra area degli strumenti dell&#39;organizzazione).
10. Jira: `add_jira_comment` collega l&#39;URL PR e ora, per la prima volta in questa esecuzione, aggiungi `{jira.picked_label}` (`update_jira_issue`, unisci con etichette esistenti). Questa è l&#39;affermazione, applicata deliberatamente solo una volta che un ramo e PR esistono entrambi: un incidente ovunque nel passaggio 3-5 lascia il biglietto completamente non etichettato e tranquillamente ri-selezionabile, invece di bloccato permanentemente. Non cambiare lo stato del ticket: lascia che sia il triage del team di documentazione; `{jira.picked_label}` è l&#39;unico segnale di stato scritto dall&#39;agente.

## Passaggio 7 — Eseguire il riepilogo

1. Aggiornamento `{state_dir}/run-state.json`: `runs_completed += 1`, timestamp, ticket selezionato (o &quot;nessuno&quot; + motivo), PR aperto/aggiornato (o &quot;nessuno&quot; + motivo), stato limite.
2. Stampa un breve riepilogo leggibile (ticket, azione intrapresa, collegamento PR, stato dei media).

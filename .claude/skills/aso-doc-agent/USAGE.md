---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---
# Agente documento ASO - Utilizzo

Cos&#39;è, come funziona, e cosa fare quando serve.

## Effetto

Ogni giorno, questo agente sceglie la singola funzione ASO non documentata con priorità più alta da
Backlog di [SITES-49539](https://jira.corp.adobe.com/browse/SITES-49539) (39 ticket, ad esempio
&quot;Canonical chance how-to&quot;, &quot;Slack notifications&quot;), scrive un pezzo di documentazione
per questo repository nello stile di casa, e apre una PR — assegnando uno dei due
i revisori configurati (`sandsinh_adobe` / `kanishka_adobe`) al momento hanno meno aperture
rivedi le richieste di questo agente. Se la funzione richiede uno screenshot o un video, richiede
uno su Slack prima di terminare il PR.

Ogni esecuzione controlla anche lo stato di revisione su ogni PR aperto: le PR approvate vengono unite
immediatamente, e il feedback richiesto dalle modifiche viene letto e, quando si tratta di un
lezione (non un errore di battitura), registrata in modo che le bozze future non ripetano lo stesso errore.

Una esecuzione = una funzione = al massimo una PR. Non tocca mai più di un biglietto per corsa,
e non apre mai più di 3 PR contemporaneamente (attende che quelli esistenti vengano prima uniti/chiusi).

## Dove tutto vive

| Cosa | Percorso |
|---|---|
| Come decide cosa fare | `.claude/skills/aso-doc-agent/SKILL.md` |
| L’esatto passaggio per passaggio | `.claude/skills/aso-doc-agent/references/pipeline.md` |
| Impostazioni specifiche per il team (modificare questa opzione per cambiare i revisori, il limite, la tempistica dell’escalation) | `.claude/skills/aso-doc-agent/config.yml` |
| Lezioni apprese dal feedback di revisione delle PR (tracciato in Git, letto prima di ogni bozza) | `.claude/skills/aso-doc-agent/references/review-learnings.md` |
| Stato di esecuzione locale (ignorato: sicuro da eliminare, verrà ricompilato) | `.claude/skills/aso-doc-agent/state/` |
| Programma di installazione giornaliero | `.claude/scripts/aso-doc-agent-setup.sh` |
| Autorizzazione per l’esecuzione headless di un’operazione di | `.claude/settings.local.json` (gitignorato, locale computer) |

## Esecuzione

- **Manualmente, in una sessione normale:** `/aso-doc-agent` (o `/aso-doc-agent --ticket SITES-XXXXX`)
- **Headless, una tantum:** `claude -p "/aso-doc-agent"` dalla directory principale dell&#39;archivio
- **Giornaliero, automatico:** già installato tramite `launchctl` (vedi sotto) — viene eseguito ogni giorno alle 07:53 ora locale, nessuna azione necessaria

### Installazione/modifica della pianificazione giornaliera

```bash
bash .claude/scripts/aso-doc-agent-setup.sh
```

Installa un processo `launchd` (`~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist`) che
esegue `claude -p "/aso-doc-agent"` da questo repository ogni giorno. Esegui nuovamente lo script ogni volta che
modifica la pianificazione al suo interno (impostazione predefinita: 07:53 locale). Questo funziona solo se il computer è
attivato e sveglio in quel momento: il lancio non esegue retroattivamente i processi saltati, ma viene eseguito
la prossima ora pianificata normalmente.

```bash
launchctl list | grep com.sandsinh.aso-doc-agent   # confirm it's loaded
launchctl start com.sandsinh.aso-doc-agent         # trigger a run right now, don't wait for 07:53
launchctl unload ~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist  # stop it
```

I registri di ogni esecuzione pianificata vengono consegnati in `.claude/skills/aso-doc-agent/state/launchd.out.log`
e `launchd.err.log`.

## Cosa ti verrà chiesto di fare

- **Un DM Slack dall&#39;agente** (inviato come te, prima sandsinh, kanishka su
escalation) la richiesta di uno screenshot o di un video, con i passaggi di acquisizione esatti e gli URL per
utilizzare. **Risposta sul ticket Jira collegato, non in Slack**: allegare direttamente lo screenshot,
o per i video, caricali tramite il solito modulo video di Experience League
(`experience-league-video-upload` abilità) e incolla il risultato `video.tv.adobe.com`
link come commento Jira. L’esecuzione successiva la raccoglie automaticamente.
- Se nessuno risponde entro **5 giorni**, la richiesta passa da sandsinh a kanishka
automaticamente. Dopo **10 giorni** senza alcuna risposta da parte di nessuno dei due agenti, l&#39;agente invia il documento
senza file multimediali e aggiunge una nota in linea. L&#39;unione automatica non è basata su timeout: il PR
attende ancora una vera e propria recensione umana, per quanto tempo ci voglia.
- **PR da rivedere** — assegnato a chi di voi ha meno PR aperti dall&#39;agente
attualmente in attesa di revisione. Le bozze delle PR indicano che i media sono ancora in sospeso; si capovolgono in
pronto per la revisione automaticamente una volta che la risorsa viene visualizzata. Approva e l’agente unisce
alla successiva esecuzione, non è necessario alcun passaggio di unione separato.
- **Se richiedi modifiche**, l&#39;agente legge i tuoi commenti alla prossima esecuzione. Generalizzabile
il feedback (non una correzione di errori di battitura o collegamenti) viene scritto in `references/review-learnings.md` in modo che il
non è necessario ripetere la stessa correzione in una PR futura.

## Regolazione del comportamento

Modifica `.claude/skills/aso-doc-agent/config.yml` (tracciato in Git — le modifiche interessano ogni
esecuzione futura, su questo computer o su chiunque altro cloni l’archivio):

- `pr.max_open` — quante PR aperte prima che l&#39;agente sospenda il prelievo di nuovi ticket (impostazione predefinita: 3)
- `pr.stale_after_hours` — per quanto tempo una PR `CHANGES_REQUESTED` può sedersi prima di smettere di contare verso `pr.max_open` (valore predefinito 336 = 14 giorni); rimane aperta, questo sblocca solo i nuovi prelievi
- `github.reviewers` — Assegnazione e saldo
- `media.contacts_in_order` / `escalate_after_hours` (impostazione predefinita: 120 = 5 giorni) / `give_up_after_hours` (impostazione predefinita: 240 = 10 giorni): chi è il destinatario della richiesta, in quale ordine e con quale pazienza; entrambi vengono misurati dalla richiesta originale; pertanto l&#39;aumento della priorità non comporta l&#39;invio della data di rinuncia
- `pr.check_reviews_every_run` — disattiva il passaggio del controllo revisioni (non consigliato; questo è il modo in cui si verificano le unioni e gli insegnamenti)

## Se si blocca in un prompt di autorizzazione

Le esecuzioni headless (`claude -p`, launchd) non dispongono di un terminale per richiedere l&#39;intervento, una chiamata dello strumento non elencata
fallirà invece di impiccarsi. Se il registro di un&#39;esecuzione mostra un rifiuto di autorizzazione per un comando
la pipeline ha legittimamente bisogno, aggiungilo all&#39;elenco `permissions.allow` in
`.claude/settings.local.json` (non tracciato in Git — locale al computer; ogni sviluppatore in esecuzione
questo agente necessita della propria copia con il proprio ambito (inserisce nell&#39;elenco Consentiti di).

## Se smette completamente di progredire

Seleziona, nell’ordine:
1. `gh pr list --repo Adobe-Enterprise-Docs/experience-manager-sites-optimizer.en --label aso-doc-agent --state open` — se questo mostra 3, è in attesa di recensioni, non bloccato.
2. Jira: è rimasto un ticket `New` idoneo in SITES-49539 che non è già `aso-doc-agent-picked`? L’etichetta viene mai applicata solo una volta che esiste una diramazione+PR (passaggio 6.10 di pipeline.md), pertanto un’esecuzione in arresto anomalo non dovrebbe lasciare un ticket etichettato ma non pubblicato; se ne trovi ancora uno (ad esempio un’etichetta aggiunta a mano), rimuovilo manualmente per rendere nuovamente idoneo il ticket.
3. `.claude/skills/aso-doc-agent/state/launchd.err.log` per l&#39;errore dell&#39;esecuzione più recente.
4. Se il riassunto di una corsa mostra &quot;backlog epico completamente coperto&quot; o &quot;niente da fare qui&quot; ma sai che ci dovrebbe essere lavoro ammissibile, trattalo come sospetto — quei messaggi sono riservati per risultati veramente vuoti. Un errore Jira/GitHub/Slack effettivo viene registrato separatamente e dovrebbe essere visualizzato come una propria riga in `launchd.err.log` invece di nascondersi dietro uno di questi messaggi.

---
description: Converti le note sulla versione interne di ASO sprint in formato Experience League rivolto al cliente e aggiungi alla pagina delle note sulla versione.
source-git-commit: 5f400c37283d1a3d8285b4d2ac5246761a7275e6
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---


# Convertitore note sulla versione

Converte le note sulla versione sprint interne (dal canale Slack `#aem-sites-optimizer-announcements` o dall&#39;output del cursore `.cursor/commands/release-notes`) in una voce visualizzata dal cliente e le aggiunge a `help/documentation/release-notes.md`.

## Utilizzo

Richiama questa abilità, quindi incolla il contenuto delle note sulla versione interne quando richiesto. L’abilità:

1. Applicare le linee guida riportate di seguito per le regole di filtraggio e tonalità.
2. Analizzare le note sulla versione interne (sezioni categorizzate come emoji: ✨ funzionalità, 🚀 miglioramenti, 🤖 IA-First, 🔧 correzioni, 🏢 BackOffice).
3. Escludi tutte le categorie escluse in base alle linee guida (strumenti di intelligenza artificiale, BackOffice, linter di localizzazione, test E2E, SitesElementi solo interni).
4. Riscrivi gli elementi rimanenti nel tono rivolto al cliente utilizzando gli esempi di tono riportati di seguito come riferimento.
5. Raggruppa gli elementi correlati per area capacità (non per team o repository).
6. Formatta come nuova voce di versione seguendo il modello di struttura della pagina riportato di seguito.
7. Anteporre la nuova voce a `help/documentation/release-notes.md` (sopra l&#39;ultima voce precedente, sotto il paragrafo di introduzione della pagina).
8. Stampa una tabella di riepilogo che mostra: elementi conservati, elementi riscritti, elementi eliminati (con il motivo di ogni elemento eliminato).

## Linee guida

### Principi fondamentali

1. **Vantaggi per i clienti.** Ogni voce dovrebbe rispondere a &quot;cosa posso fare ora che non potevo prima, o fare meglio?&quot; — non &quot;che cosa abbiamo spedito?&quot; Lead con il valore, non con l’implementazione.

2. **Tono di leadership.** Scrivi per un decision-maker: risultati e funzionalità, non meccanica tecnica. Un VP dell’esperienza digitale dovrebbe capire immediatamente perché un aggiornamento è importante.

3. **Nessun gergo interno.** Sostituisci tutte le abbreviazioni interne al team:
   - &quot;PLG&quot; → &quot;utenti di prova&quot; o &quot;nuovi clienti&quot;
   - BackOffice → omettere completamente (modifica solo dell&#39;infrastruttura)
   - &quot;MSM&quot; → &quot;AEM Multi-Site Manager&quot;
   - &quot;SHM&quot; → &quot;Monitoraggio integrità sito&quot;
   - &quot;OrcaFix&quot;, &quot;Cursor command&quot;, &quot;AGENTS.md&quot; → omettere completamente
   - &quot;EDS&quot; → &quot;Edge Delivery Services&quot;

4. **Voci brevi.** Una frase di *cosa*, una frase di *perché è importante*. Se entrambi rientrano in una frase, fallo.

5. **Ambito accurato.** Includi solo le modifiche che un cliente vedrà nell’interfaccia o nell’esperienza del prodotto nei suoi flussi di lavoro. Sono escluse l’infrastruttura, gli strumenti e le modifiche all’esperienza degli sviluppatori.

6. **Segnala le funzionalità di Accesso anticipato.** Se una funzione viene fornita dietro un flag di funzione disattivato per impostazione predefinita (consenso per organizzazione/sito, ad esempio tramite LaunchDarkly `FeatureGate`/`isEnabledByDefault={false}`), aggiungi `(Early Access)` al nome della funzione in grassetto, rispecchiando la convenzione `(General Availability)` esistente utilizzata per le funzioni graduate. In caso di dubbi, verifica se la funzione è attiva per impostazione predefinita per tutti i clienti; in caso contrario, si tratta di Accesso anticipato. Verifica in base al flag di funzione predefinito nel codice — non indovinare.

### Modello struttura pagina

Ogni voce della versione segue questa struttura:

```markdown
## [Month Start]–[Day End], [Year]

### New Features

- **[Feature Name]** — [One-sentence benefit statement. One sentence of business context if needed.] (append `(Early Access)` or `(General Availability)` to the feature name when the feature's availability status is notable)

### Enhancements

- **[Enhancement Name]** — [One-sentence improvement statement.]

### Bug Fixes

- [Short description of what was fixed and why it matters to users.]
```

**Regole:**
- Formato intervallo di date: `May 11–22, 2026` (trattino, mese abbreviato, anno di quattro cifre).
- Ordine cronologico inverso: ultima versione nella parte superiore della pagina.
- Includi solo le sezioni con contenuto. Se vuoto, ometti &quot;Miglioramenti&quot; o &quot;Correzioni di bug&quot;.
- Le voci Correzioni di bug non utilizzano nomi di funzionalità in grassetto, ma sono punti elenco semplici.
- Includi correzioni di bug solo in presenza di 3 o più correzioni visibili dall’utente e degne di nota.

### Cosa includere ed escludere

**Includi:**

| Categoria | Esempi |
|---|---|
| Nuovi tipi di opportunità | Mancata corrispondenza dell’intento dell’annuncio, nessun CTA al di sopra del piegatore |
| Nuove visualizzazioni o flussi di lavoro | Scheda Implementato, esportazione CSV, collegamento Jira |
| Miglioramenti di prova/onboarding | Flusso di configurazione guidato, stato senza onboarding del sito |
| Miglioramenti alle impostazioni | Controlla URL di destinazione, configurazione del tipo di consegna |
| Correzioni significative dell’interfaccia utente | Conteggi errati, navigazione interrotta, visualizzazione dei problemi che influiscono sulle decisioni |
| Nuovi dati/integrazioni | Dati Ahrefs in Ricerca organica, albero delle dipendenze in Sicurezza |
| Funzionalità di implementazione per l’authoring | Nuovi tipi di opportunità che supportano la distribuzione diretta |

**Escludi:**

| Categoria | Perché |
|---|---|
| Strumenti di intelligenza artificiale (OrcaFix, comandi Cursor, AGENTS.md, regole Claude Code) | Strumenti per sviluppatori interni, non visibili ai clienti |
| Hook di linter/pre-commit della localizzazione | Processo di progettazione, non una caratteristica di prodotto |
| Modifiche al back office e all&#39;infrastruttura | Non visibile nell’interfaccia utente a meno che non modifichino il comportamento dell’utente finale |
| Aggiornamenti delle versioni di React Spectrum | Dipendenza interna, non visibile all&#39;utente |
| Miglioramenti dei test E2E | Qualità tecnica, non una caratteristica di prodotto |
| Rilasciare l’automazione della pipeline | Processo interno |
| SitesFunzioni solo interne | Non disponibile per i clienti |

### Esempi di tonalità

| Espressione interna | Espressioni rivolte al cliente |
|---|---|
| &quot;È stato introdotto lo stato RIFIUTATO per il flusso di lavoro di convalida manuale&quot; | &quot;È ora possibile contrassegnare i suggerimenti come rifiutati per indicare che non si applicano al sito, mantenendo l’elenco delle opportunità incentrato sugli elementi utilizzabili.&quot; |
| &quot;Visualizzazione distribuita per opportunità Canoniche e Hreflang (raggruppate per data)&quot; | &quot;Le modifiche alle opportunità Canonical e Hreflang ora sono raggruppate per data di distribuzione in una scheda Distribuito, che fornisce una chiara cronologia di ciò che è stato corretto e quando.&quot; |
| &quot;Testo alt Autofix V2 — &#39;Verifica fissabilità&#39; valutazione pre-volo&quot; | &quot;Prima di distribuire una correzione di testo alternativo, puoi eseguire una verifica preliminare per verificare che la correzione possa essere applicata correttamente al contenuto.&quot; |
| &quot;Ottimizzazione dello storage al 96% per le metriche SHM&quot; | ometti: solo infrastruttura |
| &quot;AGENTS.md con ruoli di agente formali e protezioni di sicurezza&quot; | ometti: strumenti di intelligenza artificiale interni |
| &quot;Ottimizzazioni delle prestazioni dei test E2E (~6min → ~5min)&quot; | omesso: processo di progettazione |

### Regole di raggruppamento

- **Raggruppa per area funzionalità**, non per team o repository. Ad esempio, tutti i miglioramenti di Testo alternativo (funzioni, miglioramenti e correzioni) appartengono alla stessa area e non li distribuiscono tra le sezioni.
- **Consolidare le correzioni strettamente correlate** in un singolo punto elenco anziché elencare singolarmente ciascuna di esse (ad esempio, &quot;Miglioramenti multipli di visualizzazione e layout nelle opportunità di traffico a pagamento, accessibilità e sicurezza&quot;).
- **Soglia per la sezione Correzioni di bug**: includi questa sezione solo quando sono presenti 3 o più correzioni visibili dall&#39;utente da richiamare. Le correzioni banali o puramente cosmetiche al di sotto di questa soglia devono essere omesse.

## Passaggi

1. Applicare le linee guida in questo file: internalizzare tutti i principi, includere/escludere regole, esempi di tono e regole di raggruppamento.
2. Se non è già stato fornito, chiedi all’utente l’intervallo di date coperto (ad esempio, &quot;11-22 maggio 2026&quot;).
3. Chiedere all’utente di incollare il contenuto delle note sulla versione interne (o accettare un percorso di file).
4. Elabora il contenuto:
   - **Analizzare** ogni sezione (✨/🚀/🤖/🔧/🏢) e i relativi punti elenco.
   - **Filtro** per la tabella di esclusione precedente. Contrassegna ogni elemento rilasciato con un motivo.
   - **Riscrivi** ha mantenuto gli elementi nel tono del cliente: benefit-first, nessun gergo, voci brevi.
   - **Raggruppa** per area funzionalità in cui sono correlati più elementi.
   - **Controllo soglia**: includere una sezione &quot;Correzioni di bug&quot; solo in presenza di più di 3 correzioni visibili all&#39;utente.
5. Formatta la nuova voce utilizzando il modello struttura pagina precedente.
6. Leggere il contenuto corrente di `help/documentation/release-notes.md`.
7. Inserire la nuova voce subito dopo il paragrafo dell&#39;introduzione della pagina (prima dell&#39;ultima intestazione data `##` precedente).
8. Scrivi il file aggiornato.
9. Stampa la tabella di riepilogo.

## Formato di input

L’abilità accetta le note sulla versione interne nel formato standard del team:

```
*ASO UI Release Notes — [Date Range]*
Collaborators: [teams]

✨ *Features*
• [Feature description]

🚀 *Enhancements*
• [Enhancement description]

🤖 *AI-First Development*
• [AI tooling items — will be dropped]

🔧 *Fixes & UX Improvements*
• [Fix description]

🏢 *BackOffice*
• [BackOffice items — will be dropped]
```

## Output

I risultati dell’abilità:

1. Voce formattata rivolta al cliente (da rivedere prima della scrittura).
2. Una richiesta di conferma prima di modificare `release-notes.md`.
3. Dopo la scrittura: una tabella riepilogativa di elementi conservati, riscritti o eliminati.

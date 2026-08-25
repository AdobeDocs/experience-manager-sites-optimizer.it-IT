---
source-git-commit: 2a3a02ea04fac7ce37fdc43e836a4832be224e25
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# Agente documento ASO - Rivedi apprendimenti

Lezioni durature estratte dal feedback di una recensione PR umana sulle PR di questo agente. Lettura
questo file all&#39;inizio del passaggio 4 (Ricerca + bozza) in `pipeline.md`, prima della creazione
qualsiasi cosa — il punto è che una correzione apportata da un revisore non dovrebbe necessariamente essere
è stato rifatto su un biglietto futuro.

## Cosa appartiene qui

Solo feedback **generalizzabile**: un pattern che si ripresenterà nei ticket futuri, circa
tonalità, struttura, sezioni mancanti, posizionamento errato dei file o precisione dei contenuti. Esempi:

- &quot;Menziona sempre la scheda Ignorato per le opportunità che supportano ignora/salta.&quot;
- &quot;Non affermare il controllo a livello di Ultimate a meno che il ticket o una pagina di pari livello esistente non lo confermi, lascialo fuori con un commento e contrassegnalo come elemento aperto.&quot;
- &quot;Le pagine delle procedure per le nuove opportunità richiedono una voce TOC.md e una voce della griglia delle schede nella pagina di destinazione dei tipi di opportunità, non solo nella pagina stessa.&quot;

## Cosa NON appartiene qui

Feedback meccanico una tantum applicato solo a un singolo PR: errori di battitura, un collegamento non funzionante, un
virgola mancante, percorso di file errato in tale PR specifico. Fissali direttamente nella PR:
non generalizzare alle bozze future, quindi una voce durevole sarebbe solo rumore.

## Formato di ingresso

```markdown
## YYYY-MM-DD — SITES-XXXXX (PR #NN)

**Lesson:** [one or two sentences — the generalizable rule]

**Why:** [what the reviewer actually said, or the specific mistake it corrects]

**Applies to:** [which ticket types / pages this affects — "all opportunity how-to pages", "settings/setup pages", "everything", etc.]
```

Le voci più recenti in alto. Se una lezione successiva sostituisce o restringe una precedente, modificare
la voce precedente per notare che invece di lasciare due regole in conflitto nel file.

&#x200B;---

Ancora nessuna voce: questo file ottiene la prima voce la prima volta che una richiesta umana cambia
su uno dei PR di questo agente.

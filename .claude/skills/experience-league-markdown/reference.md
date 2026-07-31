---
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---
# Experience League Markdown — Riferimento con sintassi completa

Condensa da https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax (ultima conferma rispetto alla pagina &quot;Ultimo aggiornamento: 17 giugno 2026&quot;). Recupera nuovamente la pagina live se qualcosa qui sembra non aggiornato.

## Frontmatter e titolo

```markdown
---
title: Title for search optimization
description: This is the article description used for search optimization.
---
# Article title
```

La riga immediatamente dopo il `---` di chiusura (e una riga vuota) deve essere `# Title` e deve corrispondere a `title:` nel frontmatter.

## Formattazione testo di base

- Grassetto: `**bold**`
- Corsivo: `*italic*`
- Grassetto+corsivo: `***both***`
- Esci da un carattere di formattazione: `\*not italic\*`
- I paragrafi non richiedono alcuna sintassi particolare, ma solo una riga vuota tra di essi.

## Titoli

```markdown
# This is level 1 (article title)
## This is level 2 (mini-TOC entry)
### This is level 3
```

- `#` (H1) = titolo articolo, deve corrispondere al frontmatter `title`.
- `##` (H2) = viene visualizzato nel mini-sommario per impostazione predefinita (`mini-toc-levels: 3` in frontmatter per mostrare più livelli).
- Non saltare mai un livello (`##` → `####` non è valido).
- È necessaria una riga vuota prima di **e** dopo ogni intestazione.
- Lunghezza massima del titolo: 69 caratteri (EN), 120 (localizzato).
- ID intestazione/ancoraggio: `## Creating processing rules {#processing-rules}`, lettere minuscole e sillabazione. Obbligatorio se il testo dell’intestazione inizia con un numero (ad esempio, anno). Senza un ID esplicito, l&#39;ancoraggio predefinito è il testo dell&#39;intestazione con riempimento automatico.

## Appunti/ammonizioni

Tipi standard: `NOTE`, `TIP`, `IMPORTANT`, `WARNING`. Tipi solo EXL più recenti: `ADMIN`, `AVAILABILITY`, `PREREQUISITES`, `INFO`, `ERROR`, `SUCCESS`.

```markdown
>[!NOTE]
>
>This is a standard NOTE block.
>
>It can include multiple paragraphs.
```

Ogni riga del blocco inizia con `>`. Includi una riga `>` nuda subito dopo l&#39;indicatore del tipo.

## Schede

```markdown
>[!BEGINTABS]

>[!TAB iOS]

Content for the iOS tab.

>[!TAB Android]

Content for the Android tab.

>[!ENDTABS]
```

- Impossibile nidificare i set di schede all&#39;interno dei set di schede o dei set di schede all&#39;interno degli elenchi.
- I titoli delle schede vengono riprodotti in modo letterale, senza formattazione markdown in `>[!TAB ...]`.
- Su una pagina è possibile utilizzare più set di schede.

## Video

```markdown
>[!VIDEO](https://video.tv.adobe.com/v/27069/?learn=on&enablevpops)
```

- Il video deve essere già ospitato su `video.tv.adobe.com` (Adobe TV/MPC). I collegamenti dei file video non elaborati o i tag `<video>` non sono supportati.
- Parametri di query consigliati: `?learn=on&enablevpops` (il modulo canonico utilizzato da ogni incorporamento in questo archivio). Aggiungi `&autoplay=true` alla riproduzione automatica.
- Trascrizioni: aggiungi `{transcript=true}` al codice breve o imposta `auto-video-transcripts: true` in `TOC.md`/`metadata.md` per l&#39;intera guida/archivio.

## Badge

Badge in linea (esegue il rendering dove posizionato):

```markdown
[!BADGE Beta]{type=Informative url="https://www.example.com" tooltip="Go to example.com"}
```

Badge metadati (rendering sopra l&#39;H1) — in questione frontale:

```yaml
badgePremium: label="Premium" type="Positive" url="https://www.premium-product.com" tooltip="Download Premium"
```

- `type` (senza distinzione maiuscole/minuscole): `Informative` (predefinito/blu), `Positive` (verde), `Negative` (rosso), `Neutral` (grigio scuro), `Caution` (giallo).
- È richiesta solo l&#39;etichetta; `type`/`url`/`tooltip` facoltativo.
- Massimo **due** badge di metadati per articolo (configurabile, ma chiedi prima di fare affidamento su un&#39;eccezione).
- I valori dei badge dei metadati devono essere tra virgolette. Il badge in linea `url`/`tooltip` deve essere citato.
- Gli URL del badge utilizzati da `TOC.md` devono essere relativi alla radice (`/help/guide/article.md`), non relativi. Le voci del sommario si applicano a tutte le cartelle.
- `before-title="false"` sposta un badge di metadati sotto H1.
- Aggiungi `newtab=true` per aprire l&#39;URL del badge in una nuova scheda.

## Immagini

```markdown
![alt text](assets/logo.png "Hover text"){width="300" align="center"}
```

- `align`: solo `center` o `right` - nessun `left`, nessun `valign`.
- `width`: pixel (`"300"`) o percentuale dell&#39;area di visualizzazione (`"50%"`).
- `zoomable="yes"` fa clic sull&#39;immagine per ingrandirla (non combinarla con un&#39;immagine che è anche un collegamento, il collegamento vince).
- Percorso relativo alla directory principale per le immagini condivise: `/help/assets/imagename.png`.
- Limiti: 100 MB di capacità massima (GitHub), 5 MB prima di iniziare a prendersi cura di te, 20 MB innesca un errore di convalida. Massimo 100 immagini per articolo (limite di rendering EDS).

## Collegamenti e rimandi

- Esterno: `[Adobe](https://www.adobe.com)`
- URL non crittografato come collegamento: `<https://www.adobe.com>` — un URL non crittografato non contiene **not** collegamento automatico.
- Riferimento incrociato relativo: `[Overview](collaborative-doc-instructions/overview.md)` — risolvere dalla posizione del file *source*; supporta `./`, `../`, `../../`.
- Riferimento incrociato relativo alla radice: `[Overview](/help/using/docile-rules/introduction.md)` — funziona da qualsiasi file nell&#39;archivio indipendentemente dalla posizione di origine.
- Collegamento profondo a un&#39;intestazione: la destinazione richiede `{#heading-id}`; il collegamento con `[Text](file.md#heading-id)` (o solo `#heading-id` per la stessa pagina).
- Apri in una nuova scheda: `[See What's new](whats-new.md){target="_blank"}`.

## Elenchi

```markdown
1. This is step 1.
1. This is the next step.
   1. Sub-step (indent 3 spaces for numbered lists)
   1. Sub-step
```

```markdown
* First item.
* Second item.
```

- Elenchi numerati: scrivi sempre `1.` (o sempre `1)`). GitHub esegue il rendering della sequenza reale. Scegli uno stile (`.` vs `)`) e mantieni la coerenza all&#39;interno dell&#39;articolo.
- Elenchi puntati: scegli uno di `*`, `-`, `+` e mantieni la coerenza; la loro combinazione nello stesso articolo è un errore di convalida. Convenzione nella maggior parte dei repository: `*`.
- Riga vuota obbligatoria prima e dopo qualsiasi elenco.
- Il contenuto tra le voci di elenco (immagini, tabelle, note) deve essere rientrato all&#39;inizio del testo (3 spazi per gli elenchi numerati, 2 per gli elenchi puntati) o interrompe l&#39;elenco. Il rientro eccessivo (6 spazi) lo trasforma invece in un blocco di codice.

## Blocchi di codice

In linea: `` `code` `` - Oppure racchiudi in linea tre apici retroversi se hai bisogno di un apposito carattere di apice inverso.

Recintato:

````markdown
```javascript
var x = 1;
```
````

- Specificare sempre un linguaggio per l&#39;evidenziazione della sintassi + il pulsante Copia.
- Riga vuota richiesta sopra e sotto il blocco delimitato.
- Numeri di riga: `` ```html {line-numbers="true"} ``
- Inizia numerazione altrove: `` ```html {line-numbers="true" start-line="7"} ``
- Righe evidenziazione: `` ```html {line-numbers="true" start-line="7" highlight="11-13, 16"} ``
- Il contenuto del blocco di codice non è mai localizzato (ad eccezione dei tag `!UICONTROL`/`!DNL`, che vengono rimossi al momento della pubblicazione).
- Nessuna formattazione Markdown/HTML (come `<i>`) funziona all&#39;interno di blocchi di codice. Utilizzare parentesi angolari o testo normale per i segnaposto.

## Tabelle

- Le tabelle di pipe GFM standard funzionano per casi semplici.
- Le tabelle di HTML sono consentite per casi speciali (ad esempio, una tabella senza riga di intestazione); in caso contrario, è preferibile utilizzare il markdown.
- HTML limitato è consentito nelle celle della tabella markdown: `<p>`, `<br>`, `<ul>`, `<ol>`.
- Le tabelle possono essere impostate su rendering automatico o fisso. Vedere l&#39;articolo &quot;Tabelle&quot; collegato dalla guida alla sintassi se è necessario tale livello di controllo.

## Sezioni comprimibili

```markdown
+++See details

This is text inside a collapsible section.

* Bullet one
* Bullet two

+++
```

- Non nidificare sezioni comprimibili: non verranno riprodotte correttamente (e non falliranno la convalida, quindi il bug viene inviato in modalità silenziosa).
- Sono necessarie righe vuote intorno agli elenchi interni o ai blocchi di codice all’interno della sezione, come in qualsiasi altro punto.

## Evidenziazione testo

```markdown
This sentence is normal. <span class="preview">This text is highlighted.</span>
```

Utilizza `<span class="preview">` per evidenziare i paragrafi in linea/paragrafo, `<div class="preview">` per più paragrafi/componenti.

## Snippet e include

- Ancoraggi H2 condivisi da `help/snippets.md` di un repository: riferimento con `{{anchor-id}}`.
- File di inclusione condivisi da `help/_includes/*.md`: riferimento con `{{$include /help/_includes/filename.md}}`.

## Commenti

```markdown
<!-- standard comment code -->
```

- Non utilizzare mai `<!--> bad comment syntax <-->` (trattini mancanti): il rendering è visibile invece di nascondere il testo.
- I commenti non sono visibili nei documenti sottoposti a rendering, ma **sono visibili a chiunque visualizzi il file .md non elaborato su GitHub**. Nessun segreto o informazione riservata.
- Evita commenti all’interno di elenchi puntati (può interrompere il rendering degli elenchi). In `TOC.md`, inserire un commento solo nelle righe alla fine del file, mai al centro dell&#39;elenco.

## Soluzione alternativa a righe vuote

Il renderer comprime le righe vuote aggiuntive nell’origine. Per forzare lo spazio verticale visibile, posizionare `<br>&nbsp;` sulla propria riga in cui si desidera inserire lo spazio vuoto.

## Caratteri di escape

- Caratteri compatibili con la barra rovesciata: `` # { } [ ] * + - . ! ``, ad esempio `\# not a heading`.
- Per le parentesi angolari (`<placeholder>`), la barra rovesciata non funziona. Utilizzare un blocco di codice in linea (`` `<placeholder>` ``) o entità HTML (`&lt;placeholder&gt;`).
- Le entità HTML all&#39;interno dei blocchi di codice sono **non** riconvertite nel carattere. `&gt;` rimane il testo letterale.
- I metadati (frontmatter YAML) dispongono di regole di escape proprie. Se un valore inizia con un carattere speciale come `:` o `[`, indicare l&#39;intero valore: `title: "Processing rules: A new beginning"`.

## HTML di limitato

Solo questi tag HTML sono consentiti in qualsiasi punto di Markdown; qualsiasi altro è un errore di convalida:

```
table  tbody  td  tfoot  thead  th  tr  col  colgroup
p  ul  ol  li  br
b  i  strong  u  s  em  sub  sup  span
caption  a  img  div
pre  code  codeblock
```

Preferisci la sintassi markdown a quella di HTML ovunque sia possibile eseguire il processo: HTML in realtà è solo per i casi limite, come una tabella senza intestazione.

## Esplicitamente non supportato (non utilizzare anche se viene eseguito il rendering in un’anteprima locale)

- Regole orizzontali (`***`, `<hr>`)
- Codici brevi Emoji (`:bowtie:`)
- Elenchi attività (`- [x] done`)
- *componenti* oltre i codici brevi note/tab/video (i blockquote `>` semplici vengono visualizzati come virgolette, non come componenti con stile)
- Sintassi dell&#39;elenco di definizioni di Markdown (usare il grassetto manuale + la formattazione del trattino invece: `**Frog** - An amphibious green creature.`)
- `valign` sulle immagini

## Limiti di dimensione file/conteggio

| Cosa | Limite |
|---|---|
| Dimensione file immagine/download | Avviso di convalida a 5 MB, errore a 20 MB, limite GitHub rigido di 100 MB |
| Immagini per articolo | 100 (limite di rendering EDS) |
| Badge metadati per articolo | 2 (impostazione predefinita) |

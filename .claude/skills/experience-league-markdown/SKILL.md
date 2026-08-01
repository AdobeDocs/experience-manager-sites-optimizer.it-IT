---
name: experience-league-markdown
description: 'Da utilizzare quando si scrivono o si modificano file Markdown in un archivio Adobe Experience League/Adobe-Enterprise-Docs (help/**/*.md): controlla frontmatter, intestazioni, note (NOTE/TIP/IMPORTANTE/AVVERTENZA/ecc.), schede (BEGINTABS/TAB/ENDTABS), incorporamenti video, badge, immagini, collegamenti/riferimenti incrociati, tabelle, elenchi, blocchi di codice e l’elenco Consentiti di tag HTML limitato applicato dalla pipeline di convalida di Experience League.'
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---


# Experience League Markdown

## Panoramica

I documenti di Experience League utilizzano Markdown aromatizzato su GitHub oltre a un set di estensioni personalizzate (codici brevi basati su blockquote, badge, schede, incorporamenti di video). La pipeline di authoring **convalida** questi file, utilizzando una sintassi non supportata (tag `<video>` non elaborati, `<hr>`, elenchi di attività, caratteri punto elenco misti, livelli di intestazione saltati, immagini di dimensioni eccessive), genera un errore di compilazione/convalida, non solo un&#39;unità di stile.

Source of true: https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax (recupera questa pagina se il file reference.md locale sembra non aggiornato; la data dell’ultimo aggiornamento è nella parte superiore).

Riferimento di sintassi completo con ogni codice breve e regola: [reference.md](reference.md). Leggilo prima di scrivere qualsiasi cosa non banale (schede, video, badge, tabelle con HTML).

## Riferimento rapido

| Elemento | Sintassi | Note |
|---|---|---|
| Frontmatter | `---\ntitle: ...\ndescription: ...\n---` | Riga vuota, `# Title` deve arrivare dopo |
| Livelli di intestazione | `#`, `##`, `###` | `#` = titolo (corrisponde al frontmatter `title`), `##` = voci di sommario mini. Non saltare mai un livello. Riga vuota prima/dopo. Max 69 caratteri (EN) |
| ID intestazione | `## Heading text {#custom-id}` | Obbligatorio se l&#39;intestazione inizia con/contiene un numero, ad esempio `## 2026 release notes {#2026-release-notes}` |
| Nota/Suggerimento/ecc. | `>[!NOTE]` quindi `>` e poi `>Text` (ciascuno sulla propria riga) | Tipi: NOTA, SUGGERIMENTO, IMPORTANTE, AVVISO, ATTENZIONE, AMMINISTRATORE, DISPONIBILITÀ, PREREQUISITI, INFORMAZIONI, ERRORE, OPERAZIONE RIUSCITA |
| Schede | `>[!BEGINTABS]` / `>[!TAB Title]` / `>[!ENDTABS]` | Impossibile nidificare i set di schede; impossibile nidificare all&#39;interno degli elenchi |
| Video | `>[!VIDEO](https://video.tv.adobe.com/v/ID/?learn=on&enablevpops)` | Deve essere ospitato su video.tv.adobe.com — nessun collegamento `<video>`/file non elaborato |
| Immagine | `![alt text](assets/img.png "hover text"){width="300" align="center"}` | `align` è solo `center` o `right` (nessun `left`, nessun `valign`) |
| Collegamento (relativo) | `[Text](../folder/file.md)` | Account per la posizione del file di origine |
| Collegamento (radice) | `[Text](/help/guide/file.md)` | Funziona da qualsiasi punto dell’archivio; richiesto per gli URL di badge TOC.md |
| Collegamento profondo | `[Text](file.md#heading-id)` | L&#39;intestazione di destinazione richiede un `{#heading-id}` esplicito |
| Collegamento esterno (URL nudo) | `<https://example.com>` | Gli URL vuoti NON sono collegati automaticamente — a capo in `< >` o usa `[text](url)` |
| Elenco puntato | `* item` (scegli uno di `*`/`-`/`+`, mantieni la coerenza) | Riga vuota prima/dopo l&#39;elenco; indicatori di combinazione = errore di convalida |
| Elenco numerato | `1. item` (ripeti `1.` ogni riga) | GitHub esegue il rendering dei numeri reali |
| Codice (in linea) | `` `code` `` | Per nomi di file, comandi, valori, URL di esempio non convalidati |
| Codice (delimitato) | ` `&#x200B;``language ` ... ` ``&#x200B;` ` | Specifica sempre una lingua; riga vuota prima/dopo; `{line-numbers="true" start-line="n" highlight="n-m"}` facoltativo |
| Badge (in linea) | `[!BADGE Beta]{type=Informative url="..." tooltip="..."}` | `type`: informativo/positivo/negativo/neutro/cautela |
| Comprimibile | `+++Summary` ... `+++` | Nessun comprimibile nidificato; righe vuote intorno agli elenchi/codici interni |
| Hack di riga vuota | `<br>&nbsp;` sulla propria riga | Il renderer comprime/ignora le righe vuote in eccesso |
| Commenti | `<!-- text -->` | Mai `<!--> text <-->`: visibile a chiunque visualizzi il file non elaborato su GitHub, quindi nessun segreto |

## Errori comuni

- **Errore non elaborato `<video>`, `<iframe>` o altro errore di convalida del → di HTML** non inserito nell&#39;elenco Consentiti. Il HTML di di inserire nell&#39;elenco Consentiti è: `table tbody td tfoot thead th tr col colgroup p ul ol li br b caption i strong u s span sub sup a img div em pre code codeblock`. Qualsiasi altro elemento (incluso `<video>`/`<source>`) è rifiutato. Utilizzare il codice breve `>[!VIDEO]`, che richiede che il video sia già ospitato su video.tv.adobe.com.
- **`<hr>`/ `***` regole orizzontali, codici di scelta rapida emoji (`:bowtie:`), elenchi attività (`- [x]`)** — non sono supportati. Non utilizzarli anche se vengono visualizzati in anteprima locale.
- **Combinazione di caratteri punto elenco** (`*` e `-` nello stesso elenco). Errore di convalida. Sceglietene uno per articolo.
- **Ignorare i livelli di intestazione** (`##` direttamente in `####`). Operazione non consentita.
- **Un&#39;intestazione con interlinea numerica senza un ID esplicito** (ad esempio `## 2026 release notes`) deve aggiungere `{#some-id}` per evitare che il tag automatico si scontri o si blocchi.
- **URL vuoti in prosa** (`Visit https://example.com for more`) — non verranno visualizzati come collegamento. Eseguire il wrapping in `< >` o utilizzare `[text](url)`.
- **Righe vuote aggiuntive per la spaziatura visiva** — compresse dal renderer. Utilizza `<br>&nbsp;` invece di `<br>` nude o righe nuove ripetute.
- **Immagini superiori a ~5 MB** — avviso di convalida a 5 MB, errore a 20 MB. Più di 100 immagini in un articolo interrompono il rendering (limite EDS).
- **Più di due badge nei metadati di frontmatter** — non consentito per impostazione predefinita.
- **Problemi di escape**: backslash-escape funziona solo per `` # { } [ ] * + - . ! ``. Per `<` `>` in elementi come `<filename>` segnaposto, utilizza un blocco di codice in linea o entità HTML (`&lt;filename&gt;`), non una barra rovesciata.

## Prima di eseguire il commit delle modifiche Markdown

1. Frontmatter presente, `# Title` segue immediatamente (dopo la riga vuota).
2. Ogni titolo ha una riga vuota prima e dopo; nessun livello saltato.
3. Qualsiasi video è `>[!VIDEO](https://video.tv.adobe.com/...)`, non un tag `<video>` non elaborato.
4. Qualsiasi codice breve personalizzato (`>[!NOTE]`, `>[!BEGINTABS]`, `>[!BADGE ...]`) corrisponde alla sintassi esatta in [reference.md](reference.md), inclusa la riga `>` vuota all&#39;interno di blocchi con più righe.
5. Gli elenchi utilizzano uno stile punto elenco/numero coerente, con righe vuote intorno all&#39;intero elenco.
6. Collegamenti: i collegamenti relativi vengono risolti dalla cartella del file *source*. I collegamenti tra repository o TOC/badge utilizzano il modulo relativo alla radice (`/help/...`).
7. Nella sezione Errori comuni sopra riportata non è presente alcun tag di HTML al di fuori del elenco Consentiti di.

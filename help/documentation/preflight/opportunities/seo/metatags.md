---
title: Verifica preliminare dei metatag
description: Scopri l’audit dei metatag in Verifica preliminare per AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 59c097682899889aa2a5d76333f80cc58e28ff1e
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%
---
# Audit dei metatag

Il controllo di audit **Metatags** esamina il titolo della pagina, la metadescrizione e l&#39;intestazione principale (H1). Segnala le pagine mancanti, vuote o al di fuori della lunghezza consigliata e le pagine con più intestazioni H1.

## Perché è importante

Il titolo della pagina e la metadescrizione sono in genere quelli visualizzati per la pagina nei risultati di ricerca: il titolo come titolo cliccabile e la descrizione come riepilogo sotto di esso. Un titolo o una descrizione mancante o di dimensioni insoddisfacenti possono essere tagliati o sostituiti con testo scelto dal motore di ricerca nella pagina. L’intestazione H1 indica ai lettori e ai motori di ricerca l’argomento principale della pagina, pertanto una pagina deve avere un H1 chiaro.

## Controlli dell’audit

L’audit segnala un’opportunità per ciascuno dei seguenti problemi:

* **Titolo pagina:** mancante, vuoto, troppo breve o più lungo della lunghezza ideale.
* **Descrizione Meta:** mancante, vuota, troppo breve o più lunga della lunghezza ideale.
* **Intestazione H1:** mancante, vuota, più lunga della lunghezza ideale o più di una H1 nella pagina.

Un valore di alcuni caratteri oltre la lunghezza ideale viene segnalato come **superiore alla lunghezza ideale** e uno oltre il massimo del controllo di audit come **troppo lungo**. La verifica preliminare non ha una soglia troppo lunga per i titoli delle pagine.

| Tag | Lunghezza ideale | Oltre la lunghezza ideale | Troppo lungo |
|---|---|---|---|
| Titolo pagina | Da 40 a 60 caratteri | Più di 60 caratteri | - |
| Descrizione di Meta | Da 140 a 160 caratteri | Da 161 a 175 caratteri | Più di 175 caratteri |
| Intestazione H1 | Fino a 70 caratteri | Da 71 a 75 caratteri | Più di 75 caratteri |

Questi intervalli sono linee guida consigliate, non requisiti dei motori di ricerca. La verifica preliminare li utilizza per decidere quando segnalare un’opportunità.

## Modalità di lettura dei valori

Il controllo di audit legge la pagina che si sta modificando: il testo dell&#39;elemento `<title>`, il contenuto del tag `<meta name="description">` e il testo visibile del primo elemento `<h1>`, incluso il testo in grassetto o corsivo al suo interno.

Un tag è **mancante** quando la pagina non è presente e **vuoto** quando è presente ma non contiene testo visibile. Le lunghezze contano ogni carattere, compresi gli spazi e la punteggiatura. Viene controllata la lunghezza solo del primo H1. Quando una pagina ha più di un H1, ciascuno è elencato come istanza separata, in modo da poter trovare e modificare i titoli aggiuntivi.

## Suggerimenti

Ogni opportunità include un consiglio, ad esempio la lunghezza ideale per il tag o una H1 in una pagina.

Il titolo della pagina, la metadescrizione e le opportunità H1 possono anche includere un suggerimento generato dall’intelligenza artificiale, scritto dal contenuto della pagina. Un suggerimento viene visualizzato solo se si adatta alla lunghezza ideale. Rivedi e modifica ogni suggerimento prima di utilizzarlo.

Quando un’opportunità H1 non ha alcun suggerimento di IA, il suggerimento è fisso, ad esempio accorciare l’intestazione o cambiare le intestazioni H1 in H2. Quando un’opportunità di titolo o metadescrizione della pagina non ha alcun suggerimento di IA, la verifica preliminare mostra che non è disponibile alcun suggerimento.

## Se un valore contrassegnato ti sembra corretto

Nelle pagine Edge Delivery Services, il titolo o la metadescrizione di una pagina non impostata viene inserito automaticamente dal primo titolo e dal primo paragrafo della pagina. Spesso sono più brevi della lunghezza ideale, pertanto la pagina viene contrassegnata. Per risolvere questo problema, imposta il titolo e la descrizione nei metadati della pagina.

## Limitazioni note

* **Gli altri tag head non sono controllati**, ad esempio i tag Open Graph per la condivisione social o il tag robots.
* **La lunghezza è conteggiata in caratteri:** i titoli e le descrizioni dei motori di ricerca vengono abbreviati in base allo spazio occupato sullo schermo, pertanto un valore della lunghezza ideale può essere ancora ridotto nei risultati di ricerca.
* **Lingue senza spazi tra le parole:** nelle pagine in lingue quali cinese, giapponese o coreano, è comunque possibile contrassegnare un valore che indica che la lettura è corretta e i suggerimenti di IA potrebbero non rientrare nella lunghezza ideale.

## Come risolvere

Ogni opportunità descrive il problema e la modifica consigliata e mostra il valore corrente del titolo della pagina o della metadescrizione.

* **Titolo pagina e descrizione meta:** aggiornali dove il tuo sito li imposta, ad esempio nelle proprietà della pagina in AEM Sites o nei metadati della pagina in Edge Delivery Services. Questi tag si trovano nell&#39;intestazione della pagina, quindi **Evidenzia a pagina** non è disponibile.
* **Intestazione H1:** utilizza **Evidenzia a pagina** per trovare l&#39;intestazione nel contenuto. In Edge Delivery Services, AEM Sites Page Editor e Adobe Managed Services (AMS), la verifica preliminare scorre fino all&#39;intestazione e lo delinea; l&#39;Editor pagina e AMS richiedono la **modalità di modifica**. Nell’editor universale, Verifica preliminare seleziona l’intestazione o il blocco modificabile più vicino che la contiene. Non è possibile selezionare un&#39;intestazione nella navigazione o un piè di pagina visualizzato. Per ulteriori informazioni, vedere [Evidenzia a pagina](../../audit-results.md#highlight-on-page).

Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

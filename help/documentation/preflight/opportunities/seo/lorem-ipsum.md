---
title: Verifica preliminare Lorem Ipsum
description: Scopri l’audit Lorem ipsum in Verifica preliminare per AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 587aec4eb905a2b1ced746590ca25b8ed97b16c1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%
---
# Audit Lorem ipsum

Il controllo di controllo **Lorem ipsum** rileva il testo segnaposto lasciato nel contenuto della pagina.

## Perché è importante

Quando si pubblica una pagina con testo segnaposto, questa viene visualizzata come incompleta per i lettori. I motori di ricerca possono indicizzare il testo segnaposto e mostrarlo nei risultati di ricerca, mentre le piattaforme social possono visualizzarlo nelle anteprime dei collegamenti. Il testo segnaposto è spesso nascosto, ad esempio nel testo alt dell’immagine o nelle etichette di accessibilità. Al contrario, gli utenti che utilizzano utilità per la lettura dello schermo o altre tecnologie per l’accessibilità potrebbero ancora ascoltarlo, anche se non viene visualizzato nella pagina.

## Controlli dell’audit

Il controllo di audit segnala ogni punto della pagina in cui viene visualizzato il testo segnaposto. Controlla il testo visibile della pagina, oltre a diversi punti in cui potrebbe non essere visibile immediatamente o affatto:

* testo alternativo immagine
* etichette e descrizioni di accessibilità
* segnaposto per campo modulo
* descrizioni comandi
* titolo della pagina
* metadati, come la metadescrizione e i tag di condivisione social

Il codice che non viene presentato agli utenti, ad esempio script e stili, non è selezionato.

## Corrispondenza del testo

Il controllo di audit cerca la frase &quot;lorem ipsum&quot; in qualsiasi combinazione di lettere maiuscole e minuscole. Trova inoltre la frase quando le parole sono divise su righe o elementi o non hanno spazio tra di essi. Se la frase appare più di una volta nello stesso elemento o attributo, tale posizione viene segnalata una volta.

## Limitazioni note

* **Non viene rilevato solo &quot;lorem ipsum&quot;:** altro testo segnaposto, ad esempio &quot;TBD&quot; o altre parole di riempimento latine senza &quot;lorem ipsum&quot;.
* **Evidenzia nella pagina:** non è disponibile per il titolo o i metadati della pagina perché non sono visualizzati nella pagina. Utilizza il testo mostrato nell’opportunità per trovarli.

## Come risolvere

Quando il controllo di audit trova opportunità, ciascuna di esse identifica la posizione in cui viene visualizzato il testo segnaposto. Dove è disponibile, usa **Evidenzia a pagina** per passare al testo nel contenuto. Sostituire il segnaposto con contenuto reale o rimuoverlo. Per il testo alternativo e le etichette di accessibilità, scrivere una descrizione dell&#39;immagine o del controllo. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

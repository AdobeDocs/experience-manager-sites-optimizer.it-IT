---
title: Verifica preliminare Lorem Ipsum
description: Scopri l’audit Lorem ipsum in Verifica preliminare per AEM Sites Optimizer.
badgePreflightSEO: label="Verifica preliminare - SEO" type="Caution" url="../seo.md" tooltip="Verifica preliminare - SEO"
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 659419fa2eb570b4e1fedf87c35c5c60c46ffc8a
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%
---
# Verifica preliminare - Audit Lorem ipsum

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
* **Evidenzia nella pagina:** non è disponibile per il titolo o i metadati della pagina perché non sono visualizzati nella pagina. Utilizza **Dettagli** e la casella **Elemento** per trovare il testo.

## Come risolvere

Controllare **Dettagli** per la posizione del testo, ad esempio il titolo di una pagina, il testo alternativo o l&#39;intestazione. **Recommendation** spiega come correggerlo e la casella **Element** mostra il testo all&#39;interno del tag.

Utilizza **Evidenzia a pagina**, se disponibile. Un elemento nascosto può essere visualizzato in altre dimensioni dello schermo o in un menu o in una finestra di dialogo.

Sostituire o rimuovere il testo segnaposto. Per il testo alternativo e le etichette di accessibilità, descrivere l&#39;immagine o il controllo. Per ulteriori informazioni, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

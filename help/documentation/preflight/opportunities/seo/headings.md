---
title: Verifica preliminare intestazioni
description: Scopri l’audit Intestazioni in Verifica preliminare per AEM Sites Optimizer.
source-git-commit: af80dbb47a25b10cdbe55965fb7c4ce496448871
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%
---
# Titoli e audit

L&#39;audit **Headings** esamina i sottotitoli della pagina (da H2 a H6). Contrassegna le intestazioni prive di testo e quelle che saltano un livello, ad esempio un H2 seguito direttamente da un H4.

## Perché è importante

Le intestazioni forniscono la struttura di una pagina. I lettori eseguono la scansione per trovare ciò di cui hanno bisogno, gli utenti di utilità di lettura dello schermo si spostano all’interno di una pagina in base ai titoli e i motori di ricerca li utilizzano per comprendere come è organizzato il contenuto. Un&#39;intestazione vuota aggiunge un&#39;interruzione nella struttura senza alcun elemento, mentre un livello saltato rende la struttura più difficile da seguire.

## Controlli dell’audit

L’audit segnala un’opportunità per ciascuno dei seguenti problemi:

* **Intestazione vuota:** un H2, H3, H4, H5 o H6 senza testo. Un&#39;intestazione che contiene solo spazi o solo un&#39;immagine conta come vuota.
* **Livello di intestazione ignorato:** un&#39;intestazione che è più di un livello più profonda del titolo immediatamente precedente, ad esempio un H2 seguito da un H4 o un H1 seguito da un H3. L’opportunità viene riportata nell’intestazione più profonda.

Entrambi sono stati segnalati con un impatto moderato.

Le intestazioni H1 vengono esaminate dall&#39;audit [Metatags](./metatags.md), che verifica la presenza di un H1 mancante, vuoto o eccessivamente lungo e la presenza di più H1 in una pagina.

## Modalità di lettura delle intestazioni

Il controllo di audit legge la pagina che stai modificando e osserva ogni intestazione nell’ordine in cui viene visualizzata:

* Il conteggio di tutti i titoli, inclusi quelli nascosti nell&#39;intestazione, nella navigazione e nel piè di pagina della pagina e quelli nascosti sullo schermo.
* Viene selezionato solo il passaggio da un’intestazione all’altra. Una pagina il cui primo titolo è un H3 non viene contrassegnata per questo.
* Le intestazioni possono tornare su un numero qualsiasi di livelli, ad esempio da un H4 a un H2.

## Suggerimenti

Ogni opportunità include una raccomandazione e consigli fissi per la modifica da apportare. Il controllo Intestazioni non genera suggerimenti di IA.

## Se un&#39;intestazione contrassegnata è corretta

Se un’opportunità non corrisponde a quanto previsto, in genere il motivo è uno dei seguenti:

* **L&#39;intestazione fa parte del modello della pagina.** Le intestazioni nell’intestazione, nella navigazione o nel piè di pagina vengono controllate insieme al contenuto, pertanto un’intestazione di piè di pagina più profonda dell’ultima intestazione nel contenuto può essere contrassegnata come livello ignorato. La correzione nel modello lo risolve in ogni pagina che utilizza il modello.
* **L&#39;intestazione contiene solo un&#39;immagine o un&#39;icona.** Un’intestazione senza testo viene segnalata come vuota anche quando mostra un’immagine. Aggiungete del testo all&#39;intestazione o utilizzate un elemento diverso dal titolo per l&#39;immagine.

## Limitazioni note

* **Visibilità non considerata:** le intestazioni nascoste sullo schermo sono ancora selezionate.
* **Le pagine molto grandi:** le pagine con più di 500 intestazioni non sono selezionate.

## Come risolvere

Quando il controllo di audit trova delle opportunità, ognuna di esse descrive il problema e la modifica consigliata.

* **Intestazione vuota:** aggiungi testo descrittivo all&#39;intestazione o rimuovilo se non è necessario.
* **Livello di intestazione ignorato:** modificare l&#39;intestazione al livello successivo in basso rispetto all&#39;intestazione precedente (ad esempio, un H4 dopo un H2 diventa un H3) oppure aggiungere il livello mancante nel mezzo.

Usa **Evidenzia a pagina** per trovare l&#39;intestazione nel contenuto. La modalità di evidenziazione dell&#39;intestazione dipende dalla posizione di esecuzione della verifica preliminare:

* **Edge Delivery Services:** La verifica preliminare scorre fino all&#39;intestazione e lo delinea.
* **Editor pagina di AEM Sites e Adobe Managed Services (AMS):** La verifica preliminare scorre fino all&#39;intestazione e lo delinea. L&#39;evidenziazione richiede la **modalità di modifica**.
* **Editor universale:** La verifica preliminare seleziona l&#39;intestazione stessa o il blocco modificabile più vicino che la contiene. Per un’intestazione nel contenuto che l’editor non gestisce, ad esempio la navigazione o un piè di pagina, Verifica preliminare la visualizza ma non può selezionare l’intestazione stessa.

Per ulteriori informazioni, vedere [Evidenzia a pagina](../../audit-results.md#highlight-on-page).

Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

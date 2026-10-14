---
title: Verifica preliminare dell'audit canonico
description: Scopri il controllo Canonical in Verifica preliminare per AEM Sites Optimizer.
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
source-git-commit: 5c97431c2029e117339877219c2d6e4e30902a70
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%
---
# Audit canonico

L&#39;audit di **Canonical** esamina il collegamento canonico nella pagina. Il collegamento canonico è un tag `<link rel="canonical">` in `<head>` della pagina che denomina l&#39;URL preferito per il contenuto della pagina. Il controllo di audit flag collegamenti canonici mancanti, impostati in modo errato o che puntano a un punto diverso dalla pagina stessa.

## Perché è importante

Lo stesso contenuto può spesso essere raggiunto a più di un URL, ad esempio con e senza una barra finale, con parametri di tracciamento o con maiuscole diverse. I motori di ricerca considerano ogni URL come una pagina separata, a meno che non venga indicato diversamente. Il collegamento canonico indica l’URL preferito; ciò li aiuta a raggruppare i duplicati, combinare i segnali di classificazione come i collegamenti in entrata su un URL e mostrare tale URL nei risultati di ricerca.

Un collegamento canonico errato può essere peggiore di nessuno. I motori di ricerca possono ignorare un collegamento canonico che non possono considerare attendibile, ad esempio uno senza URL, uno posizionato al di fuori di `<head>` o uno dei diversi tag in disaccordo. Un collegamento canonico che punta a una pagina diversa richiede ai motori di ricerca di mostrare tale pagina al posto della tua, in modo da escludere la pagina dai risultati di ricerca.

## Controlli dell’audit

L&#39;audit verifica la presenza di problemi in tre settori:

* **Indica se la pagina include un solo collegamento canonico:** il collegamento canonico è mancante o se la pagina ne contiene più di uno. Diversi collegamenti canonici che puntano a URL diversi vengono segnalati separatamente, perché i motori di ricerca potrebbero ignorarli tutti.
* **Indica se il tag è configurato correttamente:** il tag si trova all&#39;esterno di `<head>`, non ha un attributo `href` o ne ha uno vuoto oppure contiene un attributo come `hreflang`, `media` o `type` che può far sì che i motori di ricerca lo ignorino.
* **Indica se l&#39;URL è corretto:** l&#39;URL canonico è relativo anziché assoluto, contiene lettere maiuscole nel percorso o nella stringa di query, utilizza un protocollo diverso (`http://` o `https://`) dalla pagina oppure punta a una pagina diversa da quella che si sta modificando.

## Confronto dell’URL canonico

La verifica preliminare viene eseguita sulle pagine di anteprima, il cui host è in genere diverso dal sito di produzione. Per evitare di contrassegnare ogni pagina di anteprima, il controllo di audit non confronta l’host dell’URL canonico con l’host della pagina. Quando controlla se il collegamento canonico punta alla pagina stessa, confronta solo il percorso dell&#39;URL, quindi `https://www.example.com/products/shoes` corrisponde alla pagina di anteprima `/products/shoes`. Una barra finale e una lettera maiuscola nel percorso non vengono considerate come differenze per questo controllo.

## Limitazioni note

* **Dominio diverso:** un URL canonico che punta a un sito diverso non viene contrassegnato dalla verifica preliminare, perché gli host di anteprima sono sempre diversi dal sito di produzione. Conferma che il dominio nell’URL canonico sia quello previsto.
* **Intestazione HTTP `Link`:** La verifica preliminare controlla solo il tag canonical e non l&#39;intestazione HTTP `Link`. Una pagina che imposta il proprio URL canonico solo nell’intestazione viene segnalata come priva del collegamento canonico.

## Come risolvere

Quando il controllo di audit trova delle opportunità, ognuna di esse descrive il problema e la modifica consigliata. Nella maggior parte dei casi la pagina deve avere esattamente un collegamento canonico, in `<head>`, con un URL assoluto con un percorso in minuscolo che punta alla pagina stessa. Se la pagina punta intenzionalmente a un’altra pagina come versione canonica, ad esempio una copia duplicata o compatibile con la stampante, puoi lasciarla invariata. L&#39;audit continuerà a riferire in merito. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

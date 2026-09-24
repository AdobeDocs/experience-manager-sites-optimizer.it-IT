---
title: Verifica preliminare dimensioni corpo
description: Scopri il controllo dimensioni corpo in Verifica preliminare per AEM Sites Optimizer.
source-git-commit: c85cfb84b315b64ab5fcddfaa192ce78dd8d1a67
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%
---
# Controllo dimensioni corpo

L&#39;audit **Body size** esamina la quantità di contenuto del corpo nella pagina. Le pagine con pochissimo contenuto possono essere meno utili per i lettori e possono non essere classificate correttamente nei risultati di ricerca. Il controllo di audit contrassegna le pagine che sembrano avere troppo poco testo.

## Perché è importante

I motori di ricerca e gli assistenti AI si basano sul testo di una pagina per comprenderne la funzione. Una pagina con poco o nessun testo viene spesso trattata come un valore basso, che può danneggiare la sua classificazione e il fatto che venga o meno evidenziata nelle risposte AI.

## Controlli dell’audit

L’audit misura la quantità di testo creato sulla pagina e segnala due situazioni:

* **Nessun contenuto di testo:** la pagina è stata letta correttamente ma non contiene alcun corpo del testo, ad esempio una pagina costituita solo da un&#39;immagine.
* **Contenuto sottile:** la pagina contiene del testo, ma è inferiore al minimo consigliato.

Una pagina con un numero sufficiente di passaggi di testo e non è contrassegnata.

## Come vengono misurati i contenuti

Il controllo di audit misura il testo nell’area del contenuto principale della pagina, non l’intera pagina. Gli elementi condivisi come navigazione, intestazioni, piè di pagina e breadcrumb si ripetono su ogni pagina e il controllo di audit li esclude dove possono essere riconosciuti in modo che questo colore condiviso non mascheri contenuti genuinamente sottili. La possibilità di separare completamente il contenuto da tale colore dipende dal markup della pagina, come descritto di seguito.

Per trovare il contenuto, il controllo di audit utilizza la prima di queste che si applica:

1. **`<main>`elementi (o `role="main"`).** Viene trattata come area di contenuto definitiva e viene misurato solo il testo al suo interno (se una pagina contiene più di un elemento di questo tipo, il relativo testo viene combinato). È l&#39;opzione più affidabile.
1. **Il corpo della pagina, con Chrome rimosso.** Se non è presente alcun `<main>` e nessun `role="main"`, il controllo di audit misura `<body>` dopo aver rimosso il cromo di pagina riconosciuto: l&#39;intestazione e il piè di pagina a livello di pagina, contrassegnati con tag HTML standard, ruoli di punto di riferimento ARIA oppure con i componenti di intestazione, piè di pagina, breadcrumb e navigazione AEM standard. Viene mantenuta un&#39;intestazione o un piè di pagina che appartiene a una sezione di contenuto, ad esempio il titolo o il nome di un articolo.
1. **Il corpo completo della pagina.** Se non è presente alcun punto di riferimento per il contenuto e non è stato riconosciuto alcun colore, verrà misurato l&#39;intero `<body>`.

Alcune note su ciò che conta. Le immagini non contribuiscono ad alcun testo (il loro testo `alt` non è misurato), quindi è ancora possibile contrassegnare una pagina che è per lo più immagini. Il testo all&#39;interno dei tag `<script>` e `<style>` non viene mai conteggiato, pertanto gli script di analisi o di livello dati non gonfiano la misurazione. Il testo di collegamento normale, tuttavia, viene conteggiato come qualsiasi altro testo nel contenuto.

## Se una pagina contrassegnata è corretta

Se una pagina è contrassegnata come sottile ma si è certi che abbia sufficiente contenuto, il controllo di audit potrebbe non aver separato in modo chiaro il contenuto dal colore circostante, ad esempio navigazione, intestazioni e piè di pagina.

Se desideri che il controllo di audit misuri la pagina in modo più preciso, le seguenti scelte di markup la aiutano:

* L&#39;opzione più affidabile consiste nel racchiudere il contenuto creato in un elemento `<main>` (o aggiungere `role="main"`). In questo modo viene eliminata qualsiasi ambiguità e viene quindi misurato solo il contenuto.
* Se non riesci ad aggiungere un `<main>`, il markup standard di intestazione e piè di pagina (`<header>`, `<footer>`) o le varianti standard di Frammento esperienza intestazione e piè di pagina di AEM aiutano il controllo di audit a riconoscere ed escludere il colore della pagina.
* Se si contrassegnano intestazioni e piè di pagina a livello di sezione in `<article>`, `<section>` o `<aside>`, il contenuto presente in tali intestazioni e piè di pagina non verrà eliminato.

## Limitazioni note

Il controllo di audit si basa sul markup della pagina per distinguere il contenuto da chrome. In una pagina con **nessun `<main>`, nessun markup di riferimento standard e componenti intestazione/piè di pagina denominati in modo diverso dalle convenzioni di piattaforma**, parte del testo chrome può essere incluso nella misurazione oppure il testo creato può essere escluso occasionalmente. L&#39;aggiunta di un elemento `<main>` intorno al contenuto risolve ogni caso simile. Il controllo di audit non tenta di indovinare l’area del contenuto dalla densità del testo o dal layout visivo; si basa su segnali di markup in modo che i risultati siano prevedibili e ripetibili.

## Come risolvere

Quando il controllo di audit trova delle opportunità, ognuna di esse descrive il problema e la modifica consigliata. Per informazioni su come esaminare e risolvere le opportunità, vedere [Risultati dell&#39;audit in Verifica preliminare](../../audit-results.md).

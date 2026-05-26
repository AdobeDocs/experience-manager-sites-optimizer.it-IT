---
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
product: adobe experience manager
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
type: Documentation
description: Documentazione di AEM Sites Optimizer.
index: true
git-repo: https://github.com/AdobeDocs/experience-manager-sites-optimizer.it-IT
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: b6745249d9a773ce875f421dd16947a1a4d0a245
workflow-type: tm+mt
source-wordcount: 85
ht-degree: 2%

---


# Metadati per uso interno

Il sistema di authoring GitHub organizza i metadati gerarchicamente, utilizzando i seguenti livelli crescenti di precedenza.

1. metadata.md
1. ToC
1. Articolo

I metadati definiti nel file metadata.md si applicano all’intero archivio, ma possono essere ignorati a livello di sommario e di articolo. Eventuali esclusioni dei metadati devono essere eseguite al livello più basso possibile.

I metadati nell&#39;archivio `experience-manager-cloud-service.en` sono il minimo richiesto.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

Articolo

* `title`
* `description`
* `contentOwner` (solo sul contenuto della risorsa principale in `/help/assets`)


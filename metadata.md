---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Service dokumentation.
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.sv-SE
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 5bc43af20dc8893303b1d1f4dc70939631933eb7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Metadata för intern användning

Metadata i GitHub-redigeringssystemet är hierarkiska och definieras så här i ökande prioritetsnivåer.

1. metadata.md
1. TillC
1. Artikel

Metadata som definieras i filen metadata.md gäller för hela repon, men kan åsidosättas på ToC- och artikelnivå. Alla åsidosättningar av metadata bör göras på lägsta möjliga nivå.

Metadata i experience-manager-cloud-service.en repo är det minsta nödvändiga.

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

ToCS

* `sub-product`
* `user-guide-title`

Artikel

* `title`
* `description`
* `contentOwner` (endast när det gäller kärnmedieinnehåll under `/help/assets`)

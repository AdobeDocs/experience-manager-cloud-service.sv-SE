---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: ea71ca9fe259fbbf497a35930a10450bd4e26ce8
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 11382 {#release-11382}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 11382, som offentliggjordes den 28 mars 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 11289.

Funktionsaktiveringen för den här underhållsversionen ger dig den fullständiga funktionsuppsättningen. Se [aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) för fullständig information.

### Kända fel {#known-issues-11382}

- SITES-12573 - GraphQL-frågor som använder variabler i ett filter misslyckas om ingen variabel anges. Please do not update to this release shall you use GraphQL with AEM as a Cloud Service.
- SKYOPS-51970 - Identifierad regression för den FACT-version som används i buildImage-steget, vilket leder till att användarmappningen inte matchar.
- GRANITE-44542 - Problem har rapporterats för kunder som inte angav en paketnodtyp (genom att tillhandahålla en .content.xml med jcr:primaryType) för mappar som ingår i paketfiltret. Detta gjorde att mapparna behandlades som not:folder, vilket i olika fall orsakade problem.

### Åtgärdade problem {#fixed-issues-11382}

- ASSETS-21023 - Fast Smart Crop-återgivning, där kunderna kunde observera ett Null-pekarundantag i Publisher-instansen för alla AEM miljöer när de försökte få åtkomst till dessa återgivningar via API:t.
- SKYOPS-49280 - När du installerar en konfigurations- eller paketuppdatering med RDE i Publicera kanske resultatet inte blir observerbart eftersom publiceringsdispatcherns cache inte är ogiltig

#### Sites {#sites-issues-11382}

- SITES-7796 - Möjlighet för innehållsförfattare att publicera det Överordnad innehållsfragmentet och dess respektive variationer vid export till målgruppen
- SITES-97 - GraphQL: Sidnumrering och sortering, hybridfiltrering

>[!NOTE]
>
> I SITES-97 har vissa förbättringar gjorts i GraphQL-implementeringen som kan orsaka oväntat beteende. Se [AEM GraphQL ändringar gällande hantering av null-värden](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-21792.html) för mer information.

#### Assets {#assets-issues-11382}

- ASSETS-20076 - Lägg till stöd för videovattenstämplar som matchar det aktuella stödet för bildvattenstämplar
- ASSETS-21428 - tillägg av undantag för CSS-ändringar

#### Forms {#forms-issues-11382}

- CQ-4351502 - Uppdaterar användarmappningen för tjänsten så att läsåtkomst tillåts på webbplatser

#### Plattform {#platform-issues-11382}

- SITES-11040 - Villkorlig aktivering av GraphQL beständig frågecachelagring i dispatcher

### Inbäddade tekniker {#embedded-tech-11382}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API för Oak API 1.4.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | Version 2.27.0 | [API för Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.21.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

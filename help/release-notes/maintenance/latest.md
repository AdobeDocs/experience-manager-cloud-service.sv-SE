---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 19567 {#19567}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 19567, som offentliggjordes den 18 februari 2025. Den tidigare underhållsutgåvan släpptes 19352.

Funktionsaktiveringen i 2025.2.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-19567}

* GRANITE-56650: Innehållsdistribution bör endast signalblockera kön efter några försök
* SKYOPS-89616: Tillåt att skapa upp till 40 tekniska konton i Adobe Developer Console

### Åtgärdade problem {#fixed-issues-19567}

* CNTBF-232: Djuppaketets nt:file-noder som ska innehålla obligatorisk jcr:content child
* CQ-4358930: Prestandaproblem vid inläsning av sidegenskaper med många multifält
* GRANITE-55960: Prestandaproblem med Coral Select Field på AEM som Cloud Service
* GRANITE-56197: Det nya arbetsflödessteget TreeActivation grupperar inte resurser i en stor, platt mappstruktur

#### AEM Guides {#guides}

* GUIDES-23526: Vid uppdatering av villkor från mappprofilen förloras alla villkorsgrupper och villkoren förenklas.
* GUIDES-22574: Om en extern länk innehåller ett UUID, överförs den i efterbearbetningen och konverterar den externa länken till UUID-länken, vilket bryter länken i redigeraren och även på publiceringswebbplatserna.
* GUIDES-24983: När du kopierar en bild från en extern produkt (till exempel MS PowerPoint) och klistrar in den i stödlinjer, bryts funktionen att överföra resursen direkt för användning i filen.
* GUIDES-21772: Inbyggd PDF-generering misslyckas för innehåll med **segmentattributet** inställt på **to-content**.
* GUIDES-23964: När du väljer **Redigera egenskaper** visas inte de villkor för dynamisk baslinje som sparats tidigare i baslinjedialogrutan.
* GUIDES-19067: När du duplicerar en mappprofil kopieras även administratörsanvändarlistan från den ursprungliga mappprofilen

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-19567}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-19567}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-19567}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 21 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-19567}

| Teknik | Version | Länk |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

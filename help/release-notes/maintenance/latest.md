---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 859af15f4038b28e6e1398e5168dc008d22985e9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

>[!NOTE]
>
> Versionerna 20936 och 20783 har gjorts privata.

## Utgåva 20626 {#20626}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 20626, som offentliggjordes den 29 april 2025. Den tidigare underhållsutgåvan släpptes 20476.

Funktionsaktiveringen i 2025.5.0 innehåller alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-20626}

* ASSETS-46413, ASSETS-46580: En ny granskningsstatus,&quot;Preview&quot;, har lagts till.
* ASSETS-49542: Utökning av språk som stöds för video- och ljudtranskriberingar och översättning.
* ASSETS-48264: Stöd för utökning av PNG-kvalitet för återgivningar.

### Åtgärdade problem {#fixed-issues-20626}

* ASSETS-50387: Korrigera standardminiatyrbild för innehållsfragment för användning i GenStudio.
* ASSETS-49006: Visa videoegenskaper när användaren inte har skrivbehörighet.
* ASSETS-46757, ASSETS-46997: Förbättra tillgängligheten i den smarta beskärningsredigeraren.
* ASSETS-48018: Förbättra resursreferensspårningen i Assets Publish Report.
* ASSETS-35846: Förbättra åtkomsten mellan författare och leveransnivå.
* ASSETS-48171: Förbättra enhetligheten i dynamiska mediamallar med arbetsytan.
* ASSETS-49813: Förbättra förfallomeddelande.
* ASSETS-47768, ASSETS-49825, ASSETS-49008, ASSETS-48287: Förbättra hanteringen och synligheten i gruppåtgärder.
* ASSETS-50003, ASSETS-50004: Förbättra namngivningen och kontrollen över de återgivningar som ingår i en mediehämtning.
* ASSETS-47939: Förbättra svarsorganisationen för Content Hub.
* ASSETS-46738: Förbättra prestanda för mycket stora samlingar.
* ASSETS-50121: Förbättra tillförlitligheten för publicerade händelser.
* ASSETS-48490: Förbättra flexibiliteten i automatiserad bearbetning vid bildhantering.
* ASSETS-28106, ASSETS-49404: Förbättra tillförlitligheten i fulltextsökning.
* ASSETS-50006, ASSETS-50423: Förbättra prestanda för sökning och bläddring i stora mappar.
* ASSETS-46021: Förbättra videouppspelningen för Safari och mobilwebbläsare.
* ASSETS-49002: Förbättrad hantering av redigering av dynamiska mediamallar.
* ASSETS-48376: Diverse förbättringar i Content Hub-gränssnittet.
* ASSETS-48504, ASSETS-49378: Diverse förbättringar av gränssnittets beteende.
* ASSETS-49540: Flytta OpenAPI för resursrelationer från experimentfasen.
* ASSETS-40284: Uppdateringsdokumentation om Adobe Stock-integrering.
* ASSETS-49739: Arbeta för att integrera Figma från resursväljaren.

#### AEM Guides {#guides}

* GUIDES-21734: Nya ID:n kan inte generera för element när sådana element läggs till via fragment eller skapas via mallar, även när alternativet för automatisk generering av ID är aktiverat i XMLEditorConfig.
* GUIDES-25969: Om attributet `scope=external` saknas i externa länkar i ett DITA-avsnitt misslyckas publiceringen i HTML5 utan att ange de filer där attributet saknas i felloggarna, särskilt när mikrotjänsten är aktiverad.
* GUIDES-27288: Det går inte att skicka metadataegenskaperna för att mappa landningssidor som genererats med den nya AEM Sites-publiceringen.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-20626}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-20626}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-20626}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar elva identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-20626}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

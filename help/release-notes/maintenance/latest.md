---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5d00bed4008c70e81f3a70d219ddc411ec8bdc59
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 21484 {#21484}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 21484, som offentliggjordes den 10 juli 2025. Den tidigare underhållsutgåvan släpptes 21331.

Funktionsaktiveringen i 2025.7.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-21484}

Ingen.

### Åtgärdade problem {#fixed-issues-21484}

Ingen.

#### AEM Guides {#guides-21484}

* GUIDES-29781: När en XML-kommentar läggs till i ett element i Source-vyn försvinner inledande och avslutande blanksteg runt kommentaren när du byter vy.
* GUIDES-29078: När du öppnar ett ämne i redigeringsvyn efter att en webbläsare har uppdaterats behålls inte tidigare använda taggar på panelen Filegenskaper. Om du lägger till nya taggar skrivs de befintliga över, särskilt när ett stort antal taggar är tillgängliga för markering.
* GUIDES-28214: Försök att skapa granskningsåtgärder via AEM-arbetsflödet misslyckas konsekvent eftersom granskningsnoden inte skapas.
* GUIDES-28104: Om du publicerar en DITA-karta med attributet `chunk=to-content` skapas dubbletter av JCR-noder i nya AEM Sites-utdata, vilket leder till en överflödig innehållsstruktur i AEM Sites.
* GUIDES-29065, GUIDES-28793: Prestandaproblem som längre inläsningstider och återkommande timeout observeras när du arbetar med stora samlingar.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-21484}

* Den SDK som är tillgänglig i Software Distribution Portal har problem som körs lokalt. Fortsätt att använda den tidigare SDK-versionen för lokal testning.

### Föråldrade funktioner och API:er {#deprecated-21484}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-21484}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 5 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-21484}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.29.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |

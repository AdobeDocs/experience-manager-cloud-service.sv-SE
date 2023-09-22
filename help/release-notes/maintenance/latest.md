---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 13420 {#release-13420}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 13420, som offentliggjordes den 12 september 2023. Den här underhållsversionen ersätter version 13323.

2023.9.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-13420}

- ASSETS-19544: Resurser som senast ändrades av egenskapen ställs nu in på den användare som begär bearbetning.

### Åtgärdade problem {#fixed-issues-13420}

- ASSETS-27628: Felaktig kanalnod skapas när resurspanelen anpassas
- ASSETS-27539: Överför begränsningar för matchning av reguljära uttryck.
- ASSETS-26530: Enhetligt gränssnitt återför inte användare till originalsidan.
- ASSETS-22719: Hakparenteser i Namngivning av brytpunkter för smart beskärning bryter redigeringsfunktionen för smart beskärning.
- ASSETS-27726: linkshare.html ska inte indexeras av Google.
- ASSETS-27791: Validering av metadatamatchema utförs endast för det första fältet.
- ASSETS-25544: Korrigerad inaktiverad Cacheogiltighetsknapp för CDN.
- ASSETS-26575: Trunkering av fast namn när bilduppsättningar skapas.
- ASSETS-26705: Korrigerad onödig bearbetning av icke-DM-mappresurser och innehållsfragment.
- ASSETS-25740: Fasta skärmläsare utan berättarröst Namn och roll för Redigera/Beskär-kontroller på sidan Redigera smarta beskärningar med hjälp av nedpilstangenterna.
- CQ-4354266: Det går inte att öppna inkorgsobjekt.
- CQ-4354347: Uppdaterade AEM.
- DISP-1009: Användaren-agenten trimmar X-Forwarded-Host som icke-första huvud.
- Olika hjälpmedels- och säkerhetsrelaterade korrigeringar.

### Kända fel {#known-issues-13420}

Ingen.

### Inbäddade tekniker {#embedded-tech-13420}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

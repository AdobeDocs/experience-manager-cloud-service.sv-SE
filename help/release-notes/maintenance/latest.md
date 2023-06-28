---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: fd0b8ca281f35a92876f3c31baa4e17884f23948
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Version 12441 {#release-12441}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 12441, som offentliggjordes den 27 juni 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 12255.

2023.7.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lansering av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-12441}

- SITES-8769: Förbättra StyleImpl-anrop i ResponsiveGrid

### Åtgärdade problem {#fixed-issues-12441}

- Olika tillgänglighetsrelaterade uppdateringar
- SITES-12688: Sidredigeraren: Logiska operatorn ELLER fungerar inte korrekt i sökningen i Resurssökaren
- SITES-4951: Sidredigeraren: Taggar-sökning i sidredigeraren hittar inte undertaggar
- SITES-12465: Upplevelsefragment: Piltangenter fungerar inte i Experience fragment-komponentens dialogruta
- SITES-12893: Upplevelsefragment: Använd cirkulär referensvalidering för Experience Fragments
- SITES-12715: Upplevelsefragment: Konfigurationer av molntjänster som används i Experience fragments mapp finns inte kvar
- SITES-13097: Upplevelsefragment: Det går inte att lägga till upplevelsefragment i ett översättningsprojekt
- SITES-13165: GraphQL: Återställ standardbeteende för filtrering av null-värden
- SITES-12577: Länkkontroll: Transformatorn skriver inte om länkar ibland
- SITES-13559: MSM: Undantaget &#39;Är inte ändringsbart&#39; utlöses när komponenten rullas ut
- SITES-11757: MSM: Ärv utrullningskonfiguration från överordnad återställs inte för underordnade sidor
- SITES-14073: Webbplatsadministratör: CSV-rapporten misslyckas med 500 när ingen egenskap väljs för export

### Kända fel {#known-issues-12441}

Ingen.

### Inbäddade tekniker {#embedded-tech-12441}

| Teknik | Version | Länk |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | Version 2.27.0 | [API för Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |

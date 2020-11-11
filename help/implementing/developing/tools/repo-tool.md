---
title: AEM
description: AEM är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och den AEM servern via kommandoraden som kan jämföras med FTP.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# AEM {#aem-repo-tool}

AEM är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och den AEM servern via kommandoraden som kan jämföras med FTP. AEM Repo Tool liknar [Jackrabbit FileVault Maven plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin), men är snabbare, har minimalt med beroenden och är ett enkelt basskript.

Detta verktyg förenklar filöverföringen för utvecklaren och kan även integreras i Eclipse och IntelliJ för att göra utvecklingen ännu effektivare.

## Översikt {#overview}

För en given sökväg i en `jcr_root` FileVault-struktur i filsystemet skapar AEM-postverktyget ett paket med ett enda filter för hela underträdet och överför det till servern (liknar FTP `put`), hämtar det från servern ( `get`) eller jämför skillnaderna ( `status` och `diff`).

Verktyget stöder inte flera filtersökvägar eller FileVault-sökvägar `filter.xml`.

>[!CAUTION]
>
>Observera att AEM alltid skriver över hela filen eller katalogen som anges.

## Ladda ned och dokumentation {#download-and-documentation}

Verktyget [AEM finns på GitHub via den här länken](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) tillsammans med detaljerade installations- och användningsanvisningar.

Om du vill hämta källan till AEM kan du läsa GitHub-projektet som är länkat nedan.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna verktygsprojekt på GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

---
title: AEM Repo Tool
description: AEM Repo Tool är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och AEM-servern via kommandoraden som kan jämföras med FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och AEM-servern via kommandoraden som kan jämföras med FTP. AEM Repo Tool liknar [Jackrabbit FileVault Maven plugin](https://jackrabbit.apache.org/filevault-package-maven-plugin) men är snabbare, har minimalt med beroenden och är ett enkelt basskript.

Detta verktyg förenklar filöverföringen för utvecklaren och kan även integreras i Eclipse och IntelliJ för att göra utvecklingen ännu effektivare.

## Ökning {#overview}

För en given sökväg i en `jcr_root` FileVault-struktur i filsystemet skapar AEM Repo-verktyget ett paket med ett enda filter för hela underträdet och skickar det till servern (liknande FTP `put`), hämtar det från servern ( `get`) eller jämför skillnaderna ( `status` och `diff`).

Verktyget stöder inte flera filtersökvägar eller FileVault-objektets `filter.xml`.

>[!CAUTION]
>
>AEM Repo-verktyget skriver alltid över hela filen eller katalogen som anges.

## Ladda ned och dokumentation {#download-and-documentation}

[AEM Repo Tool är tillgängligt på GitHub via den här länken](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) tillsammans med detaljerade installations- och användningsanvisningar.

Om du vill hämta källan till AEM Repo Tool läser du GitHub-projektet som är länkat nedan.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna verktygsprojekt på GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

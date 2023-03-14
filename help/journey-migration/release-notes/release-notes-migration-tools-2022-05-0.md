---
title: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.5.0
description: Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.5.0
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
source-git-commit: 01c4a21b980918ba99ac174419d80b577bc96dda
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 2%

---

# Versionsinformation för migreringsverktyg i AEM as a Cloud Service version 2022.5.0 {#release-notes}

Den här sidan innehåller versionsinformation för migreringsverktyg i AEM as a Cloud Service 2022.5.0.

## Best Practices Analyzer {#bpa-release}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.30 är 1 juni 2022.

### Nyheter {#what-is-new-bpa}

* Möjlighet att identifiera och rapportera användning av anpassade dialogrutewidgetar med hjälp av CoralUI- och Classic-dialogrutewidgetar. Vi rekommenderar att du konverterar anpassade widgetar för klassisk dialog från ExtJS till CoralUI. Anpassade widgetar för Coral Dialog bör uppdateras till CoralUI3.
* Möjlighet att identifiera och rapportera om användning och version av Assets Share Commons. Resursdelningskommentarer 1.x stöds inte på AEM as a Cloud Service och måste uppgraderas till 2.x.
* Möjlighet att upptäcka och rapportera antalet noder från versioner.
* Möjlighet att identifiera och rapportera om anpassade replikeringsagenter eller replikeringsagenter som har ändrats.

### Felkorrigeringar {#bug-fixes-bpa}

* BPA rapporterade NCC (ej kompatibla ändringar), UMI (Upgrade Misconfiguration Issue) och PCX (Page Complexity)-resultat som är falskt positiva. De här har åtgärdats.
* BPA rapporterade fel när en nodnamnslängd överskred 150 byte. Detta har åtgärdats för att identifiera sådana fel endast när den överordnade noden är lika med eller större än 350 byte.

## Content Transfer Tool {#ctt-release}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v2.0.10 är 2 juni 2022.

### Nyheter {#what-is-new-ctt}

* Verktyget för innehållsöverföring (CTT) har utvecklats för att fungera ihop med Cloud Acceleration Manager för att effektivisera hela innehållsöverföringsprocessen. CTT fokuserar nu på att utföra innehållsextraheringar. CTT-tjänsten för förtäring är nu integrerad i Cloud Acceleration Manager. Fördelarna med den här utvecklingen är:
   * Självbetjäning för att extrahera en migreringsuppsättning en gång och importera den i flera miljöer parallellt.
   * Förbättrad användarupplevelse tack vare bättre inläsningstillstånd, skyddsanvisningar och felhantering.
   * Inmatningsloggarna sparas och är alltid tillgängliga för felsökning.

## Cloud Acceleration Manager {#cam-release}

### Releasedatum {#release-date-cam}

Releasedatum för Cloud Acceleration Manager är 2 juni 2022.

### Nyheter {#what-is-new-cam}

* Med Cloud Acceleration Manager kan användare nu starta och hantera innehållsöverföringar för att flytta innehåll från en kunds AEM (lokala eller Adobe Managed Services) till AEM as a Cloud Service som en del av ett migreringsprojekt. Se [Använda innehållsöverföringskort](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) för mer information.

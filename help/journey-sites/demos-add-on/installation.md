---
title: Förstå installationen av tilläggsprogrammet för referensdemo
description: Lär dig mer om Cloud Manager och hur det används för att installera tillägget.
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Förstå installationen av tilläggsprogrammet för referensdemo {#understand-installation}

Lär dig mer om Cloud Manager och hur det används för att installera tillägget.

>[!TIP]
>
>Om du redan har erfarenhet av Cloud Manager eller vill gå direkt till konfiguration och användning av tillägget kan du hoppa till [Skapa ett program och en pipeline](create-program.md)
>
>Om du vill veta hur Cloud Manager och AEM samarbetar för att skapa din demomiljö och hur du konfigurerar och använder din egen, ska du fortsätta att läsa det aktuella dokumentet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur installationsprocessen för tillägget Referensdemonstrationer fungerar, vilket illustrerar hur de olika delarna fungerar tillsammans. När du har läst bör du:

* Få en grundläggande förståelse för Cloud Manager.
* Förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Se hur mallarna kan skapa nya webbplatser med demomaterial med bara några klick.

Det här dokumentet fokuserar på att förstå dessa grundläggande delar i AEM Reference Demo Add-On innan du går vidare till nästa steg på resan där du börjar installera.

Även om vi rekommenderar att du går igenom den här resan steg för steg, kan du hoppa till [Skapa ett program och en pipeline](create-program.md)

## Ansvarig roll {#responsible-role}

Den här resan gäller en systemadministratör som är medlem i **Företagsägare** roll i Cloud Manager för din organisation.

## Krav och krav {#requirements-prerequisites}

Det finns minimala krav att lära sig om och börja använda tillägget Referensdemonstrationer.

### Kunskap {#knowledge}

* Grundläggande kunskaper i Cloud Manager

### verktyg {#tools}

* Bli medlem i **Företagsägare** roll i Cloud Manager för din organisation

## Om Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för plattformen.

Cloud Manager används för att administrera de molnresurser som stöder dina AEM projekt, inklusive de miljöer och verktyg som behövs. För den här resan behövs ingen fullständig förståelse för Cloud Manager. Du måste dock känna till några grundläggande begrepp.

>[!TIP]
>
>Om du vill veta mer om Cloud Manager i detalj kan du läsa [Ytterligare resurser](#additional-resources) i den här artikeln om du vill ha länkar till mer information.

### Program {#programs}

När du loggar in i Cloud Manager har du tillgång till en eller flera **program**. Ett program kan definieras på många olika sätt, men det är enklast att tänka på att det är kopplat till de webbplatser och upplevelser som är kopplade till en varumärkesidentitet.

Om du loggar in på Cloud Manager som representerar **WKND Resor- och äventyföretag** kan du skapa en **WKND Nightlife** program och **WKND-projekt** program. Båda dessa program har AEM miljöer för hantering av associerade platser.

### Sandlådor {#sandboxes}

Program kan vara antingen produktionsprogram eller sandlådeprogram.

* **Ett produktionsprogram** skapas för att så småningom tillåta livstrafik när ditt program är klart att användas live.
* **Ett sandlådeprogram** har skapats för utbildning, löpande demonstrationer, aktivering, POC, osv. och är inte avsedd för livstrafik.

För att kunna installera tillägget AEM Reference Demos måste du skapa ett nytt sandlådeprogram.

>[!NOTE]
>
>AEM Reference Demos Add-On är bara tillgänglig i sandlådeprogram.

## Installation och användningsflöde {#installation-flow}

Nu när du förstår några grundläggande begrepp i Cloud Manager är installationen av AEM Reference Demos Add-On begreppsmässigt enkel.

1. Logga in i Cloud Manager.
1. Skapa en ny sandlåda AEM och aktivera AEM Reference Demos Add-On som ett alternativ för programmet.
1. Demonsinnehållet och konfigurationen distribueras till programmet. Demonsinnehållet innehåller:
   * Webbplatsmallar som används för att skapa olika AEM sajter med AEM funktioner, förifyllda med exempel på bästa praxis.
   * Konfigurationsverktyg för att hantera demoinnehåll.
1. Logga in i AEM i ditt nya sandlådeprogram och använd verktyget för att snabbt skapa webbplatser och skapa demowebbplatser baserade på mallarna.
1. Använd konfigurationsverktygen för att hantera demowebbplatser och -mallar, inklusive att ta bort dem när de inte längre behövs.

## AEM webbplatsmallar {#site-templates}

AEM är paket som innehåller fördefinierat innehåll och struktur för en plats. Webbplatsmallar kan anpassas efter behoven i specifika projekt, så när AEM skapar nya webbplatser kan de välja bland mallar som passar deras ärenden.

Tillägget AEM Reference Demos innehåller flera mallar för olika test- och demonstrationsbehov. När du har skapat programmet och distribuerat pipeline för att installera tillägget kan du logga in på AEM och skapa webbplatser baserade på många demomallar

## What&#39;s Next {#what-is-next}

Nu när du har slutfört den här delen av AEM Reference Demos Add-On-resan bör du:

* Få en grundläggande förståelse för Cloud Manager.
* Förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Se hur mallarna kan skapa nya webbplatser med demomaterial med bara några klick.

Bygg vidare på den här kunskapen och fortsätt din AEM snabbwebbplats genom att nästa gång du granskar dokumentet [Skapa ett program och en pipeline,](create-program.md) där du får lära dig hur du konfigurerar ett nytt program och en ny pipeline för att distribuera tillägget.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av processen Skapa snabbwebbplats genom att granska dokumentet [Skapa ett program och en pipeline,](create-program.md) Nedan följer ytterligare, valfria resurser som fördjupar sig i några koncept som nämns i det här dokumentet, men som inte behöver fortsätta på resan.

* [Program och programtyper](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html) - Börja här för att förstå skillnaden mellan live- och sandlådeprogram.
* [Webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) - Om du vill veta mer om strukturen för webbplatsmallar och hur de används för att skapa webbplatser kan du läsa det här dokumentet.
* [Dokumentation för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Om du vill ha mer information om funktionerna i Cloud Manager kan du läsa de detaljerade tekniska dokumenten direkt.

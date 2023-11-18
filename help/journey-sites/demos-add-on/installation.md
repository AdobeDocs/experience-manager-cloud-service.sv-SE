---
title: Förstå installationen av tilläggsprogrammet för referensdemo
description: Lär dig mer om Cloud Manager och hur det används för att installera tillägget.
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Förstå installationen av tilläggsprogrammet för referensdemo {#understand-installation}

Lär dig mer om Cloud Manager och hur det används för att installera tillägget.

>[!TIP]
>
>Om du har erfarenhet av Cloud Manager eller vill gå direkt till konfiguration och användning av tillägget går du vidare till [Skapa ett program och en pipeline](create-program.md)
>
>Om du vill lära dig hur Cloud Manager och AEM samarbetar för att skapa din demomiljö och hur du konfigurerar och använder din egen, kan du fortsätta att läsa det aktuella dokumentet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur installationsprocessen för tillägget Referensdemonstrationer fungerar, vilket illustrerar hur de olika delarna fungerar tillsammans. När du har läst bör du:

* Få en grundläggande förståelse för Cloud Manager.
* Förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Se hur mallarna kan skapa webbplatser med demomaterial med bara några klick.

Det här dokumentet fokuserar på att förstå dessa grundläggande delar i AEM Reference Demo Add-on innan du går vidare till nästa steg på resan där du börjar installera.

Vi rekommenderar att du går igenom den här resan, men om du har erfarenhet av Cloud Manager eller vill gå direkt till konfiguration och användning av tillägget går du till [Skapa ett program och en pipeline](create-program.md).

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
>Om du vill lära dig mer om Cloud Manager i detalj kan du läsa [Ytterligare resurser](#additional-resources) i den här artikeln om du vill ha länkar till mer information.

### Program {#programs}

När du loggar in i Cloud Manager har du tillgång till en eller flera **program**. Ett program kan definieras på många olika sätt, men det är enklast att tänka på att det är kopplat till de webbplatser och upplevelser som är kopplade till en varumärkesidentitet.

Om du loggar in på Cloud Manager som representerar **WKND Resor- och äventyföretag** kan du skapa en **WKND Nightlife** program och **WKND-projekt** program. Båda dessa program har AEM miljöer för hantering av associerade platser.

### Sandlådor {#sandboxes}

Program kan vara antingen produktionsprogram eller sandlådeprogram.

* **Ett produktionsprogram** skapas för att så småningom tillåta livstrafik när ditt program är klart att användas live.
* **Ett sandlådeprogram** skapas för utbildning, löpande demos, aktivering, POC och så vidare, och är inte avsedd för livtrafik.

Skapa ett sandlådeprogram om du vill installera AEM Reference Demos Add-on.

>[!NOTE]
>
>Tillägget AEM Reference Demos är bara tillgängligt i sandlådeprogram.

## Installations- och användningsflöde {#installation-flow}

Nu när du förstår några grundläggande begrepp i Cloud Manager är det begreppsmässigt enkelt att installera tillägget AEM referensdemonstrationer.

1. Logga in i Cloud Manager.
1. Skapa ett sandlådeprogram AEM och aktivera AEM Reference Demos Add on som ett alternativ för programmet.
1. Demonsinnehållet och konfigurationen distribueras till programmet. Demonsinnehållet innehåller:
   * Webbplatsmallar som används för att skapa olika AEM sajter med AEM funktioner, förifyllda med exempel på bästa praxis.
   * Konfigurationsverktyg för att hantera demoinnehåll.
1. Logga in i AEM i ditt nya sandlådeprogram och använd verktyget för att snabbt skapa webbplatser och skapa demosajter baserat på mallarna.
1. Använd konfigurationsverktygen för att hantera demowebbplatser och -mallar, inklusive att ta bort dem när de inte längre behövs.

## AEM webbplatsmallar {#site-templates}

AEM är paket som innehåller fördefinierat innehåll och struktur för en plats. Webbplatsmallar kan anpassas efter behoven i specifika projekt, så när AEM skapar webbplatser kan de välja bland mallar som gäller för deras affärsärenden.

Tillägget AEM Reference Demos innehåller flera mallar för olika test- och demonstrationsbehov. När du har skapat programmet och distribuerat pipeline för att installera tillägget kan du logga in på AEM och skapa webbplatser baserade på många demomallar

## What&#39;s Next {#what-is-next}

Nu när du har slutfört den här delen av AEM Reference Demos Add-on:

* Få en grundläggande förståelse för Cloud Manager.
* Förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Se hur mallarna kan skapa webbplatser med demomaterial med bara några klick.

Bygg vidare på den här kunskapen och fortsätt din AEM snabbwebbplats genom att granska [Skapa ett program och en pipeline,](create-program.md) där du får lära dig hur du konfigurerar ett nytt program och en ny pipeline för att distribuera tillägget.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av snabbplatsgenereringen genom att granska [Skapa ett program och en pipeline](create-program.md)är följande ytterligare, valfria resurser: Dessa resurser tar en djupdykning i de begrepp som nämns i det här dokumentet. De behöver dock inte fortsätta resan.

* [Program och programtyper](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html) - Börja här för att förstå skillnaden mellan live- och sandlådeprogram.
* [Webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) - Om du vill veta mer om strukturen för webbplatsmallar och hur de används för att skapa webbplatser kan du läsa det här dokumentet.
* [Dokumentation för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Om du vill ha mer information om funktionerna i Cloud Manager kan du läsa de detaljerade tekniska dokumenten direkt.

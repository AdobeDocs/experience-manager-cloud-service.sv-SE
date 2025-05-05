---
title: Förstå installationen av tilläggsprogrammet för referensdemo
description: Läs om Cloud Manager och hur det används för att installera tillägget.
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Förstå installationen av tilläggsprogrammet för referensdemo {#understand-installation}

Läs om Cloud Manager och hur det används för att installera tillägget.

>[!TIP]
>
>Om du har erfarenhet av Cloud Manager eller vill gå direkt till konfiguration och användning av tillägget går du till [Skapa ett program och en pipeline](create-program.md)
>
>Om du vill veta hur Cloud Manager och AEM samarbetar för att skapa en demomiljö och hur du konfigurerar och använder en egen, kan du fortsätta att läsa det aktuella dokumentet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur installationsprocessen för tillägget Referensdemonstrationer fungerar, vilket illustrerar hur de olika delarna fungerar tillsammans. När du har läst bör du:

* Få en grundläggande förståelse för Cloud Manager.
* Förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Se hur mallarna kan skapa webbplatser med demomaterial med bara några klick.

Det här dokumentet fokuserar på att förstå dessa grundläggande delar i AEM Reference Demo Add-on innan du går vidare till nästa steg på resan där du börjar installera.

Vi rekommenderar att du går igenom den här resan, men om du har erfarenhet av Cloud Manager, eller vill gå direkt till konfiguration och användning av tillägget, går du till [Skapa ett program och en pipeline](create-program.md).

## Ansvarig roll {#responsible-role}

Den här resan gäller en systemadministratör som är medlem av rollen **Business Owner** i Cloud Manager för din organisation.

## Krav och krav {#requirements-prerequisites}

Det finns minimala krav att lära sig om och börja använda tillägget Referensdemonstrationer.

### Kunskap {#knowledge}

* Grundläggande kunskaper i Cloud Manager

### verktyg {#tools}

* Bli medlem i rollen **Business Owner** i Cloud Manager för din organisation

## Förstå Cloud Manager {#cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för plattformen.

Cloud Manager används för att administrera de molnresurser som stöder dina AEM projekt, inklusive de miljöer och verktyg som behövs. För denna resa behövs ingen fullständig förståelse av Cloud Manager. Du måste dock känna till några grundläggande begrepp.

>[!TIP]
>
>Om du vill lära dig mer om Cloud Manager i detalj kan du läsa avsnittet [Ytterligare resurser](#additional-resources) i den här artikeln för att få länkar till mer information.

### Program {#programs}

När du loggar in på Cloud Manager har du tillgång till ett eller flera **program**. Ett program kan definieras på många olika sätt, men det är enklast att tänka på att det är kopplat till de webbplatser och upplevelser som är kopplade till en varumärkesidentitet.

Om du loggar in på Cloud Manager som representerar **WKND Travel and Adventure Enterprises** kan du skapa ett **WKND Nightlife** -program och ett **WKND Backhem Projects** -program. Båda dessa program har AEM miljöer för hantering av associerade platser.

### Sandlådor {#sandboxes}

Program kan vara antingen produktionsprogram eller sandlådeprogram.

* **Ett produktionsprogram** skapas för att så småningom tillåta livstrafik när ditt program är klart att användas live.
* **Ett sandlådeprogram** har skapats för utbildning, körning av demos, aktivering, POC och så vidare, och är inte avsett för direkttrafik.

Skapa ett sandlådeprogram om du vill installera AEM Reference Demos Add-on.

>[!NOTE]
>
>Tillägget AEM Reference Demos är bara tillgängligt i sandlådeprogram.

## Installations- och användningsflöde {#installation-flow}

Nu när du förstår några grundläggande begrepp i Cloud Manager är installationen av tillägget AEM Reference Demos enkelt att komma igång med.

1. Logga in på Cloud Manager.
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

Bygg vidare på den här kunskapen och fortsätt din resa med att skapa AEM genom att granska [Skapa ett program och en pipeline](create-program.md), där du får lära dig hur du konfigurerar ett nytt program och en pipeline för att distribuera tillägget.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av processen Skapa snabbwebbplats genom att granska [Skapa ett program och en pipeline](create-program.md), men följande är ytterligare, valfria resurser. Dessa resurser tar en djupdykning i de begrepp som nämns i det här dokumentet. De behöver dock inte fortsätta resan.

* [Förstå program och programtyper](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html?lang=sv-SE) - Börja här för att förstå skillnaderna mellan live- och sandlådeprogram.
* [Webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) - Om du vill veta mer om strukturen för webbplatsmallar och hur de används för att skapa webbplatser läser du det här dokumentet.
* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=sv-SE) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.

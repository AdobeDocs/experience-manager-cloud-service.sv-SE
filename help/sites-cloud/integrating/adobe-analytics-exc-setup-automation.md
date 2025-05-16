---
title: Integrera Adobe Analytics med Experience Cloud Setup Automation
description: Experience Cloud Setup Automation är ett enkelt och automatiserat sätt att integrera och instrumentera Experience Manager Sites med Experience Platform Tags och Adobe Analytics med ett enkelt gränssnitt. Lär dig hur du använder den automatiska konfigurationen med din egen webbplats.
feature: Integration
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
solution: Experience Manager Sites
source-git-commit: 4a3e65ef6a8aa08c8bc78db31f94272334994ac5
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Integrera Adobe Analytics med Experience Cloud Setup Automation {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
>Experience Cloud Setup Automation-funktionen är föråldrad.

Experience Cloud Setup Automation är ett enkelt och automatiserat sätt att integrera och instrumentera Experience Manager Sites med Experience Platform Tags och Adobe Analytics med ett enkelt gränssnitt.

Det har aldrig varit enklare att integrera Adobe Analytics med AEM Sites. Med Experience Cloud Setup Automation kan du konfigurera, integrera och instrumentera din webbplats för att få en inblick i hur väl era kunder engagerar och konverterar med bara några klick.

I den här videon utforskas hur en AEM-webbplats är integrerad med Experience Platform Tags and Analytics med Experience Cloud Setup Automation:

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## Krav

Automatiseringskonfigurationen är utformad för att fungera direkt med en AEM-webbplats som byggts med [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) med [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) aktiverad. Du kan skapa en ny webbplats som har dessa funktioner aktiverade automatiskt med [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) eller genom att skapa en webbplats med en [webbplatsmall](/help/journey-sites/quick-site/create-site.md).

## Förutsättningar {#prerequisites}

Innan du använder den här funktionen är det viktigt att du följer dessa anvisningar för att säkerställa att de nödvändiga tjänsterna har konfigurerats korrekt i din miljö:

1. Logga in på Adobe Admin Console (https://adminconsole.adobe.com/).
1. Kontrollera att rätt IMS-organisations-ID är markerat i det övre högra hörnet.
1. Klicka på navigeringsalternativet Produkter.
1. Kontrollera att&quot;Adobe Experience Manager as a Cloud Service&quot; har etablerats för IMS-organisationen.
1. Kontrollera att&quot;Adobe Analytics&quot; har etablerats för IMS-organisationen.
1. Gå till Cloud Manager (https://experience.adobe.com/cloud-manager).
1. Välj lämpligt program.
1. Kontrollera att miljön finns i den senaste versionen av Cloud Service (om så inte är fallet väljer du Uppdatera i menyalternativen).
1. Kör en pipeline i Full Stack i Cloud Manager.

Miljön bör nu vara redo för Experience Cloud Setup Automation.

## Så här konfigurerar du

1. Navigera till **Webbplatser** och markera roten för webbplatsen som ska integreras med Adobe Analytics.
1. Expandera sidofältets meny och välj **Konfigurera analys**.

   Det här är ett nytt alternativ på sidospåret som öppnar en panel med kontroller och status för Experience Cloud Setup Automation.
1. Välj knappen **Integrera analys** .
1. Ange ett namn för **Report Suite-ID** i den dialogruta som visas.

   Den här strängen används för att skapa ett [Report Suite-ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html) i Adobe Analytics som datalager för analysdata för den valda AEM-webbplatsen. Den angivna strängen har bifogats med miljö- och skiktidentifierare för att säkerställa unikt utseende.

1. Uppdatera sidan och panelen och välj **Kontrollera integreringsstatus** för att kontrollera automatiseringsstatus.

   Automatiseringsinställningarna görs asynkront. **Kontrollera integreringsstatus** visar integreringens aktuella status.

   * **Pågår** - anger att jobbet körs.
   * **Integreringen är slutförd** - anger att jobbet har slutförts genom att integrera analys och taggar, konfigurera taggtillägg och taggar samt skapa den nya rapportsviten i Adobe Analytics.
   * **Fel** - anger att det automatiska jobbet inte kunde slutföras. Kontrollera loggfilerna för det här jobbet genom att klicka på länken Loggar.

## Validera AEM-konfiguration

När automatiseringen är klar validerar du att webbplatsen nu kör Analytics-händelserna.

1. Öppna en sida på webbplatsen med **webbplatsredigeraren**.
1. Använd alternativet **Visa som publicerad** om du vill läsa in en publicerad version av sidan.
1. Använd utvecklarverktygen i webbläsaren för att kontrollera nätverkstrafiken och att **taggar** och `AppMeasurement.js` filer nu läses in.
1. Kontrollera webbläsarens konsol för att se att händelser på sid- och komponentnivå utlöses och samlas in av Adobe Client Data Layer.

## Validera Analytics-konfiguration

Navigera sedan till Adobe Analytics för att visa data som flödar in från händelser på AEM webbplats.

1. Navigera till Adobe Analytics i samma IMS-organisation som din AEM-webbplats.
1. Skapa en ny översiktsrapport för AEM Sites genom att navigera till **Rapporter** > **engagemang** > **Adobe Experience Manager** > **Platsprestandaöversikt**.
1. Välj **Öppna rapport**.
1. Välj det **Report Suite-ID** som matchar namnet på Report Suite som användes i föregående övning.
1. Visa dataflödet för analyser i den nya mallen över tid.

   >[!NOTE]
   >
   > Med en ny integrering kan det ta några timmar innan rapporten fylls med data.

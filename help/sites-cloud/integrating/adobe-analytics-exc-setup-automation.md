---
title: Integrera Adobe Analytics med Experience Cloud Setup Automation
description: Experience Cloud Setup Automation är ett enkelt och automatiserat sätt att integrera och instrumentera Experience Manager Sites med Experience Platform Launch och Adobe Analytics med ett enkelt gränssnitt. Lär dig hur du använder den automatiska konfigurationen med din egen webbplats.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
source-git-commit: 6c84c0eff6392f1f86c18c9daf15c402c4d9e778
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Integrera Adobe Analytics med Experience Cloud Setup Automation {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> Den här funktionen finns för närvarande i en intern betaversion. Målversionen är Q1 2022.

Experience Cloud Setup Automation är ett enkelt och automatiserat sätt att integrera och instrumentera Experience Manager Sites med Experience Platform Launch och Adobe Analytics med ett enkelt gränssnitt.

Det har aldrig varit enklare att integrera Adobe Analytics med AEM Sites. Med Experience Cloud Setup Automation kan du konfigurera, integrera och instrumentera din webbplats för att få en inblick i hur väl era kunder engagerar och konverterar med bara några klick.

I den här videon utforskas hur en AEM sajt integreras med Experience Platform Launch och Analytics med Experience Cloud Setup Automation:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Krav

Automatiseringskonfigurationen är utformad för att fungera direkt med en AEM sajt som byggts med [AEM kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) med [Adobe-klientdatalager](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) aktiverat. Du kan skapa en ny webbplats där dessa funktioner aktiveras automatiskt med [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) eller genom att skapa en plats med en [Webbplatsmall](/help/journey-sites/quick-site/create-site.md).

## Så här konfigurerar du

1. Navigera till **Webbplatser** och välj roten på webbplatsen som ska integreras med Adobe Analytics.
1. Expandera menyn för sidospåret och tryck **Konfigurationsanalys**.

   Det här är ett nytt alternativ på sidospåret som öppnar en panel med kontroller och status för Experience Cloud Setup Automation.
1. Tryck på **Integrera analyser** -knappen.
1. Ange ett namn för **Report Suite-ID**.

   Strängen används för att skapa en ny [Report Suite-ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) i Adobe Analytics som datalager för analysdata för den valda AEM. Den angivna strängen läggs till med miljö- och skiktidentifierare för att säkerställa unikt utseende.

1. Uppdatera sidan och panelen och tryck på **Kontrollera integreringsstatus** för att kontrollera automatiseringsstatus.

   Automatiseringsinställningarna görs asynkront. The **Kontrollera integreringsstatus** visar integreringens aktuella status.

   * **Pågår** - anger att jobbet körs.
   * **Integreringen är klar** - anger att jobbet har slutfört integreringen av Analytics och Launch, konfigureringen av Launch-tillägg och Launch-regler samt skapandet av nya Report Suite i Adobe Analytics.
   * **Fel** - anger att det automatiska jobbet inte kunde slutföras. Kontrollera loggfilerna för det här jobbet genom att klicka på länken Loggar.

## Validera AEM

När automatiseringen är klar validerar du att webbplatsen nu kör Analytics-händelserna.

1. Öppna en sida på webbplatsen med **Webbplatsredigeraren**.
1. Använd **Visa som publicerad** om du vill läsa in en publicerad version av sidan.
1. Använd webbläsarens utvecklarverktyg för att inspektera nätverkstrafiken och att **Starta** och `AppMeasurement.js` filer läses nu in.
1. Inspect är webbläsarens konsol för att se att händelser på sid- och komponentnivå utlöses och samlas in av Adobe Client Data Layer.

## Validera Analytics-konfiguration

Navigera sedan till Adobe Analytics för att visa data som flödar in från händelser på AEM webbplats.

1. Navigera till Adobe Analytics i samma IMS-organisation som din AEM.
1. Skapa en ny översiktsrapport för AEM Sites genom att navigera till **Rapporter** > **Engagemang** > **Adobe Experience Manager** > **Översikt över webbplatsprestanda**.
1. Tryck **Öppna rapport**.
1. Välj **Report Suite-ID** som matchar namnet på Report Suite som användes i föregående övning.
1. Visa dataflödet för analyser i den nya mallen över tid.

   >[!NOTE]
   >
   > Med en ny integrering kan det ta några timmar innan rapporten fylls med data.

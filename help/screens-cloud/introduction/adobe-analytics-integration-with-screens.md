---
title: Adobe Analytics Integration med AEM Screens
seo-title: Adobe Analytics Integration with AEM Screens
description: Följ den här sidan om du vill veta mer om hur AEM Screens kan integreras med Adobe Analytics och få ett spelbevis.
seo-description: Follow this page to learn about out of the box integration of AEM Screens with Adobe Analytics and provides you with a proof of play.
uuid: 80d61af7-bf4d-46ca-a026-99a666c2e1a0
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
discoiquuid: b1a0e00e-0368-42c9-8bcd-5f00b4d0990c
docset: aem65
role: Admin, Developer
level: Intermediate
source-git-commit: bf0a841a5cd5eb278fd3d59484c84d1cee172b4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Adobe Analytics Integration med AEM Screens {#adobe-analytics-integration-with-aem-screens}

Detta avsnitt behandlar följande ämnen:

* **Översikt**
* **Arkitekturinformation**

## Översikt {#overview}

***AEM Screens*** utnyttjar Adobe Analytics och med det kan ni uppnå något unikt på marknaden - flerkanalsanalyser som hjälper er att korrelera innehåll som visas på plats med andra datakällor.

AEM Screens är en färdig integrerad lösning med Adobe Analytics och ger dig ett bevis på uppspelning.

I det här avsnittet beskrivs följande funktioner som används för att ansluta ett AEM Screens-projekt till Adobe Analytics:

* Tillåter att uppspelningsrapportering kan styrkas per enhet
* Tillåter granskning av uppspelningsrapportering efter tillgång
* Ser till att alla spelarhändelser hämtas och tidsstämplas
* Ser till att alla spelarhändelser lagras lokalt om uppspelningen inte är ansluten till ett nätverk
* Gör det möjligt att skapa feedbackslingor som spårar uppspelningshändelser över tid
* Tillåter systemet att ändra innehåll och layouter baserat på kriterier som innehållets författare har definierat

Adobe Analytics Integration med AEM Screens har alltså följande begränsningar *mål*:

* Aktivera ROI från implementering av digitala signaturer
* Integrera Analytics som grund för att i framtiden kunna samla in och analysera användningsinformation

## Arkitekturinformation {#architectural-details}

En AEM Screens-kund vill förstå vilket innehåll som visades vid vilken tidpunkt och hur länge (aggregerat). Detta är en vanlig funktion för signeringslösning. I stället för att bygga upp våra egna analyser kommer AEM Screens att utnyttja Adobe Analytics, och med det kan vi uppnå något unikt på marknaden - flerkanalsanalyser som hjälper till att korrelera innehåll som visas på plats med andra datakällor.

I följande diagram förklaras Adobe Analytics Integration med AEM Screens:

![Integrering med Adobe Analytics](/help/screens-cloud/assets/analytics-architecture.png)

## Aktivera Adobe Analytics i AEM Screens moln {#enabling-adobe-analytics-in-aem-screens-cloud}

Kontakta din Adobe Relationship Manager för att aktivera Adobe-analys i Screens Cloud.

## Skärmanalys: Aktiveringsflöde {#screens-analytics-enablement-flow}

>[!CAUTION]
>
>Innan du konfigurerar egenskaperna bör du kontakta din Adobe Relationship Manager och skapa en biljett för att få en **API-nyckel för analyser** och **Analysprojekt** för AEM Screens.

## Använda Adobe Analytics-tjänsten i AEM Screens {#using-adobe-analytics-service-in-aem-screens}

Det här scenariot anropar Analytics API via REST-anrop från en analystjänst i den inbyggda programvaran och kärnkomponenter för instrumentskärmar för att explicit skapa och skicka händelser som är specifika för ett visst användningsfall, samtidigt som det tillåter utökningsmöjligheter där anpassade meddelanden kan skickas till Analytics från en anpassad utvecklad kanal.

Analyshändelser lagras offline i indexedDB och sedan i chunked-läge och skickas till molnet.

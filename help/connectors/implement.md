---
title: Implementera en AEM Connector
description: Lär dig mer om kopplingar, vad de kan göra och hur du implementerar dessa värdefulla verktyg i Experience Manager.
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 07db10c4ee9cced7b6a697fe4f41c99eaba6a39f
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 7%

---


Implementera en AEM Connector
=============================

Nedan finns användbara referenser för att bygga [AEM-kopplingar](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) och de bör läsas tillsammans med riktlinjerna för hur kopplingar [skickas in](submit.md) och [underhålls](maintain.md).

En utvecklarlicens för AEM kan fås via [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).

Vanliga integreringsmönster
---------------------------

AEM är en banbrytande lösning för hantering av webbupplevelser och erbjuder många potentiella integrationsområden. Vanliga integreringsmönster:

* Hämta data från ett externt system till AEM. Du kan till exempel exportera kontaktinformation från ett CRM-system så att den blir tillgänglig för en större publik på en AEM webbplats.  Implementeringar ska använda Sling&#39;s [Schemalagda jobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs), vilket garanterar att jobbet utförs även om behållarna går ner. Koden bör utformas så att den antar att jobbet kan utlösas mer än en gång.
* Exportera data från AEM till ett externt system. Exempel: prenumerationsinställningar för nyhetsbrev som skickas till en CRM på en webbplats som drivs AEM.
* Hämtar resurser från AEM. Ett externt CMS-system (Content Management System) som refererar till en resurs som lagras i AEM Assets. Eller som ett annat exempel, ett PIM-system som länkar till en bild i AEM Assets.
* Lagra resurser i den AEM infrastrukturen. Ett system för hantering av marknadsföringsresurser (MRM) som lagrar en godkänd resurs i AEM Assets.
* Konfigurera och återge en anpassad UI-komponent. Tillåt till exempel en författare att dra och släppa en videokomponent och konfigurera en viss video som ska spelas upp på den publicerade webbplatsen.
* Arbeta med en resurs med en partnertjänst. Du kan till exempel skicka en resurs till en videoplattform när en sida publiceras.
* Analyserar en webbplats, sida eller resurs i AEM Admin Console. Du kan till exempel göra SEO-rekommendationer för en befintlig eller opublicerad sida.
* Åtkomst på sidnivå till användardata som hanteras av en extern tjänst. Använd till exempel demografisk information för att anpassa webbplatsupplevelsen. Läs om ContextHub, ett ramverk för lagring, manipulering och presentation av kontextdata.
* Översätter webbplatskopia eller metadata för resurser. Se [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) för exempelkod med AEM Translation Framework, vilket är den rekommenderade implementeringen av översättningskopplingar.


Användbar dokumentation
--------------------

Experience Manager as a Cloud Service [dokumentation](../overview/introduction.md) ger värdefulla insikter i utvecklingen av AEM. Nedan finns några specifika tekniska ämnen och referenser som du kan finna användbara när du implementerar en AEM-anslutning:

* Adobe konsulttjänster (ACS) [AEM](https://adobe-consulting-services.github.io/acs-aem-samples/) för kommenterad kod som hjälper AEM att utbilda utvecklare
* De olika dokumentationslänkarna i avsnittet Vanliga integreringsmönster i den här artikeln

Community-resurser
--------------------

Förutom den statiska dokumentationen ovan erbjuder Adobe och AEM resurser för att få ut en kontakt på marknaden:

* The Adobe Community&#39;s [AEM](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) är en aktiv webbplats där dina kollegor ställer och svarar på frågor
* Ytterligare tekniska resurser för Adobe finns tillgängliga på vissa partnernivåer. Läs mer om [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Om er organisation vill ha hjälp med implementeringen kan ni överväga Adobes [Professional Services](https://www.adobe.com/marketing-cloud/service-support/professional-consulting-training.html)-team eller visa en lista över Adobes partners över hela världen i [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html)

Strukturregler för paket
-----------------------

För att stödja rullande driftsättningar har AEM as a Cloud Service paket, av vilka kopplingar är exempel, en strikt separation mellan&quot;oföränderligt&quot; och&quot;muterbart&quot; innehåll. Paketen ska separeras på ett tydligt sätt mellan dem som innehåller:

* `/apps`
* `/content` och `/conf`

Kopplingarna ska följa dessa riktlinjer för förpackningen, som beskrivs i [den här artikeln](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Befintliga kopplingar bör även omfaktoriseras för att anpassas.

Dessutom bör bara Adobe skriva kod i `/libs`, med kunder och partners som skriver till `/apps`.

Befintliga anslutningar kan också behöva omarbetas för att kunna flytta en konfiguration som tidigare har monterats `/etc` till andra mappar på den översta nivån som `/conf`. Denna omstrukturering gjordes som en del av AEM 6.5 och beskrivs i [AEM 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

Vi rekommenderar att större delen av kopplingskoden placeras under `/apps/connectors/<vendor>` för att främja en ren databasstruktur för kunder som har flera kontakter.

Konfigurationer av Cloud Service
-----------------------------

En aspekt av anslutningsimplementeringen är att koden som stöder konfigurationen av kopplingen är. Den här koden gör att ett kort med kopplingens namn visas under Verktyg > Åtgärder > Cloud Service. Vid klickning visas en [konfigurationsläsare](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) öppnas där kunden väljer den överordnade mappen som ska innehålla kopplingskonfigurationen. Kopplingskoden ska resultera i ett formulär med alla egenskaper som måste konfigureras, och slutligen lagra värdena i en konfigurationsmapp under `/conf`. Den här mappen kan senare väljas på fliken Webbplatsegenskaper eller på fliken Resursegenskaper.


Kontextmedvetna konfigurationer
-----------------------------

[Kontextmedvetna konfigurationer](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) gör det möjligt att skapa lager i olika mappar, inklusive `/libs`, `/apps`, `/conf` och undermappar under `/conf`. Det har stöd för arv så att kunden kan konfigurera den globala konfigurationen samtidigt som specifika ändringar görs för varje mikroplats. Eftersom den här funktionen kan användas för konfigurationer av Cloud Service bör kopplingskoden referera till konfigurationen med hjälp av det kontextmedvetna konfigurations-API:t i stället för att referera till en specifik konfigurationsnod.

Om ändrade konfigurationer används i Connector ska du skapa Connector som hanterar/sammanfogar eventuella framtida uppdateringar av standardkonfigurationer som tillhandahålls av Connector med eventuella kundkonfigurationer. Kom ihåg att om du ändrar anpassat (som det ändrats av kunden) innehåll eller konfiguration utan kundvarning och samtycke kan det hända att det inte fungerar (eller att det inte fungerar som det ska) med Connector-funktionen.

Metodtips för kodning
----------------------

Eftersom AEM as a Cloud Service är en molnbaserad lösning finns det vissa riktlinjer som kan påverka en anslutares kodstrategier. Se [AEM riktlinjer för as a Cloud Service utveckling](/help/implementing/developing/introduction/development-guidelines.md) för mer information.

Testa AEM Connector
-------------------------

Nya kopplingar ska skapas (eller befintliga kopplingar ändras) med hjälp av lokala miljöutvecklingstekniker. Partnerteamet kommer att förse ISV-partners med en sandlådemiljö där de kan distribuera sin AEM Connector till ett vaniljprogram för att säkerställa att den fungerar.

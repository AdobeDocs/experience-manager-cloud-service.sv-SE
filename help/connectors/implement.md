---
title: Implementera en AEM-anslutning
description: Implementera en AEM-anslutning
translation-type: tm+mt
source-git-commit: b77113ccc55f2063c684d49e2babdd7563b9d6fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


Implementera en AEM-anslutning
=============================

Nedan finns användbara referenser för att bygga [AEM-kopplingar](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) och de bör läsas tillsammans med riktlinjerna för hur kopplingar [skickas in](submit.md) och [underhålls](maintain.md).

Observera att en utvecklarlicens för AEM kan hämtas via [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).

Vanliga integreringsmönster
---------------------------

AEM är en banbrytande lösning för hantering av webbupplevelser och erbjuder många potentiella integrationsområden. Vanliga integreringsmönster:

* Hämta data från ett externt system till AEM. Du kan till exempel exportera kontaktinformation från ett CRM-system så att den blir tillgänglig för en större publik på en AEM webbplats.  Vid implementeringar ska Sling-jobb [schemalagda jobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs) användas, vilket garanterar att jobbet körs även om behållarna går ner. Koden bör utformas så att den antar att jobbet kan utlösas mer än en gång.
* Exportera data från AEM till ett externt system. Exempel: prenumerationsinställningar för nyhetsbrev som skickas till en CRM på en webbplats som drivs AEM.
* Hämtar resurser från AEM. Ett externt CMS-system (Content Management System) som refererar till en resurs som lagras i AEM Assets. Eller som ett annat exempel, ett PIM-system som länkar till en bild i AEM Assets.
* Lagra resurser i den AEM infrastrukturen. Ett system för hantering av marknadsföringsresurser (MRM) som lagrar en godkänd resurs i AEM Assets.
* Konfigurera och återge en anpassad UI-komponent. Tillåt till exempel en författare att dra och släppa en videokomponent och konfigurera en viss video som ska spelas upp på den publicerade webbplatsen.
* Arbeta med en resurs med en partnertjänst. Du kan till exempel skicka en resurs till en videoplattform när en sida publiceras.
* Analyserar en webbplats, sida eller resurs i AEM Admin Console. Du kan till exempel göra SEO-rekommendationer för en befintlig eller opublicerad sida.
* Åtkomst på sidnivå till användardata som hanteras av en extern tjänst. Använd till exempel demografisk information för att anpassa webbplatsupplevelsen. Läs om ContextHub, ett ramverk för lagring, manipulering och presentation av kontextdata.
* Översätter webbplatskopia eller metadata för resurser. Se [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) för exempelkod med hjälp av AEM Translation Framework, som är den rekommenderade implementeringen av översättningsanslutningar.


Användbar dokumentation
--------------------

Experience Manager som Cloud Service [dokumentation](../overview/introduction.md) ger värdefulla insikter i utvecklingen av AEM. Nedan finns några specifika tekniska ämnen och referenser som du kan använda när du implementerar en AEM-anslutning:

* Adobe Consulting Services (ACS) [AEM Samples](http://adobe-consulting-services.github.io/acs-aem-samples/) för kommenterad kod som hjälper AEM att utbilda utvecklare
* De olika dokumentationslänkarna i avsnittet Vanliga integreringsmönster i den här artikeln

Community-resurser
--------------------

Förutom den statiska dokumentationen ovan erbjuder Adobe och AEM resurser för att få ut en kontakt på marknaden:

* Adobe Community&#39;s [AEM Forum](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) är en aktiv webbplats där dina kollegor ställer och svarar på frågor
* Ytterligare tekniska resurser för Adobe finns tillgängliga på vissa partnernivåer. Läs mer om [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Om er organisation vill ha hjälp med implementeringen kan ni överväga Adobes [Professional Services](http://www.adobe.com/se/marketing-cloud/service-support/professional-consulting-training.html)-team eller visa en lista över Adobes partners över hela världen i [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html)

Strukturregler för paket
-----------------------

För att stödja rullande driftsättningar har AEM som ett Cloud Service-paket, av vilket kopplingar är exempel, en strikt separation mellan&quot;oföränderligt&quot; och&quot;muterbart&quot; innehåll. Paketen ska separeras på ett tydligt sätt mellan dem som innehåller:

* `/apps`
* `/content` and `/conf`

Kopplingar bör följa dessa paketeringsriktlinjer, som beskrivs i [den här artikeln](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Befintliga kopplingar bör även omfaktoriseras för att anpassas.

Dessutom bör endast Adobe skriva kod i `/libs`, där kunder och partners skriver till `/apps`.

Befintliga anslutningar kan också behöva omarbetas för att flytta en konfiguration som en gång har placerats `/etc` till andra mappar på den översta nivån, till exempel `/conf`. Denna omstrukturering gjordes som en del av AEM 6.5 och beskrivs i [AEM 6.5-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

Vi rekommenderar att större delen av kopplingskoden placeras under `/apps/connectors/<vendor>` för att främja en ren databasstruktur för kunder som har flera kopplingar.

Konfigurationer av Cloud Services
-----------------------------

En aspekt av anslutningsimplementeringen är att koden som stöder konfigurationen av kopplingen är. Den här koden gör att ett kort med kopplingens namn visas under Verktyg > Åtgärder > Cloud Services. När du klickar på det här alternativet visas en [konfigurationsläsare](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) där kunden väljer den överordnade mappen som ska innehålla kopplingskonfigurationen. Kopplingskoden ska resultera i ett formulär med alla egenskaper som måste konfigureras, och slutligen lagra värdena i en konfigurationsmapp under `/conf`. Den här mappen kan senare väljas på fliken Webbplatsegenskaper eller på fliken Resursegenskaper.


Kontextmedvetna konfigurationer
-----------------------------

[Kontextmedvetna ](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) konfigurationergör att du kan skikta konfigurationen i olika mappar, inklusive  `/libs`,  `/apps`och undermappar under  `/conf`   `/conf`. Det stöder arv så att kunden kan konfigurera den globala konfigurationen samtidigt som specifika ändringar görs för varje mikroplats. Eftersom den här funktionen kan användas för konfigurationer av Cloud Services bör kopplingskoden referera till konfigurationen med hjälp av det kontextmedvetna konfigurations-API:t i stället för att referera till en specifik konfigurationsnod.

Om ändrade konfigurationer används i Connector ska du skapa Connector för att hantera eventuella framtida uppdateringar av standardkonfigurationer som tillhandahålls av Connector med eventuella kundkonfigurationer. Kom ihåg att om du ändrar anpassat (som det ändrats av kunden) innehåll eller konfiguration utan kundvarning och samtycke kan det hända att det inte fungerar (eller att det inte fungerar som det ska) med Connector-funktionen.

Metodtips för kodning
----------------------

Eftersom AEM som Cloud Service är en molnbaserad lösning finns det vissa riktlinjer som kan påverka en anslutares kodstrategier. Mer information finns i [AEM som riktlinjer för Cloud Service](/help/implementing/developing/introduction/development-guidelines.md).

Testa AEM Connector
-------------------------

Nya kopplingar ska skapas (eller befintliga kopplingar ändras) med hjälp av lokala miljöutvecklingstekniker. Partnerteamet kommer att förse ISV-partners med en sandlådemiljö där de kan distribuera sin AEM Connector till ett vaniljprogram för att säkerställa att den fungerar.

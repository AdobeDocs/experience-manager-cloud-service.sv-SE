---
title: Implementera en AEM-anslutning
description: Implementera en AEM-anslutning
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 7%

---


Implementera en AEM-anslutning
=============================

Nedan finns användbara referenser för att bygga [AEM-kopplingar](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) och de bör läsas tillsammans med riktlinjerna för hur kopplingar [skickas in](submit.md) och [underhålls](maintain.md).

Observera att en utvecklarlicens för AEM kan hämtas via [Adobe Exchange Program](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html).

Vanliga integreringsmönster
---------------------------

AEM är en ledande lösning för hantering av webbupplevelser och erbjuder många potentiella integrationsområden. Vanliga integreringsmönster:

* Hämta data från ett externt system till AEM. Du kan till exempel exportera kontaktinformation från en CRM så att den blir tillgänglig för en större publik på en AEM-driven webbplats.  Vid implementeringar ska Slings [schemalagda jobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)användas, vilket garanterar att jobbet körs även om behållarna går ner. Koden bör utformas så att den antar att jobbet kan utlösas mer än en gång.
* Exportera data från AEM till ett externt system. Exempel: prenumerationsinställningar för nyhetsbrev som skickas till en CRM på en AEM-baserad webbplats.
* Hämtar resurser från AEM. Ett externt CMS-system (Content Management System) som refererar till en resurs som lagras i AEM Assets. Eller som ett annat exempel, ett PIM-system som länkar till en bild i AEM Assets.
* Lagra resurser i AEM-infrastrukturen. Ett system för hantering av marknadsföringsresurser (MRM) som lagrar en godkänd resurs i AEM Assets.
* Konfigurera och återge en anpassad UI-komponent. Tillåt till exempel en författare att dra och släppa en videokomponent och konfigurera en viss video som ska spelas upp på den publicerade webbplatsen.
* Arbeta med en resurs med en partnertjänst. Du kan till exempel skicka en resurs till en videoplattform när en sida publiceras.
* Analyserar en webbplats, sida eller resurs i AEM Admin Console. Du kan till exempel göra SEO-rekommendationer för en befintlig eller opublicerad sida.
* Åtkomst på sidnivå till användardata som hanteras av en extern tjänst. Använd till exempel demografisk information för att anpassa webbplatsupplevelsen. Läs om ContextHub, ett ramverk för lagring, manipulering och presentation av kontextdata.
* Översätter webbplatskopia eller metadata för resurser. Se [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) för exempelkod med hjälp av AEM Translation Framework, som är den rekommenderade implementeringen av översättningsanslutningar.


Användbar dokumentation
--------------------

Experience Manager som [dokumentation](../overview/introduction.md) för molntjänster ger värdefulla insikter om hur man utvecklar i AEM. Nedan följer några specifika tekniska ämnen och referenser som du kan finna användbara när du implementerar en AEM-anslutning:

* Adobe Consulting Services (ACS) [AEM Samples](http://adobe-consulting-services.github.io/acs-aem-samples/) för kommenterad kod som hjälper AEM-utvecklare att utbilda sig
* De olika dokumentationslänkarna i avsnittet Vanliga integreringsmönster i den här artikeln

Community-resurser
--------------------

Förutom den statiska dokumentationen ovan erbjuder Adobe och AEM-communityn resurser för att få kontakt på marknaden:

* Adobe Community&#39;s [AEM Forum](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) är en aktiv webbplats där dina kollegor ställer och svarar på frågor
* Ytterligare tekniska resurser från Adobe finns på vissa partnernivåer. Läs mer om [Adobe Exchange-programmet](https://marketing.adobe.com/resources/content/resources/exchange-partner-program.html).
* Om er organisation vill ha hjälp med implementeringen kan ni överväga Adobes [Professional Services](http://www.adobe.com/se/marketing-cloud/service-support/professional-consulting-training.html)-team eller visa en lista över Adobes partners över hela världen i [Solution Partner Finder](https://solutionpartners.adobe.com/home/partnerFinder.html)

Strukturregler för paket
-----------------------

För att stödja rullande distributioner har AEM som ett molntjänstpaket, där anslutningar är exempel, en strikt separation mellan&quot;oföränderligt&quot; och&quot;muterbart&quot; innehåll. Paketen ska separeras på ett tydligt sätt mellan dem som innehåller:

* `/apps`
* `/content` and `/conf`

Kopplingarna bör följa dessa riktlinjer för förpackningar, som beskrivs i [den här artikeln](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Befintliga kopplingar bör även omfaktoriseras för att anpassas.

Dessutom bör bara Adobe skriva kod i `/libs`och skriva till kunder och partners `/apps`.

Befintliga anslutningar kan också behöva omarbetas för att kunna flytta en konfiguration som tidigare har placerats `/etc` i andra mappar på den översta nivån, till exempel `/conf`. Detta beskrivs i [AEM-dokumentationen](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html).

Vi rekommenderar att större delen av kopplingskoden placeras under `/apps/connectors/<vendor>` för att marknadsföra en ren databasstruktur för kunder som har flera kopplingar.

Konfigurationer av molntjänster
-----------------------------

En aspekt av anslutningsimplementeringen är att koden som stöder konfigurationen av kopplingen är. Den här koden gör att ett kort med anslutningsprogrammets namn visas under Verktyg > Åtgärder > Molntjänster. När användaren klickar på det öppnas en konfigurationsläsare där kunden väljer den överordnade mappen som ska innehålla kopplingskonfigurationen. Kopplingens kod ska resultera i ett formulär med alla egenskaper som måste konfigureras, vilket i slutänden lagrar värdena i en konfigurationsmapp under `/conf`. Den här mappen kan senare väljas på fliken Webbplatsegenskaper eller på fliken Resursegenskaper.


Kontextmedvetna konfigurationer
-----------------------------

[Med Context-Aware Configurations](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) kan du lagerkonfigurera olika mappar, inklusive `/libs`, `/apps``/conf` och undermappar under `/conf`. Det stöder arv så att kunden kan konfigurera den globala konfigurationen samtidigt som specifika ändringar görs för varje mikroplats. Eftersom det är möjligt att utnyttja den här funktionen för molntjänstkonfigurationer bör kopplingskoden referera till konfigurationen med hjälp av det kontextmedvetna konfigurations-API:t i stället för att referera till en specifik konfigurationsnod.

Om ändrade konfigurationer används i Connector ska du skapa Connector som hanterar/sammanfogar eventuella framtida uppdateringar av standardkonfigurationer som tillhandahålls av Connector med eventuella kundkonfigurationer. Kom ihåg att om du ändrar anpassat (som det ändrats av kunden) innehåll eller konfiguration utan kundvarning och samtycke kan det hända att det inte fungerar (eller att det inte fungerar som det ska) med Connector-funktionen.

Metodtips för kodning
----------------------

Eftersom AEM som en molntjänst är en molnbaserad lösning finns det vissa riktlinjer som kan påverka en anslutares kodstrategier. Mer information finns i [AEM som riktlinjer](/help/implementing/developing/introduction/development-guidelines.md) för molntjänstutveckling.

Testa AEM Connector
-------------------------

Nya kopplingar ska skapas (eller befintliga kopplingar ändras) med hjälp av lokala miljöutvecklingstekniker. Partnerteamet kommer att förse ISV-partners med en sandlådemiljö där de kan driftsätta sin AEM Connector till en vaniljapplikation för att se till att den fungerar.

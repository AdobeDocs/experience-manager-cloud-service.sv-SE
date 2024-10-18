---
title: Implementera en AEM Connector
description: Lär dig mer om kopplingar, vad de kan göra och hur du implementerar dessa värdefulla verktyg i Experience Manager.
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
feature: Operations
role: Admin
source-git-commit: a9cec66cf518a19a5a6152d431a052369b5b503a
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 4%

---


Implementera en AEM Connector
=============================

Nedan anges användbara referenser för att skapa AEM Connectors och de bör läsas med vägledning om [sändning](submit.md) och [underhåll](maintain.md) anslutningar.

En utvecklarlicens för AEM kan hämtas via [Adobe Exchange-programmet](https://partners.adobe.com/technologyprogram/experiencecloud.html).

Vanliga integreringsmönster
---------------------------

AEM är en banbrytande lösning för hantering av webbupplevelser och erbjuder många potentiella integrationsområden. Vanliga integreringsmönster:

* Hämta data från ett externt system till AEM. Du kan till exempel exportera kontaktinformation från ett CRM-system så att den blir tillgänglig för en större publik på en AEM webbplats.  Implementeringar ska använda Sling:s [schemalagda jobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs), vilket garanterar att jobbet körs även om behållarna går ner. Koden bör utformas så att den antar att jobbet kan utlösas mer än en gång.
* Exportera data från AEM till ett externt system. Exempelvis skickas prenumerationsinställningar för nyhetsbrev till en CRM på en AEM webbplats.
* Hämtar resurser från AEM. Ett externt innehållshanteringssystem (CMS) som refererar till en resurs som lagras i AEM Assets. Eller som ett annat exempel, ett PIM-system som länkar till en bild i AEM Assets.
* Lagra resurser i den AEM infrastrukturen. Ett system för hantering av marknadsföringsresurser (MRM) som lagrar en godkänd resurs i AEM Assets.
* Konfigurera och återge en anpassad UI-komponent. Tillåt till exempel en författare att dra och släppa en videokomponent och konfigurera en viss video som ska spelas upp på den publicerade webbplatsen.
* Arbeta med en resurs med en partnertjänst. Du kan till exempel skicka en resurs till en videoplattform när en sida publiceras.
* Analyserar en webbplats, sida eller resurs i AEM Admin Console. Du kan till exempel göra SEO-rekommendationer för en befintlig eller opublicerad sida.
* Åtkomst på sidnivå till användardata som hanteras av en extern tjänst. Använd till exempel demografisk information för att anpassa webbplatsupplevelsen. Läs om ContextHub, ett ramverk för lagring, manipulering och presentation av kontextdata.
* Översätter webbplatskopia eller metadata för resurser. Se [AEM Translation Framework Bootstrap Connector](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) för exempelkod med AEM Translation Framework, som är den rekommenderade implementeringen av översättningsanslutningar.


Användbar dokumentation
--------------------

Experience Manager as a Cloud Service [documentation](../overview/introduction.md) ger värdefulla insikter om hur du utvecklar i AEM. Nedan finns några specifika tekniska ämnen och referenser som du kan finna användbara när du implementerar en AEM-anslutning:

* Adobe Consulting Services (ACS) [AEM Samples](https://adobe-consulting-services.github.io/acs-aem-samples/) för kommenterad kod som hjälper AEM utvecklare att utbilda
* De olika dokumentationslänkarna i avsnittet Vanliga integreringsmönster i den här artikeln

Community-resurser
--------------------

Förutom den statiska dokumentationen ovan erbjuder Adobe och AEM resurser för att få ut en kontakt på marknaden:

* Adobe-communityns [AEM forum](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) är en aktiv webbplats där dina kollegor ställer och svarar på frågor
* Ytterligare tekniska resurser för Adobe finns tillgängliga på vissa partnernivåer. Läs mer om programmet [Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).
* Om er organisation vill ha hjälp med implementeringen kan ni överväga Adobes [Professional Services](https://solutionpartners.adobe.com/s/directory)-team eller visa en lista över Adobes partners över hela världen i [Solution Partner Finder](https://solutionpartners.adobe.com/s/directory/)

Strukturregler för paket
-----------------------

För att underlätta rullande installationer bibehåller AEM as a Cloud Service-paket, som till exempel kopplingar, en strikt uppdelning mellan&quot;oföränderligt&quot; och&quot;ändringsbart&quot; innehåll. Paketen bör vara tydligt organiserade och innehålla följande:

* `/apps`
* `/content` och `/conf`

Kopplingar bör följa de här riktlinjerna för paketering, som beskrivs under [AEM Projektstruktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Befintliga kopplingar bör även omfaktoriseras för att anpassas.

Dessutom bör bara Adobe skriva kod till `/libs`, där kunder och partners skriver till `/apps`.

Befintliga anslutningar kan också behöva omarbetas för att flytta en konfiguration som en gång har placerats `/etc` till andra mappar på den översta nivån, till exempel `/conf`. Omstruktureringen gjordes som en del av AEM 6.5 och beskrivs i [AEM 6.5-dokumentationen](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/repository-restructuring).

Adobe rekommenderar att du placerar större delen av kopplingskoden under `/apps/connectors/<vendor>` för att behålla en ren databasstruktur, särskilt för kunder som använder flera anslutningar.

Konfigurationer av Cloud Service
-----------------------------

En aspekt av anslutningsimplementeringen är koden som stöder konfigurationen av kopplingen. Den här koden gör att ett kort med kopplingens namn visas under Verktyg > Åtgärder > Cloud Service. När användaren klickar på det visas en [konfigurationsläsare](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) där kunden väljer den överordnade mappen som ska innehålla kopplingskonfigurationen. Kopplingskoden ska resultera i ett formulär med alla egenskaper som måste konfigureras, och slutligen lagra värdena i en konfigurationsmapp under `/conf`. Den här mappen kan senare väljas på egenskapsfliken Platser eller på egenskapsfliken för Assets.


Kontextmedvetna konfigurationer
-----------------------------

Med [Kontextmedvetna konfigurationer](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) kan du skikta konfigurationen mellan olika mappar, inklusive `/libs`, `/apps`, `/conf` och undermappar under `/conf`. Det har stöd för arv så att kunden kan konfigurera den globala konfigurationen samtidigt som specifika ändringar görs för varje mikroplats. Eftersom den här funktionen kan användas för konfigurationer av Cloud Service bör kopplingskoden referera till konfigurationen med hjälp av det kontextmedvetna konfigurations-API:t i stället för att referera till en specifik konfigurationsnod.

Om ändrade konfigurationer används i Connector ska du skapa Connector som hanterar/sammanfogar eventuella framtida uppdateringar av standardkonfigurationer som tillhandahålls av Connector med eventuella kundkonfigurationer. Tänk på att ändringar av kundanpassat innehåll eller konfigurationer utan föregående meddelande och samtycke kan störa eller orsaka oväntade beteenden i Connector.

Metodtips för kodning
----------------------

Eftersom AEM as a Cloud Service är en molnbaserad lösning finns det vissa riktlinjer som kan påverka en anslutares kodstrategier. Mer information finns i [AEM as a Cloud Service utvecklingsriktlinjer](/help/implementing/developing/introduction/development-guidelines.md).

Testa AEM Connector
-------------------------

Nya kopplingar ska skapas (eller befintliga kopplingar ändras) med hjälp av lokala miljöutvecklingstekniker. Partnerteamet förser ISV-partners med en sandlådemiljö där de kan driftsätta sin AEM Connector till ett vaniljprogram för att säkerställa att den fungerar.

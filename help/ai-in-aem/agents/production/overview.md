---
title: Översikt över Experience Production Agent
description: Läs om hur Experience Production Agent i AEM hjälper er att skapa innehåll snabbare och automatiskt hantera ändringar.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Översikt över Experience Production Agent {#experience-production-agent}

Experience Production Agent automatiserar arbetsmoment med hög arbetsinsats och stora volymer. Ge teamen möjlighet och omvandla manuella, veckovisa processer till snabba, AI-assisterade arbetsflöden som håller alla upplevelser aktuella och enhetliga och hjälper företaget att uppnå sina mål.

## Jobb {#jobs}

Agenten tillhandahåller följande jobb:

* [Innehållsuppdatering](#content-update)
* [Skapa formulär](#form-creation)
* [Kommunikationsskapande](#communications-creation)
* [Platsmigrering](#site-migration)

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

### Innehållsuppdatering {#content-update}

[Innehållsuppdateringen](/help/ai-in-aem/agents/production/content-update.md) uppdaterar enkelt befintligt innehåll i hela CMS - inklusive innehållsfragment, sidor, formulär och resurser -. Agenten kan utföra åtgärder som att uppdatera, ta bort, ersätta eller lägga till innehållselement för att hålla upplevelsen korrekt och aktuell. Inmatningar kan vara naturliga språkbeskrivningar, och när de används med Jira PDF-filer och skärmbilder kan de också ge inmatning.

### Skapa formulär {#form-creation}

Med kompetensen [Skapa formulär](/help/ai-in-aem/agents/production/form-creation.md) kan användare skapa anpassningsbara formulär med hjälp av naturliga språkinställningar utan att vara beroende av utvecklings- eller IT-team. Denna funktion snabbar upp formulärutvecklingen samtidigt som varumärkets enhetlighet bibehålls och gör det möjligt för företagsanvändare att skapa formulär utan djupgående tekniska produktkunskaper.

### Kommunikationsskapande {#communications-creation}

Med kompetensen [Kommunikationsskapande](/help/ai-in-aem/agents/production/communications-creation.md) kan företagsanvändare skapa personaliserad, datadriven korrespondens i stor skala. Från kontoutdrag och policydokument till räkningar och välkomstpaket - agenten omvandlar de naturliga språkkraven till professionell kommunikation.

>[!NOTE]
>
> Kommunikationsskapandet är för närvarande alfavärdet. Om du vill delta skickar du en förfrågan från din officiella e-postadress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com).

### Platsmigrering {#site-migration}

[Platsmigrering](/help/ai-in-aem/agents/production/site-migration.md) migrerar sömlöst icke-AEM-webbplatser till AEM-miljöer (Experience Delivery Services), vilket garanterar att de är presterande, kompatibla och agentklara. Agenten effektiviserar konfigurationen och omvandlingen, vilket minskar den manuella ansträngningen och tiden till värde.

Medarbetaren bör kunna arbeta med andra agentfärdigheter, till exempel:

## Användning tillsammans med andra läkemedel {#use-with-other-agents}

* Hämta källmaterial från Experience Advisory Agent

## Aktivering {#activation}

Om du vill aktivera och få tillgång till Experience Production Agent måste du kontakta Adobe. Du kan kontakta:

* `experience-production-agent@adobe.com`
* eller kontakta ditt kontoteam

Om du vill snabba upp processen kan du få följande information:

* För AEM as a Cloud Service
   * Du måste ange:
      * Organisations-ID
      * `product_id`
      * `profile_id`

   * Dessa värden hittades med följande steg:
      * Din administratör måste besöka <https://adminconsole.adobe.com/>
      * Välj **Adobe Experience Manager as a Cloud Service**
      * Välj lämplig AEM-instans
      * Välj den profil som tillåter läs- och skrivåtgärder för innehållet i fråga
      * Hämta webbläsarens URL
      * Extrahera `product_id` och `profile_id` från URL:en.
Exempel: <https://adminconsole.adobe.com/products/profiles/users>

* Edge Delivery Document Authoring
   * Ge ditt Adobe-team följande information:
      * Relevanta domäner
      * Relevant Github-information:
         * Org
         * Repo
         * Gren

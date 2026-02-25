---
title: Innehållsuppdateringsjobb
description: Lär dig vad uppdateringsjobbet för varumärkesupplevelseagenten är och vad det kan göra för dig.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 0%

---


# Innehållsuppdateringsjobb {#content-update}

Innehållsuppdateringsjobbet för [varumärkesagenten](/help/ai-in-aem/agents/brand-experience/overview.md) automatiserar innehållsproduktionen för att snabba upp rutinuppgifterna för Adobe Experience Manager (AEM) as a Cloud Service och Edge Delivery Services.

## Ökning {#overview}

Innehållsuppdateringsjobbet uppdaterar befintligt innehåll, inklusive innehållsfragment, sidor, formulär och resurser. Jobbet kan utföra åtgärder som att uppdatera, ta bort, ersätta eller lägga till innehållselement för att hålla upplevelsen korrekt och aktuell. Inmatningar kan vara naturliga språkbeskrivningar, och när de används med Jira PDF-filer och skärmbilder kan de också ge inmatning.

Innehållsuppdateringsjobbet omvandlar den information du anger, antingen på det naturliga språket eller visuellt, till innehållsuppdateringar på sidan. Du anger URL-adressen till en sida som behöver uppdateras, tillsammans med information om vad som behöver uppdateras, och agentens kompetens slutför uppgiften.

## Funktioner {#capabilities}

Du kan få åtkomst till innehållsuppdateringskunskaperna från:

* [AI-assistenten](#ai-assistant)
* [Jira](#jira)

## AI-assistenten {#ai-assistant}

Du kommer åt jobbet i AEM via AI-assistenten.

Öppna AI-assistenten från [`experience.adobe.com`,](https://experience.adobe.com) och börja sedan interagera genom att ange din uppmaning på ett naturligt språk i fältet `Ask AI Assistant anything`:

![Innehållsuppdateringsjobb](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Exempelfrågor {#sample-prompts}

För att starta innehållsuppdateringar kan du ge dig ett brett urval av naturliga språk. Du måste också ange den offentliga URL:en för sidan som du vill uppdatera. Till exempel:

* Ändra följande sida `https://www.your-url.com/sale` Uppdatera huvudhjälterubriken till&quot;Black Friday Mega Sale - upp till 70 % rabatt&quot;, ändra nedräkningstimern till&quot;Ends in 48 Hours&quot;, Ta bort&quot;Sign up for updates&quot;, Ändra alla&quot;Shop Now&quot;-knappar till&quot;Get the Deal&quot;&quot;

* `https://www.your-url.com/laptops/your-laptop-model` Uppdatera banderollkopia till&quot;Spara 300 USD endast idag&quot;, uppdatera priser från 1 299 USD till 999 USD, ta bort banderoll för finansieringsalternativ

* `https://www.your-url.com/your-sneaker` Uppdatera Stock-status från Låg Stock till Tillbaka i Stock - begränsade kvantiteter, Ändra storleksväljaren så att tillgängliga storlekar markeras i grönt, ta bort ikonen Kommer snart

* `https://www.your-url.com/your-sneaker` Uppdatera produktbilderna så att nya färger visas

>[!NOTE]
>
>Filöverföringar kan användas vid interaktion med [Jira](#jira), men stöds inte med AI Assistant.

## Jira {#jira}

Genom att använda innehållsuppdateringsjobbet med Jira kan du skapa en biljett med instruktioner som automatiserar dina redigeringar.

### Skapa en biljett {#create-a-ticket}

Skapa en Jira-biljett (av valfri typ). Det krävs två viktiga uppgifter i fältet **Beskrivning** för din biljett:

1. Den offentliga URL:en för sidan som du behöver redigera.

1. Ändringarna behövs.

   Jobbet har stöd för följande format för att beskriva dina ändringar:

   * Naturligt språk i biljettbeskrivningen
      * till exempel&quot;Ändra rubriken från X till Y&quot;
   * Antecknade PDF bifogade
      * skapa t.ex. en PDF av din sida och lägga till anteckningar som anger vad du vill ändra
   * Kommentarer i bifogade PDF
      * skapa t.ex. en PDF av din sida och lägga till kommentarer som anger vad du vill ändra
   * Antecknad skärmbild bifogad
      * ta till exempel en skärmbild av en del av sidan och lägg till anteckningar som anger vad du vill ändra
   * Bifogad Microsoft Word-fil, med naturliga språkändringar

### Anropa jobbet från din biljett {#invoke-the-job-from-your-ticket}

Om du vill använda jobbet lägger du till en kommentar i din biljett. I kommentaren anger du jobbet med symbolen `@`, tillsammans med det kommando som det ska köra, till exempel:

* `@aemagent@adobe.com process`

Jobbet förstår för närvarande kommandona:

* `process` - bearbeta begäran
* `cancel` - avbryt en bearbetningsbegäran
* `retry` - bearbeta en begäran igen
* `feedback` - använd feedback på en tidigare generation
* `reprocess` - bearbeta om den ursprungliga begäran

### Hur jobbet samverkar {#how-the-agent-interacts}

När du har skickat ett kommando till jobbet svarar det med kommentarer i Jira. Kommentarerna beskriver hur jobbet fortskrider och vilka åtgärder som vidtagits.

Om ett `process`-kommando utlöser uppdateringar kan svaren följa sekvensen:

* Den inledande kommentaren bekräftar att jobbet har startats.

* När uppgiften är slutförd svarar jobbet med en annan kommentar som innehåller information om de åtgärder som har vidtagits.
   * De innehållsuppdateringar som jobbet gör är icke-förstörande, vilket innebär att de görs till en förhandsvisningsinstans.
   * Kommentaren innehåller länkar till uppdateringarna, så att du kan granska och publicera efter behov, eller tilldela Jira till den som ska vara ansvarig.

* Följande bild visar ett exempel på Jira som utlöser kommandot `process` för innehållsuppdateringsjobbet:

  ![Exempel-Jira som använder innehållsuppdateringsjobbet för Experience Production Agent](assets/content-update-jira-example.png)

## Aktivering {#activation}

Om du vill aktivera och få tillgång till kommunikationsjobbet måste du kontakta Adobe. Du kan antingen:

* Kontakt `experience-production-agent@adobe.com`
* Eller kontakta ditt kontoteam

Om du vill snabba upp processen kan du få följande information:

* För AEM as a Cloud Service måste du ange:
   * Organisations-ID
   * `product_id`
   * `profile_id`

   * Dessa värden finns i följande steg:
      1. Din administratör måste besöka [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)
      1. Välj **Adobe Experience Manager as a Cloud Service**
      1. Välj lämplig AEM-instans
      1. Välj den profil som tillåter läs- och skrivåtgärder för innehållet i fråga
      1. Hämta webbläsarens URL
      1. Extrahera `product_id` och `profile_id` från URL:en.
Exempel: `https://adminconsole.adobe.com/products/profiles/users`

* Edge Delivery Document Authoring
   * Ge ditt Adobe-team följande information:
      * Relevanta domäner
      * Relevant Github-information:
         * Org
         * Repo
         * Gren

## Begränsningar {#limitations}

Observera följande begränsningar:

* Filöverföringar kan användas vid interaktion med [Jira](#jira), men stöds inte vid interaktion med [AI-assistenten.](#ai-assistant)

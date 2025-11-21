---
title: Innehållsuppdateringskunskap
description: Lär dig vad Experience Production Agents kompetens när det gäller innehållsuppdatering är och vad den kan göra för dig.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: d5b7a8343551c5880b40c692266f33a1864f9d2b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# Innehållsuppdateringskunskap {#content-update}

Med Experience Production Agent kan ni automatisera innehållsproduktionen och därmed snabba upp rutinuppgifterna för Adobe Experience Manager (AEM) as a Cloud Service och Edge Delivery Services.

Innehållet uppdaterar befintligt innehåll i hela CMS, inklusive innehållsfragment, sidor, formulär och resurser. Agenten kan utföra åtgärder som att uppdatera, ta bort, ersätta eller lägga till innehållselement för att hålla upplevelsen korrekt och aktuell. Inmatningar kan vara naturliga språkbeskrivningar, och när de används med Jira PDF-filer och skärmbilder kan de också ge inmatning.

## Ökning {#overview}

Kunskapen om innehållsuppdatering omvandlar den information du ger, antingen via det naturliga språket eller bilderna, till innehållsuppdateringar på sidan. Du anger URL-adressen till en sida som behöver uppdateras, tillsammans med information om vad som behöver uppdateras, och agentens kompetens slutför uppgiften.

## Funktioner {#capabilities}

Du kan få åtkomst till innehållsuppdateringskunskaperna från:

* [AI Assistant](#ai-assistant)

* [Jira](#jira)

## AI Assistant {#ai-assistant}

Du kan nå AEM Business Agents via AI Assistant.

Öppna AI Assistant från experience.adobe.com och börja sedan interagera genom att ange din uppmaning på ett naturligt språk i fältet `Ask AI Assistant anything`:

![Åtkomstidentifieringsagent](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

<!--
### Sample Prompts {#sample-prompts}

To initiate content updates you can give a wide range of natural language prompts. You also need to specify the public facing URL of the page you want to update:

* Change your headlines

  * On your-URL change the headline from X to Y
-->

>[!NOTE]
>
>Filöverföringar kan användas vid interaktion med [Jira](#jira), men stöds inte med AI Assistant.

## Jira {#jira}

Genom att använda innehållsuppdateringskunskaperna med Jira kan du skapa en biljett med instruktioner som automatiserar dina redigeringar.

### Skapa en biljett {#create-a-ticket}

Skapa en Jira-biljett (av valfri typ).

Det krävs två viktiga uppgifter i fältet **Beskrivning** för din biljett:

1. Den offentliga URL:en för sidan som du behöver redigera.

1. Ändringarna behövs.

   För närvarande har kompetensen stöd för följande format för att beskriva dina ändringar:

   * Naturligt språk i biljettbeskrivningen
      * till exempel&quot;Ändra rubriken från X till Y&quot;
   * Antecknade PDF bifogade
      * skapa t.ex. en PDF av din sida och lägga till anteckningar som anger vad du vill ändra
   * Kommentarer i bifogade PDF
      * skapa t.ex. en PDF av din sida och lägga till kommentarer som anger vad du vill ändra
   * Antecknad skärmbild bifogad
      * ta till exempel en skärmbild av en del av sidan och lägg till anteckningar som anger vad du vill ändra
   * Bifogad Microsoft Word-fil, med naturliga språkändringar

### Anropa agenten från din biljett {#invoke-the-agent-from-your-ticket}

Om du vill använda agenten lägger du till en kommentar i din biljett. I kommentaren anger du agenten med symbolen `@`, tillsammans med det kommando som den ska köra, till exempel:

* `@aemagent@adobe.com process`

För närvarande förstår agenten kommandona:

* `process` - bearbeta begäran
* `cancel` - avbryt en bearbetningsbegäran
* `retry` - bearbeta en begäran igen
* `feedback` - använd feedback på en tidigare generation
* `reprocess` - bearbeta om den ursprungliga begäran

### Hur agenten interagerar {#how-the-agent-interacts}

När du har skickat ett kommando till agenten svarar den med kommentarer i Jira. Kommentarerna beskriver agentens förlopp och vilka åtgärder som vidtagits.

Om ett `process`-kommando utlöser uppdateringar kan svaren följa sekvensen:

* Den inledande kommentaren bekräftar att agenten har startat.

* När uppgiften är slutförd. agenten svarar med en annan kommentar som innehåller information om de åtgärder som vidtagits.
   * De innehållsuppdateringar som agenten gör är icke-förstörande, vilket betyder att de görs till en förhandsvisningsinstans.
   * Kommentaren innehåller länkar till uppdateringarna, så att du kan granska och publicera efter behov, eller tilldela Jira till den som ska vara ansvarig.

* I följande bild visas ett exempel på Jira som utlöser kommandot `process` för innehållsuppdateringskunskaperna:

  ![Exempel på Jira som använder innehållsuppdateringskunskaper i Experience Production Agent](assets/content-update-jira-example.png)

### Aktivering {#activation}

Om du vill aktivera och få tillgång till Production Agent med Jira måste du skicka ett e-postmeddelande till Adobe. Du kan kontakta:

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

## Begränsningar {#limitations}

Begränsningarna för Content Updater är:

* Filöverföringar kan användas vid interaktion med [Jira](#jira), men stöds inte vid interaktion med [AI-assistenten](#ai-assistant).

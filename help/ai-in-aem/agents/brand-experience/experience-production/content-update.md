---
title: Innehållsuppdateringsjobb
description: Lär dig vad uppdateringsjobbet för varumärkesupplevelseagenten är och vad det kan göra för dig.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: baf12e49dadc7b25f5169279a52d5712380445de
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---


# Innehållsuppdateringsjobb {#content-update}

Innehållsuppdateringsjobbet för [Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md) automatiserar innehållsproduktionen för att snabba upp rutinuppgifterna för Adobe Experience Manager (AEM) as a Cloud Service och Edge Delivery Services.

## Ökning {#overview}

Innehållsuppdateringsjobbet uppdaterar befintligt innehåll, inklusive innehållsfragment, sidor, formulär och resurser. Jobbet kan utföra åtgärder som att uppdatera, ta bort, ersätta eller lägga till innehållselement för att hålla upplevelsen korrekt och aktuell. Inmatningar kan vara naturliga språkbeskrivningar, och när de används med Jira PDF-filer och skärmbilder kan de också ge inmatning.

Innehållsuppdateringsjobbet omvandlar den information du anger, antingen på det naturliga språket eller visuellt, till innehållsuppdateringar på sidan. Du anger URL-adressen till en sida som behöver uppdateras, tillsammans med information om vad som behöver uppdateras, och agentens kompetens slutför uppgiften. När det används med Adobe Experience Manager (AEM) as a Cloud Service skapas en ny [start](/help/sites-cloud/authoring/launches/overview.md) så att du kan granska uppdateringarna innan du tillämpar dem. När det används med dokumentredigering skapar jobbet en ny [version](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#).

## Funktioner {#capabilities}

Du kan få åtkomst till innehållsuppdateringskunskaperna från:

* [AI-assistenten](#ai-assistant)
* [Jira](#jira)

## AI-assistenten {#ai-assistant}

Du kommer åt jobbet i AEM via AI-assistenten.

Öppna AI-assistenten från [`experience.adobe.com`,](https://experience.adobe.com) och börja sedan interagera genom att ange din uppmaning på ett naturligt språk i fältet `Ask AI Assistant anything`:

![Innehållsuppdateringsjobb](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Konfigurera publicerings-URL {#configuring-the-publish-url}

Om du vill använda en publicerings-URL (offentlig) måste en engångskonfiguration göras:

* Förutsättningar:

   * För att kunna göra konfigurationen måste användaren ha behörighet som systemadministratör eller produktadministratör.

* Konfiguration:

   1. Anropa kompetensen för innehållsuppdatering genom att begära en innehållsuppdatering för URL:en.
   1. Assistenten vägleder dig genom konfigurationen genom att ställa ett antal frågor.
   1. När publicerings-URL:en är klar konfigureras den och kan användas.

Till exempel:

![Kompetens för innehållsuppdatering - konfigurera publicerings-URL](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### Fråga {#prompts}

För att starta innehållsuppdateringar kan du ge dig ett brett urval av naturliga språk. Du måste ange den offentliga webbadressen (publicerings-) eller webbadressen till författarmiljön för sidan som du vill uppdatera. Vissa, men inte alla, av de verb som stöds: ersätt, uppdatera, ta bort, ändra, ändra, justera, ta bort.

>[!NOTE]
>
>Filöverföringar kan användas vid interaktion med [Jira](#jira), men stöds inte med AI Assistant.

### Exempelfrågor {#sample-prompts}

Exempeluppmaningar:

* den `<your-publish-URL>` uppdateringen &quot;Det perfekta kaffet är fyra frågor bort!&quot; till &quot;Ditt kaffe, på ditt sätt!&quot;
* på `<your-author-env-URL>` ersätt bilden från &quot;holkat.png&quot; till &quot;stairhead.png&quot;
* på `<your-publish-URL>` ändra knappen &quot;Ta vår offefråga&quot; till en mer engagerande version&quot;
* den `<your-author-env-URL>` ta bort avsnittet &quot;Rewards unclaimed is a Gift missing!&quot;

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

Om du vill använda jobbet lägger du till en kommentar i din biljett. I kommentaren anger du jobbet med symbolen `@`, tillsammans med instruktionerna.

Till exempel:

* `@aemagent@adobe.com process this ticket`

### Hur jobbet samverkar {#how-the-agent-interacts}

När du har skickat ett kommando till jobbet svarar det med kommentarer i Jira. Kommentarerna beskriver hur jobbet fortskrider och vilka åtgärder som vidtagits.

Om ett `process`-kommando utlöser uppdateringar kan svaren följa sekvensen:

* Den inledande kommentaren bekräftar att jobbet har startats.

* När uppgiften är slutförd svarar jobbet med en annan kommentar som innehåller information om de åtgärder som har vidtagits.
   * De innehållsuppdateringar som jobbet gör är icke-förstörande, vilket innebär att de görs till en förhandsvisningsinstans.
   * Kommentaren innehåller länkar till uppdateringarna, så att du kan granska och publicera efter behov, eller tilldela Jira till den som ska vara ansvarig.

* Följande bild visar ett exempel på Jira som utlöser kommandot `process` för innehållsuppdateringsjobbet:

  ![Exempel-Jira som använder innehållsuppdateringsjobbet för varumärkesupplevelseagenten](assets/content-update-jira-example.png)

## Aktivering {#activation}

Du kan utforska AEM Agents via [Playground](https://www.aem.live/developer/aem-playground) eller ansluta till din CSM eller TAM för att diskutera åtkomst via din SKU.

## Begränsningar {#limitations}

Observera följande begränsningar:

* Filöverföringar kan användas vid interaktion med [Jira](#jira), men stöds inte vid interaktion med [AI-assistenten.](#ai-assistant)

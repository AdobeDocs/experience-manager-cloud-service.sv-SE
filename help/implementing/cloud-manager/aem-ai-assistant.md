---
title: AI Assistant i Adobe Experience Manager (Limited Beta)
description: Använd AI Assistant i Adobe Experience Manager för att hitta svar, felsöka och utforska webbplatser, Assets, Forms och Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 2db966405b5326d735083a66b2625d6d973ad7db
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# Om AI Assistant i Adobe Experience Manager {#aem-home}

AI Assistant i AEM (Adobe Experience Manager) har ett konversationsgränssnitt som gör det enkelt att hitta svar på frågor som rör Adobe Experience Manager. Det hjälper dig att få tillgång till produktinformation, felsöka problem och utforska information som finns i Experience League. Under det begränsade Beta-programmet stöder AI Assistant Adobe Experience Manager as a Cloud Service, bland annat Sites, Assets, Forms och Cloud Manager.

>[!IMPORTANT]
>Kontrollera att du har granskat och skickat in användaravtalet så att Adobe kan aktivera AI Assistant-funktionen så att du kan testa och delta i Beta.
>
>Om du har några frågor skickar du ett e-postmeddelande till [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

## Integritet, säkerhet och styrning

AI Assistant i AEM har utformats med stor betoning på integritet, säkerhet och styrning.

I den här artikeln beskrivs de förtroendecentrerade funktioner som du kan förvänta dig av AI-assistenten:

* Inga personuppgifter används av AI Assistant, även i utbildningssyfte.
* AI Assistant har inte åtkomst till konsumentdata.
* Explicit behörighet krävs för att interagera med AI-assistenten.
* Användarspecificerade uppmaningar (frågor, frågor och så vidare) delas inte med andra kunder.


## Lär känna AI Assistant för produktkännedom {#ai-prod-insights}

Produktkunskap omfattar begrepp och ämnen som härletts ur Adobe Experience League-dokumentationen. Dessa frågor kan kategoriseras i följande undergrupper:

| Produktkunskap | Exempel |
| --- | --- |
| Undervisning | <ul><li>Vad är den universella redigeraren?</li><li>Hur skapar jag ett program i Cloud Manager?</li></ul> |
| Öppna identifiering | <ul><li>Hur använder jag Universal Editor?</li><li>Finns det något sätt att kopiera innehåll från en miljö till en annan?</li></ul> |
| Felsökning | <ul><li>Varför har jag inte åtkomst till Universal Editor?</li><li>Varför misslyckas min pipeline?</li></ul> |

AI Assistentens nuvarande omfattning fokuserar på produktkunskapsfrågor för Adobe Experience Manager as a Cloud Service. Detta omfattar omfattande stöd för nyckelområden som Sites, Assets, Forms och Cloud Manager.

## AI Assistant för AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Förutom den allmänna AI-assistenten för produktkunskap erbjuder AEM en specialiserad **[AI-assistent för AEM Forms (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. Denna förbättrade assistent kan aktivt hjälpa dig att skapa och konfigurera formulär med hjälp av naturliga språkfrågor och svar på frågor som är specifika för formulär.

### Nyckelfunktioner

AI Assistant för AEM Forms ger:

* **Skapa formulär**: Skapa nya formulär från grunden med naturliga språkbeskrivningar
* **Designimport**: Konvertera befintliga designer (PDF, Figma, bilder) till fungerande AEM-formulär
* **Formulärkonfiguration**: Lägg till fält, paneler, verifieringsregler och villkorslogik
* **Layouthantering**: Ordna formulärstrukturen och optimera för olika enheter
* **Integrationsinställningar**: Konfigurera formulärinskick och datahantering
* **Produktkunskap**: Svara på frågor om AEM Forms funktioner och bästa praxis

### Åtkomstplats

AI Assistant för AEM Forms finns i:

* **Universell redigerare**: För Edge Delivery Services-formulär med visuella redigeringsfunktioner
* **Adaptiv Forms Editor**: För detaljerad formulärkonfiguration och avancerade funktioner
* **Forms Management UI**: För formulärskapande och hanteringsåtgärder på hög nivå

### Komma igång

>[!NOTE]
>
> AI Assistant för AEM Forms (Forms Experience Builder) är tillgänglig via programmet för tidiga användare. Skicka ett e-postmeddelande från din arbetsadress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) för att begära åtkomst.

Mer information om hur du använder AI-assistenten för AEM Forms, med detaljerade exempel och bästa praxis, finns i [AI-assistenten för AEM Forms-dokumentation](/help/edge/docs/forms/forms-ai-assistant.md).

### Exempel på användningsfall

* **&quot;Skapa ett formulär för kundfeedback med namn, e-post, betyg och kommentarfält&quot;**
* **&quot;Konvertera det här överförda PDF-programformuläret till ett digitalt anpassat formulär&quot;**
* **&quot;Lägg till villkorlig logik om du bara vill visa information om make/maka när civilstånd är gift&quot;**
* **&quot;Konfigurera det här formuläret för att skicka data till vårt CRM-system&quot;**

Denna specialiserade Forms AI Assistant utgör nästa steg i formulärskapandet och kombinerar styrkan i AI med AEM kraftfulla formulärfunktioner för att effektivisera arbetsflödet för att skapa formulär.

## Skapa effektiva frågor {#ai-craft-questions}

För att få de mest korrekta svaren från AI-assistenten är det viktigt att formulera dina frågor tydligt och i rätt sammanhang. Använd följande tips för att kontrollera att dina frågor är tydliga och välstrukturerade:

* Ange tydligt din uppgift eller fråga på ett kortfattat sätt.
* Undvik tvetydiga formuleringar eller alltför komplex syntax för att öka förståelsen.
* Inkludera relevant kontext om din uppgift eller fråga, eftersom den här metoden hjälper AI-assistenten att ge mer exakta och relevanta svar.

### Exempel på frågor som inte stöds {#ai-unsupported-questions}

| Område | Exempel |
| --- | --- |
| Driftsinsikter | <ul><li>Hur många utvecklingsmiljöer finns det i min hyresgäst?</li><li>Vem startade den senaste produktionslinjen?</li></ul> |
| Felsökning | <ul><li>Varför misslyckas min produktionsprocess?</li></ul> |
| Uppgift och automatisering | <ul><li>Konfigurera en pipeline för kodkvalitet från en utvecklingsgren åt mig.</li></ul> |


## Använd AI-assistenten {#ai-use}


### Starta eller återställa en konversation

Du kan återställa AI-assistenten och starta en ny konversation när du vill ändra ämnen. Den här funktionen är särskilt användbar vid felsökning av frågor som är felaktiga eller ger felaktig information.

![Starta konversationsknapp](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Så här startar eller återställer du en konversation:**

1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i AI-assistenten.
1. Om du vill informera AI Assistant om ett nytt ämne eller om en ändring i ett ämne klickar du på **Starta ny konversation**.

### Använd identifiering

AI Assistant innehåller en identifieringsfunktion som hjälper dig att utforska de ämnen och kategorier som stöds.

![Ideas glödlampsikon](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Så här använder du identifierbarhet:**

1. Klicka på ikonen ![Lär dig](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) i det övre högra hörnet av AI-assistenten.
1. Välj en kategori om du vill visa en lista med relaterade uppmaningar.
1. Välj ett kommando för att bättre förstå vilka typer av frågor som AI-assistenten kan besvara.

### Ge feedback på AI Assistant

Dina indata hjälper till att förbättra AI-assistenten för bättre prestanda och precision.

Dela med dig av dina synpunkter på din upplevelse med AI Assistant via följande alternativ:

![Tummen uppåt, tummen nedåt och flaggikoner](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Ikon | Beskrivning |
| --- | --- |
| ![Miniatyrbilderna är en ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Klicka för att ange vad som gick bra och för att dela positiv feedback. |
| ![Miniatyrbilder nedåt, ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Klicka för att ge förslag på förbättringar. Lägg till specifika kommentarer om din upplevelse, som granskas dagligen. |
| ![Flaggikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Klicka för att rapportera problem eller ge detaljerad feedback om din interaktion med AI-assistenten. |

## Frågor och svar om AI Assistant {#ai-faq}

Här är svar på några vanliga frågor om AI-assistenten:

* **Tillhandahåller AI-assistenten information i realtid?**\
  Nej. AI Assistant hämtar sitt innehåll från Adobe Experience League-dokumentation. Det kan ta lite tid att reflektera över uppdateringarna i svaren.
* **Vilka Adobe-program stöder AI Assistant?**\
  För närvarande har AI Assistant stöd för AEM as a Cloud Service, som Sites, Assets, Forms och Cloud Manager, särskilt för produktinformationsfrågor.
* **Vilka funktioner har AI Assistant?**\
  AI Assistant är utformat för att besvara frågor som rör Adobe produktkunskaper.
* **Använder AI Assistant personlig information för utbildningsdata?**\
  Nej. AI Assistant använder inte personuppgifter för utbildningsändamål. Undvik att dela personuppgifter om dig själv eller andra, inklusive namn eller kontaktuppgifter, med AI-assistenten.

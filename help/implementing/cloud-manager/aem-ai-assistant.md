---
title: AI Assistant i Adobe Experience Manager (Beta)
description: Använd AI Assistant för att hitta svar och felsöka de lösningar som finns i Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 577e15165057fcf6537b4b0b738a1f45e5feb097
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---

# AI Assistant i Adobe Experience Manager {#aem-home}

AEM (Adobe Experience Manager) AI Assistant har ett konversationsgränssnitt som underlättar för dig att hitta svar på dina Adobe Experience Manager-relaterade frågor. Det hjälper dig att få snabba svar på dina produktrelaterade AEM-frågor (*som är tillgängliga för alla användare*) och automatisera skapandet av supportärenden (*som är tillgängliga för supportadministratörer*).

Under den privata betaversionen stöder AEM AI Assistant AEM as a Cloud Service, inklusive följande lösningar:

* Sites
* Assets
* Dynamiska medier
* Edge Delivery Services
* Cloud Manager
* Forms

Det är direkt inbäddat i AEM och tillgängligt från AEM Experience Hub, Cloud Manager och redigeringsgränssnittet.

>[!IMPORTANT]
>Kontrollera att du har granskat och skickat in användaravtalet så att Adobe kan aktivera AI Assistant-funktionen så att du kan testa och delta i det privata betaprogrammet.
>
>Om du har några frågor skickar du ett e-postmeddelande till [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

## Omfång {#scope}

AEM AI Assistant har nu fokus på produktkunskapsfrågor för Adobe Experience Manager as a Cloud Service. Detta omfattar omfattande stöd för nyckelområden som Sites, Assets, Forms, Edge Delivery Services och Cloud Manager.

* **Ytor**: Finns i AEM Experience Hub, Author UI, Cloud Manager.
* **Funktioner**: Produktkunskap och första stopp för felsökning och vägledning, automatiskt skapande av supportärenden och sökning.
* **Värde**: sparar tid, snabbar upp inlärningen och värdesätter tid, minskar behovet av att skapa supportärenden manuellt och förbättrar effektiviteten när det gäller att skapa supportärenden.

## Integritet, säkerhet och styrning{#privacy-security-governance}

AEM AI Assistant är utformat med stor betoning på sekretess, säkerhet och styrning.

I den här artikeln beskrivs de förtroendecentrerade funktioner som du kan förvänta dig av AEM AI Assistant:

* AEM AI Assistant använder inga personuppgifter, inte ens i utbildningssyfte.
* AEM AI Assistant har inte åtkomst till konsumentdata.
* Explicit behörighet krävs för att interagera med AEM AI Assistant.
* Användarspecificerade uppmaningar (frågor, frågor och så vidare) delas inte med andra kunder.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## Lär känna AEM AI Assistant för produktkännedom och automatisk hantering av supportärenden {#ai-prod-insights}

Produktkunskap omfattar begrepp och ämnen som härletts ur Adobe Experience League-dokumentationen. Dessa frågor kan kategoriseras i följande undergrupper:


| Produktkunskap | Tillgängligt för alla användare<br>Exempel |
| :--- | :--- |
| Undervisning | <ul><li>Vad är den universella redigeraren?</li><li>Hur skapar jag ett program i Cloud Manager?</li></ul> |
| Öppna identifiering | <ul><li>Hur använder jag Universal Editor?</li><li>Finns det något sätt att kopiera innehåll från en miljö till en annan?</li></ul> |
| Felsökning | <ul><li>Varför har jag inte åtkomst till Universal Editor?</li><li>Varför misslyckas min pipeline?</li></ul> |
| **Skapa supportbiljett** | **Endast tillgängligt för supportadministratörer &#x200B;**<br>**Exempel** |
| Automatiserad framtagning av supportbiljetter som fångar AI Assistant-chatthistorik och kontext | <ul><li>Skapa en supportbiljett åt mig.</li></ul> |
| Hämta status för supportanmälan | <ul><li>Visa alla supportärenden som jag har öppnat.</li><li>Visa status för biljetten E—</li></ul> |

{style="table-layout:auto"}


## Skapa effektiva frågor {#ai-craft-questions}

För att få de mest korrekta svaren från AEM AI Assistant är det viktigt att formulera dina frågor tydligt och i rätt sammanhang. Använd följande tips för att kontrollera att dina frågor är tydliga och välstrukturerade:

* Ange tydligt din uppgift eller fråga på ett kortfattat sätt.
* Undvik tvetydiga formuleringar eller alltför komplex syntax för att öka förståelsen.
* Lägg in relevant information om arbetsuppgifterna eller frågorna, eftersom detta gör att AEM AI Assistant kan ge mer exakta och relevanta svar.
Till exempel får du hjälp med att namnge den AEM-lösning du arbetar i: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager eller Forms.

### Exempel på frågor som inte stöds {#ai-unsupported-questions}

| Område | Exempel |
| --- | --- |
| Driftsinsikter | <ul><li>Hur många utvecklingsmiljöer finns det i min hyresgäst?</li><li>Vem startade den senaste produktionslinjen?</li></ul> |
| Felsökning | <ul><li>Varför misslyckas min produktionsprocess?</li></ul> |
| Uppgift och automatisering | <ul><li>Konfigurera en pipeline för kodkvalitet från en utvecklingsgren åt mig.</li></ul> |


## Använd AEM AI Assistant {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AEM AI Assistant access through Admin Console 

To use the AEM AI Assistant, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AEM AI Assistant in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AEM AI Assistant of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Starta eller återställa en konversation

Du kan återställa AEM AI Assistant och starta en ny konversation när du vill ändra ämnen. Den här funktionen är särskilt användbar vid felsökning av frågor som är felaktiga eller ger felaktig information.

![Starta konversationsknapp](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Så här startar eller återställer du en konversation:**

1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i AEM AI Assistant.
1. Klicka på **Starta ny konversation** om du vill informera AEM AI Assistant om ett nytt ämne eller om ett nytt ämne.

### Använd identifiering

AEM AI Assistant innehåller en funktion som hjälper dig att utforska de ämnen och kategorier som stöds.

![Ideas glödlampsikon](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Så här använder du identifierbarhet:**

1. Klicka på ikonen ![Lär dig mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) i det övre högra hörnet av AEM AI Assistant.
1. Välj en kategori om du vill visa en lista med relaterade uppmaningar.
1. Välj ett kommando för att bättre förstå vilka typer av frågor som AEM AI Assistant kan besvara.

### Ge feedback på AEM AI Assistant

Dina indata hjälper till att förbättra AEM AI Assistant för bättre prestanda och precision.

Dela med dig av dina synpunkter på ditt arbete med AEM AI Assistant genom följande alternativ:

![Tummen uppåt, tummen nedåt och flaggikoner](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Ikon | Beskrivning |
| --- | --- |
| ![Miniatyrbilderna är en ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Klicka för att ange vad som gick bra och för att dela positiv feedback. |
| ![Miniatyrbilder nedåt, ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Klicka för att ge förslag på förbättringar. Lägg till specifika kommentarer om din upplevelse, som granskas dagligen. |
| ![Flaggikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Klicka för att rapportera eventuella problem eller ge detaljerad feedback om din interaktion med AEM AI Assistant. |

## Frågor och svar om AEM AI Assistant {#ai-faq}

Här är svar på några vanliga frågor om AI-assistenten:

* **Tillhandahåller AEM AI Assistant information i realtid?**\
  Nej. AI Assistant hämtar sitt innehåll från Adobe Experience League-dokumentation. Det kan ta lite tid att reflektera över uppdateringarna i svaren.
* **Vilka Adobe-program stöder AEM AI Assistant?**\
  För närvarande stöder AI Assistant produktkunskapsfrågor i AEM as a Cloud Service, inklusive Sites, Assets, Dynamic Media, Cloud Manager och Forms.
* **Vilka funktioner har AEM AI Assistant?**\
  AEM AI Assistant är utformat för att besvara frågor om Adobe produktkunskaper.
* **Använder AEM AI Assistant personlig information för utbildningsdata?**\
  Nej. AEM AI Assistant använder inte personuppgifter för utbildningsändamål. Undvik att dela personuppgifter om dig själv eller andra, inklusive namn eller kontaktuppgifter, med AEM AI Assistant.


## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

Förutom den allmänna AEM AI Assistant för produktinformation erbjuder AEM en specialiserad **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. Denna förbättrade assistent kan aktivt hjälpa dig att skapa och konfigurera formulär med hjälp av naturliga språkfrågor och svar på frågor som är specifika för formulär.

### Viktiga funktioner

AEM Forms AI Assistant ger:

* **Skapa formulär**: Skapa nya formulär från grunden med naturliga språkbeskrivningar.
* **Designimport**: Konvertera befintliga designer (PDF, Figma, bilder) till fungerande AEM Forms.
* **Formulärkonfiguration**: Lägg till fält, paneler, verifieringsregler och villkorslogik.
* **Layouthantering**: Ordna formulärstrukturen och optimera för olika enheter.
* **Integrationsinstallation**: Konfigurera formuläröverföringar och datahantering.
* **Produktkunskap**: Svara på frågor om AEM Forms funktioner och bästa praxis.

### Åtkomstplats

AEM Forms AI Assistant finns i:

* **Universell redigerare**: För Edge Delivery Services-formulär med visuella redigeringsfunktioner.
* **Adaptiv Forms Editor**: För detaljerad formulärkonfiguration och avancerade funktioner.
* **Forms Management UI**: För formulärskapande och hanteringsåtgärder på hög nivå.

### Komma igång

>[!NOTE]
>
> AEM Forms AI Assistant (Forms Experience Builder) är tillgängligt via det privata betaprogrammet. Skicka ett e-postmeddelande från din arbetsadress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) för att begära åtkomst.

Mer information om hur du använder AEM Forms AI Assistant finns i [dokumentationen för AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md).

### Exempel på användningsfall

* **&quot;Skapa ett formulär för kundfeedback med namn, e-post, betyg och kommentarfält&quot;**
* **&quot;Konvertera det här överförda PDF-programformuläret till ett digitalt anpassat formulär&quot;**
* **&quot;Lägg till villkorlig logik om du bara vill visa information om make/maka när civilstånd är gift&quot;**
* **&quot;Konfigurera det här formuläret för att skicka data till systemet för kundrelationshantering&quot;**

Denna specialiserade AEM Forms AI Assistant utgör nästa steg i formulärskapandet och kombinerar styrkan i AI med AEM kraftfulla formulärfunktioner för att effektivisera arbetsflödet för att skapa formulär.

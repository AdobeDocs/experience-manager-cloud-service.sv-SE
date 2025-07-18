---
title: AI Assistant i Adobe Experience Manager (privat beta)
description: Använd AI Assistant i Adobe Experience Manager för att hitta svar, felsöka och utforska webbplatser, Assets, Dynamic Media, Cloud Manager och Forms.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 0afd74120380c9ae3d02db9fb684189c2f19648f
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---

# Om AEM AI Assistant i Adobe Experience Manager {#aem-home}

AI Assistant i AEM (Adobe Experience Manager) har ett konversationsgränssnitt som gör det enkelt att hitta svar på frågor som rör Adobe Experience Manager. Det hjälper dig att få tillgång till produktinformation, felsöka problem och utforska information som finns i Experience League. Under det privata betaprogrammet stöder AEM AI Assistant Adobe Experience Manager as a Cloud Service, inklusive Sites, Assets, Dynamic Media, Cloud Manager och Forms.

>[!IMPORTANT]
>Kontrollera att du har granskat och skickat in användaravtalet så att Adobe kan aktivera AI Assistant-funktionen så att du kan testa och delta i det privata betaprogrammet.
>
>Om du har några frågor skickar du ett e-postmeddelande till [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

## Integritet, säkerhet och styrning

AEM AI Assistant är utformat med stor betoning på sekretess, säkerhet och styrning.

I den här artikeln beskrivs de förtroendecentrerade funktioner som du kan förvänta dig av AEM AI Assistant:

* AEM AI Assistant använder inga personuppgifter, inte ens i utbildningssyfte.
* AEM AI Assistant har inte åtkomst till konsumentdata.
* Explicit behörighet krävs för att interagera med AEM AI Assistant.
* Användarspecificerade uppmaningar (frågor, frågor och så vidare) delas inte med andra kunder.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## Lär känna AEM AI Assistant för produktkännedom {#ai-prod-insights}

Produktkunskap omfattar begrepp och ämnen som härletts ur Adobe Experience League-dokumentationen. Dessa frågor kan kategoriseras i följande undergrupper:

| Produktkunskap | Exempel |
| --- | --- |
| Undervisning | <ul><li>Vad är den universella redigeraren?</li><li>Hur skapar jag ett program i Cloud Manager?</li></ul> |
| Öppna identifiering | <ul><li>Hur använder jag Universal Editor?</li><li>Finns det något sätt att kopiera innehåll från en miljö till en annan?</li></ul> |
| Felsökning | <ul><li>Varför har jag inte åtkomst till Universal Editor?</li><li>Varför misslyckas min pipeline?</li></ul> |

AEM AI Assistant har nu fokus på produktkunskapsfrågor för Adobe Experience Manager as a Cloud Service. Detta omfattar omfattande stöd för nyckelområden som Sites, Assets, Forms och Cloud Manager.

## Skapa effektiva frågor {#ai-craft-questions}

För att få de mest korrekta svaren från AEM AI Assistant är det viktigt att formulera dina frågor tydligt och i rätt sammanhang. Använd följande tips för att kontrollera att dina frågor är tydliga och välstrukturerade:

* Ange tydligt din uppgift eller fråga på ett kortfattat sätt.
* Undvik tvetydiga formuleringar eller alltför komplex syntax för att öka förståelsen.
* Lägg in relevant information om arbetsuppgifterna eller frågorna, eftersom detta gör att AEM AI Assistant kan ge mer exakta och relevanta svar.
Till exempel får du hjälp med att namnge den AEM-lösning du arbetar i - Sites, Assets, Dynamic Media, Cloud Manager och Forms.

### Exempel på frågor som inte stöds {#ai-unsupported-questions}

| Område | Exempel |
| --- | --- |
| Driftsinsikter | <ul><li>Hur många utvecklingsmiljöer finns det i min hyresgäst?</li><li>Vem startade den senaste produktionslinjen?</li></ul> |
| Felsökning | <ul><li>Varför misslyckas min produktionsprocess?</li></ul> |
| Uppgift och automatisering | <ul><li>Konfigurera en pipeline för kodkvalitet från en utvecklingsgren åt mig.</li></ul> |


## Använd AEM AI Assistant {#ai-use}

### Få åtkomst till AEM AI Assistant via Admin Console

Om du vill använda AEM AI Assistant måste du anmäla dig på Admin Console-nivå. En produktadministratör skapar (eller väljer) en användargrupp och ger den den nya behörigheten AI Assistant. Alla som läggs till i den gruppen får omedelbart tillgång till assistenten i AEM. Om målet är företagsomfattande tillgänglighet tilldelar administratören helt enkelt alla användare till den gruppen.

![AEM AI Assistant i Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

Ur personalens perspektiv är processen enkel: identifiera produktadministratören för Adobe Experience Manager i din organisation och begär att få läggas till i den AI-aktiverade användargruppen. När du visas i den gruppen visas ikonen Assistant automatiskt nästa gång du loggar in.

Administratörer bör tänka på normal Cloud Manager-styrning. Du måste ha administratörsbehörighet för produkten i Admin Console för att skapa profiler, hantera användargrupper eller redigera behörigheter. Om användarna också behöver assistentens inbyggda **Skapa supportbiljett** -funktion lägger du till standardrollen **Support Admin** (Admin Console standardroll) för samma personer eller grupp.

![Teknisk supportanmälan i AEM AI Assistant i Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

En genomgång av hur du konfigurerar användare och grupper i AEM as a Cloud Service finns i [Konfigurera åtkomst till AEM as a Cloud Service](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/accessing/overview).

Se även [Anpassade behörigheter](/help/implementing/cloud-manager/custom-permissions.md).


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

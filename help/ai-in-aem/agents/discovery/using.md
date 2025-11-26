---
title: Översikt över identifieringsagent
description: Lär dig hur du kan använda Discovery Agent för att leverera relevant AEM-innehåll på begäran via naturliga, konversationsmoment för att få en smidig, klickfri upptäckt.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b7bdb86c3d1b537b536173b6307c486fe436636
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# Identifieringsagent {#discovery-agent}

Identifieringsagenten levererar AEM-material on demand via naturliga, konversationsmoment för en smidig, klickfri upptäckt. Programmet söker på ett intelligent sätt i Assets, Content Fragments och Adaptive Forms för att leverera relevant material som bilder, videor, PDF-dokument, artiklar och formulärmallar. Med det naturliga språket kan du söka efter innehåll utan att behöva skapa komplexa frågor eller använda filter i AEM Assets-gränssnittet. Baserat på din uppmaning returnerar agenten kuraterade resultat tillsammans med metadata för resursen och URL:er för leverans, som är klara att bäddas in i andra program.

Några av fördelarna med Discovery Agent:

* **Identifiering av enhetligt innehåll**: Få tillgång till alla typer av AEM-innehåll, som bilder, videor, PDF-dokument, artiklar och formulär från ett enda konversationsgränssnitt.

* **Snabbare kampanjplanering**: Samla snabbt in bilder och formulär för marknadsföringskampanjer i e-postmeddelanden, på webben och i sociala kanaler.

* **Förbättrad produktivitet**: Minska den tid det tar att söka i databaser eller filtrera metadata via automatiserad, avsiktsbaserad sökning.

* **Konsekvent innehållsanvändning**: Säkerställer återanvändning av godkända resurser och fragment, vilket upprätthåller varumärkets enhetlighet i alla kanaler.

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Kompetens {#skills-discovery-agent}

Identifieringsagenten har följande kunskaper:

* **Identifiering av naturligt språkinnehåll**\
  Med Discovery Agent kan man hitta resurser, innehållsfragment och anpassningsbara formulär i Adobe Experience Manager (AEM) på ett enkelt naturligt språk - inga komplexa sökfrågor krävs.

* **Taggbaserad resursidentifiering**

  Identifieringsagenten använder naturliga språkkommandon för att hitta resurser som är kopplade till särskilda taggar i AEM-databasen, vilket gör att användare snabbt kan komma åt innehåll som är organiserat eller som inte är organiserat enligt organisationens taxonomi.

* **Mappbaserad innehållsidentifiering:**\
  Identifieringsagenten kan identifiera resurser genom att tolka naturliga språkuppmaningar som refererar till mappnamn i AEM. Användarna kan bara ange mappen när de uppmanas till det, utan att navigera i databasen manuellt, vilket avsevärt minskar antalet klick som behövs för att hitta rätt innehåll.

## Personas {#personas-discovery-agent}

### Kampanjansvariga {#campaign-managers}

Identifieringsagenten gör det möjligt för kampanjchefer att snabbt identifiera och återanvända betrott, högpresterande innehåll för idéer.

### Kanalmarknadsförare {#channel-marketers}

Med Discovery Agent kan kanalmarknadsförare effektivt hitta relevanta resurser för att skapa sammanhängande flerkanalsupplevelser.

### DAM-bibliotek {#dam-librarians}

DAM-biblioteken kan flagga resurser som saknar de metadatastandarder som organisationen har angett, vilket ger stöd för enhetlig styrning och säkerställer att resurserna är fullständiga och klara att användas i alla kanaler.

### Byråer och partners {#agencies-partners}

Byråer och partners kan enkelt hitta varumärkesgodkända mediefiler i Content Hub och återanvända dem för att snabba upp det kreativa arbetet samtidigt som de följer varumärkesstandarderna.

## Hur kommer jag åt Discovery Agent? {#access-discovery-agent}

Du kommer åt agenterna i AEM via AI-assistenten. Logga in på experience.adobe.com så kan du börja interagera med AI Assistant genom att ange din uppmaning på ett naturligt språk i sökrutan:

![Åtkomstidentifieringsagent](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

Om du vill ha information om MCP-slutpunkten för att komma åt Discovery Agent kontaktar du Adobe Support.

## Vanliga användningsområden och exempelfrågor {#use-cases-prompts}

### Assets {#discovery-agent-use-cases-assets}

**Taggbaserad resursidentifiering**

Identifieringsagenten använder naturliga språkkommandon för att hitta resurser som är kopplade till särskilda taggar i AEM-databasen, vilket gör att användare snabbt kan komma åt innehåll som är organiserat enligt organisationens taxonomi.

Exempelfråga:

Visa bilder som har taggats `office` i mappen `WKND`.

**Mappbaserad innehållsidentifiering:**\
Identifieringsagenten kan identifiera resurser genom att tolka naturliga språkuppmaningar som refererar till mappnamn i AEM. Användarna kan bara ange mappen när de uppmanas till det, utan att navigera i databasen manuellt, vilket avsevärt minskar antalet klick som behövs för att hitta rätt innehåll.

Exempeluppmaningar:

* Finns det några svgs i mappen `WKND`?
* Visa resurser som ändrats efter `Nov 1 2025` i mappen `WKND`.
* Lista `lifestyle` bilder i mappen `WKND`.

**Upplösning och formatbaserad resursidentifiering**

Identifieringsagenten kan identifiera resurser som uppfyller specifika kvalitetskrav, t.ex. filformat eller minimiupplösning, så att användarna snabbt kan hitta produktbilder som är klara för högkvalitativ leverans och återanvändning i olika kanaler.

Exempelfråga:

Hitta PNG-bilder med produktförpackningar som är minst 2 000 pixlar breda.

**Orienteringsbaserad innehållsidentifiering**

Identifieringsagenten kan filtrera resurser genom att identifiera visuella attribut, som närvaron av personer och bildens orientering. På så sätt kan man snabbt begränsa innehållet till de mest relevanta bilderna utan att manuellt lägga på flera filter i AEM.

Exempelfråga:

Visa resurser med personer i liggande orientering.

### Innehållsfragment {#discovery-agent-use-cases-content-fragments}

Identifieringsagenten hjälper användarna att snabbt hitta rätt innehållsfragment genom att tolka naturliga språkreferenser till kampanjnamn, produktvarumärken, publiceringsstatus och nyligen skapade aktiviteter. Det gör att teamen kan identifiera kampanjklara fragment och visa varumärkesspecifikt innehåll, utan att behöva bläddra bland mappar eller använda flera filter i AEM manuellt.

Exempeluppmaningar:

* Visa innehållsfragment för att skapa WKND-erbjudandekampanj.

* Visa innehållsfragmentet för americano-dryck.

* Visa alla publicerade innehållsfragment för WKND-drycker.

* Lista alla innehållsfragment som skapats de senaste två veckorna.

### Forms {#discovery-agent-use-cases-forms}

Identifieringsagenten hjälper dig att snabbt hitta anpassningsbara formulär med hjälp av naturliga språkinställningar. Den söker igenom formulärinnehåll och metadata för att hitta matchningar baserat på nyckelord från dina uppmaningar. Det innebär att du kan identifiera relevanta formulär även om söktermerna inte finns i formulärets titel eller beskrivning.

Exempeluppmaningar:

* Visa alla låneansökningsblanketter.
* Sök efter formulär att söka efter för ett jobb.
* Hitta kontaktformulär.
* Jag letar efter anställdas introduktionsblanketter.
* Visa formulär för kreditkortsansökningar.

Obs! Formuläridentifiering har för närvarande bara stöd för Edge Delivery Services-formulär, och taggbaserad sökning är för närvarande inte tillgänglig för formulär.

## Sökresultat {#discovery-agent-search-results}

### Assets {#discovery-agent-search-results-assets}

Identifieringsagenten returnerar de översta resultaten för varje fråga, sorterade efter relevans för att säkerställa att de exakta matchningarna visas först. Agenten kombinerar metadatadrivna frågor med semantisk sökning för att sätta ihop en fokuserad uppsättning troliga matchningar, och använder sedan ett LLM för att rangordna dem baserat på användaravsikten. Den här blandningsmetoden ger korrekta, sammanhangsberoende resultat utan att vara helt beroende av en direkt nyckelordsmatchning.

Varje resultat innehåller resursnamn tillsammans med metadata för nyckelresurser som resurssökväg, skapare, skapandedatum, titel, beskrivning, format, senaste ändringsdatum, filstorlek, dimensioner, [URL för dynamiska media](/help/assets/dynamic-media/dynamic-media.md) och associerade taggar. Om en resurs är i ett godkänt tillstånd innehåller resultatet även [Dynamic Media med OpenAPI URL](/help/assets/dynamic-media-open-apis-overview.md).

Du kan klicka på resurssökvägen för att smidigt navigera till resursplatsen i AEM.

![Sök efter resurser med identifieringsagenten](/help/ai-in-aem/agents/discovery/assets/search-results-discovery-agent.png)

Du kan använda den här tillgångsinformationen för att snabbt utvärdera om en resurs uppfyller kraven utan att navigera till varje resurs för att visa dessa detaljer.

>[!NOTE]
>
>Fältet [Dynamisk media-URL](/help/assets/dynamic-media/dynamic-media.md) visas i sökresultatet endast om resursen är publicerad och du har en giltig Dynamic Media-licens. På samma sätt visas endast fältet [Dynamiska media med OpenAPI URL](/help/assets/dynamic-media-open-apis-overview.md) om du har en giltig Dynamic Media-licens och Dynamic Media med OpenAPI är aktiverat för din AEM as a Cloud Service-instans.

### Innehållsfragment {#discovery-agent-search-results-content-fragments}

Identifieringsagenten erbjuder fulltextsökningsfunktioner för innehållsfragment och returnerar de översta resultat som bäst matchar den angivna uppmaningen. Varje resultat innehåller innehållets fragmentnamn tillsammans med viktiga metadatafält, t.ex. sökvägen till innehållsfragmentet, skaparen, datum när det skapades, variationer, senaste modifiering och senast ändrade datumfält.

![Sök efter innehållsfragment med identifieringsagenten](/help/ai-in-aem/agents/discovery/assets/search-content-fragments-discovery-agent.png)

Du kan klicka på sökvägen för innehållsfragment för att smidigt navigera till platsen för innehållsfragment i AEM.

## Uppmana till bästa praxis {#prompting-best-practices-discovery-agent}

Ange kortfattade detaljer i dina naturliga språkfrågor så att agenten kan returnera korrekta och relevanta resultat. Ju tydligare du beskriver vad du söker, desto bättre kan agenten förfina och begränsa resultatet. Du kan till exempel:

* Definiera metadata för resurser som taggar, mappnamn, datum när de skapades, publiceringsstatus, författarnamn i dina uppmaningar för att filtrera resurser.

* Använd era organisationsspecifika metadata, t.ex. kategorier (löpande skor, elektronik), säsonger (höst, vår), händelser (svart fredag, produktlansering) och kanaler (webb, e-post, utskrift) för att filtrera innehållet ytterligare.


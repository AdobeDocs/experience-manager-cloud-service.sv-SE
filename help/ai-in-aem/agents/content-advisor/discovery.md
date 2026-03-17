---
title: Innehållsidentifieringsagent
description: Lär dig hur du kan använda agenten för innehållsidentifiering för att leverera relevant AEM-innehåll på begäran via naturliga, konversationsmoment för en smidig, klickfri identifieringsupplevelse.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 676300cd-b799-4c53-a58e-043e58a2cbc5
source-git-commit: 45c547a0a7372e5ebe23bd6b816798cd3b225872
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 0%

---


# Innehållsidentifieringsagent {#discovery-agent}

Som en del av AEM [Content Advisor-agenten](/help/ai-in-aem/agents/content-advisor/overview.md) levererar innehållsidentifieringsagenten AEM-innehåll på begäran via naturliga, konversationsmoment för en smidig, klickfri identifieringsupplevelse. Programmet söker på ett intelligent sätt i Assets, Content Fragments, AEM Sites pages och Adaptive Forms för att leverera relevant material som bilder, videor, PDF-dokument, artiklar och formulärmallar. Med det naturliga språket kan du söka efter innehåll utan att behöva skapa komplexa frågor eller använda filter i AEM Assets-gränssnittet. Baserat på din uppmaning returnerar agenten kuraterade resultat tillsammans med metadata för resursen och URL:er för leverans, som är klara att bäddas in i andra program.

Några av fördelarna med innehållsidentifieringsagenten är:

* **Identifiering av enhetligt innehåll**: Få tillgång till alla typer av AEM-innehåll, som bilder, videor, PDF-dokument, artiklar, sidor och formulär från ett enda konversationsgränssnitt.

* **Snabbare kampanjplanering**: Samla snabbt in bilder och formulär för marknadsföringskampanjer i e-postmeddelanden, på webben och i sociala kanaler.

* **Förbättrad produktivitet**: Minska den tid det tar att söka i databaser eller filtrera metadata via automatiserad, avsiktsbaserad sökning.

* **Konsekvent innehållsanvändning**: Säkerställer återanvändning av godkända resurser och fragment, vilket upprätthåller varumärkets enhetlighet i alla kanaler.

>[!VIDEO](https://video.tv.adobe.com/v/3479983)

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

## Kompetens {#skills-discovery-agent}

Agenten för innehållsidentifiering tillhandahåller följande färdigheter:

* **Identifiering av naturligt språkinnehåll**

  Med Content Discovery-agenten kan användarna hitta relevanta resurser, innehållsfragment, adaptiva formulär och AEM Sites-sidor i Adobe Experience Manager (AEM) med enkla, naturliga språkkommandon - inga komplexa sökfrågor krävs.

* **Metadatabaserad resursidentifiering**

  Innehållsidentifieringsagenten använder naturliga språkuppmaningar för att hitta resurser baserat på metadata som är tillgängliga för resurser i AEM. Användare kan identifiera resurser med hjälp av metadata som taggar, e-post-ID för författare eller utgivare, publicerade eller ändrade datum, MIME-typ, resurstyp, status, anpassade metadataegenskaper som definieras i metadataformulär i Assets-vyn eller administratörsvyn, osv. En fullständig lista finns i [Vanliga användningsfall och Exempelfrågor](#use-cases-prompts).

  Du kan också kombinera flera metadatafilter i en enda dialogruta för att förfina sökresultaten.

* **Mappbaserad innehållsidentifiering:**\
  Agenten för innehållsidentifiering kan identifiera resurser genom att tolka naturliga språkuppmaningar som refererar till mappnamn i AEM. Användarna kan bara ange mappen när de uppmanas till det, utan att navigera i databasen manuellt, vilket avsevärt minskar antalet klick som behövs för att hitta rätt innehåll.

## Personas {#personas-content-discovery}

### Kampanjansvariga {#campaign-managers}

Med hjälp av agenten för innehållsidentifiering kan kampanjansvariga snabbt identifiera och återanvända betrott, högpresterande innehåll för idéer.

### Kanalmarknadsförare {#channel-marketers}

Med hjälp av innehållsidentifieringsagenten kan kanalmarknadsförare effektivt hitta relevanta resurser för att skapa sammanhängande flerkanalsupplevelser.

### DAM-bibliotek {#dam-librarians}

DAM-bibliotek kan flagga resurser som saknar de metadatastandarder som organisationen har angett, vilket ger stöd för enhetlig styrning och säkerställer att resurserna är fullständiga och klara att användas i alla kanaler.

### Byråer och partners {#agencies-partners}

Myndigheter och partners kan enkelt hitta varumärkesgodkända mediefiler i Content Hub och återanvända dem för att snabba upp det kreativa arbetet samtidigt som de följer varumärkesstandarderna.

## Åtkomst {#access}

Du kan nå innehållsidentifieringsagenten i AEM via AI-assistenten. Logga in på [`experience.adobe.com`](https://experience.adobe.com) så kan du börja interagera med AI Assistant genom att ange din uppmaning på det naturliga språket i sökrutan:

![Åtkomst till agenten för innehållsidentifiering](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

Kontakta Adobe Support om du vill ha information om MCP-slutpunkten för åtkomst till agenten för innehållsidentifiering.

## Vanliga användningsfall och exempelfrågor {#use-cases-prompts}

### Assets {#discovery-agent-use-cases-assets}

**Metadatabaserad resursidentifiering**

Innehållsidentifieringsagenten använder naturliga språkuppmaningar för att hitta resurser baserat på metadata som är tillgängliga för resurser i AEM. Användare kan identifiera resurser med hjälp av följande metadataegenskaper: Taggar, Skapad med e-post-ID, Ändrad med e-post-ID, Publicerad med e-post-ID, Skapad den, Publicerat den, MIME-typ, Resurstyp, Status, Filformat, Bildstorlek, Bildhöjd och flera metadatafilter i ett och samma fönster.

Innehållsidentifieringsagenten söker även efter de anpassade egenskaper som finns i metadatascheman för administratörsvyn och metadataformulär för Assets-vyn. Du kan ändra dina uppmaningar i enlighet med detta för att söka efter värden som är tillgängliga i de anpassade resursegenskaperna.

>[!NOTE]
>
>Indexera relevanta anpassade metadataegenskaper för att förbättra identifieringsprestanda. Med indexerade egenskaper kan agenten hämta matchande innehåll snabbare när användarna tar med dessa egenskaper i sina uppmaningar.


Exempeluppmaningar:

* **Sök baserat på taggar**: Visa bilder som taggats `office` i mappen `WKND`.
* **Sök baserat på filformat, resurstyp, objektstatus och publicerat med e-post-ID**: Visa bilder i `.PNG`-format som är `approved` och `published by <user email ID>`.
* **Sök baserat på filformat, resurstyp, resursstatus och Skapat med e-post-ID**: Visa videoklipp i `.mp4`-format som har godkänts och `created by <user email ID>`.
* **Sök baserat på filformat, resurstyp, resursstatus och Skapad**: Visa bilder i `.PNG`-format som har skapats efter 1 januari 2025 och `published by <user email ID>`
* **Sök baserat på MIME-typ, Skapad och Publicerad av e-post-ID**: Visa `image/jpeg` som skapats efter `January 1, 2025` och `published by <user email ID>`.
* **Sök baserat på filformat och anpassade metadataegenskaper**: Visa bilder i `.JPEG`-format som har `Product SKU ID as <SKU value>`.

* **Sök efter resurser som saknar metadata**: Visa resurser som skapats de senaste 90 dagarna med `<Name of metadata property including custom properties>` är tomma.

* **Sök efter resurser med hjälp av filstorlek, bildbredd och bildhöjd**: Visa bilder som är större än 5 MB med en bredd som är större än 2 000 pixlar och en höjd som är större än 1 200 pixlar.


**Mappbaserad innehållsidentifiering:**\
Innehållsidentifieringsagenten kan identifiera resurser genom att tolka naturliga språkuppmaningar som refererar till mappnamn i AEM. Användarna kan bara ange mappen när de uppmanas till det, utan att navigera i databasen manuellt, vilket avsevärt minskar antalet klick som behövs för att hitta rätt innehåll.

Exempeluppmaningar:

* Finns det några svgs i mappen `WKND`?
* Visa resurser som ändrats efter `Nov 1 2025` i mappen `WKND`.
* Lista `lifestyle` bilder i mappen `WKND`.

**Ytterligare frågor för att aktivera mappbaserad innehållsidentifiering**

När ett mappnamn ingår i en fråga (utan den fullständiga resurssökvägen) söker Content Discovery-agenten först efter en matchande mapp på rotsökvägen `/content/dam/<folder-name>`.

Om ingen matchande mapp hittas på rotnivå föreslår agenten alternativa mappsökvägar där det angivna mappnamnet finns i databasen. Detta gör att användarna snabbt kan hitta rätt plats utan att behöva bläddra i mappstrukturen manuellt.

Sökvägen `/content/dam/<folder-name>` hittades till exempel inte. Menade du en av de här?

* Alternativ 1

* Alternativ 2

**Formatbaserad resursidentifiering**

Agenten för innehållsidentifiering kan identifiera resurser som uppfyller specifika kvalitetskrav, till exempel filformat, så att användarna snabbt kan hitta produktbilder som är klara för högklassig leverans och återanvändning i olika kanaler.

Exempelfråga:

Hitta PNG-bilder för produktförpackningar.

**Orienteringsbaserad innehållsidentifiering**

Agenten för innehållsidentifiering kan filtrera resurser genom att identifiera visuella attribut, som närvaron av personer och bildens orientering. På så sätt kan man snabbt begränsa innehållet till de mest relevanta bilderna utan att manuellt lägga på flera filter i AEM.

Exempelfråga:

Visa resurser med personer i liggande orientering.

**Expanderar sökresultat**

Innehållsidentifieringsagenten returnerar de 20 mest relevanta resultaten per innehållstyp för att få en fråga. Om ytterligare matchande resultat är tillgängliga kan användare begära nästa uppsättning genom att ange en uppföljningsfråga som `show me more`. Agenten hämtar sedan nästa uppsättning resultat från den ursprungliga sökningen, vilket gör att användarna kan utforska större resultatuppsättningar utan att behöva förfina frågan.

**Söker efter liknande resurser**

Med Content Discovery Agent kan användare hitta resurser som liknar ett specifikt resultat som returneras i sökresultaten. När agenten visar de översta resultaten för en fråga kan du begära liknande resurser genom att referera till positionen för ett objekt i resultatlistan. En uppmaning som `find assets similar to the 3rd result` instruerar agenten att identifiera och returnera andra relevanta tillgångar som hör till objektet. Detta hjälper användarna att snabbt identifiera relaterat innehåll utan att skapa en ny sökfråga.

**Sorterar sökresultat**

Med hjälp av innehållsidentifieringsagenten kan användare sortera sökresultat direkt i de naturliga språkinställningarna. Användare kan ange sorteringsvillkor som ändringsdatum, skapat datum eller resursnamn och välja stigande eller fallande ordning.

Exempeluppmaningar:

* Hitta bilder i bergen sorterade efter ändringsdatum i fallande ordning (visar de senast ändrade resurserna först).

* Visa bergbilder sorterade efter namn i stigande ordning (visar bildnamnen med bokstaven A först följt av B osv.).

### AEM Sites sidor {#content-discovery-agent-aem-sites-pages}

Med Content Discovery-agenten kan man snabbt hitta relevanta AEM Sites-sidor genom att tolka naturliga språkuppmaningar som hänvisar till sidämnen, kampanjer eller andra kontextuella nyckelord. Agenten utför en fulltextsökning baserad på nyckelorden i uppmaningen för att identifiera matchande sidor i AEM-databasen, vilket eliminerar behovet av att bläddra bland webbplatsstrukturen manuellt.

Exempelfrågor:

* Hitta alla AEM Sites-sidor för sommarkampanjen.

* Hitta AEM Sites-sidor med temat Kaffe.

### Innehållsfragment {#discovery-agent-use-cases-content-fragments}

Med Content Discovery Agent kan användarna snabbt hitta rätt innehållsfragment genom att tolka naturliga språkreferenser till kampanjnamn, produktvarumärken, publiceringsstatus och nyligen skapade aktiviteter. Det gör att teamen kan identifiera kampanjklara fragment och visa varumärkesspecifikt innehåll, utan att behöva bläddra bland mappar eller använda flera filter i AEM manuellt.

Exempeluppmaningar:

* Visa innehållsfragment för att skapa WKND-erbjudandekampanj.

* Visa innehållsfragmentet för americano-dryck.

* Visa alla publicerade innehållsfragment för WKND-drycker.

* Lista alla innehållsfragment som skapats de senaste två veckorna.

### Forms {#discovery-agent-use-cases-forms}

Med Content Discovery Agent kan du snabbt hitta anpassningsbara formulär med hjälp av naturliga språkuppmaningar. Den söker igenom formulärinnehåll och metadata för att hitta matchningar baserat på nyckelord från dina uppmaningar. Det innebär att du kan identifiera relevanta formulär även om söktermerna inte finns i formulärets titel eller beskrivning.

Exempeluppmaningar:

* Visa alla låneansökningsblanketter.
* Sök efter formulär att ansöka om för en handläggare.
* Hitta kontaktformulär.
* Jag letar efter anställdas introduktionsblanketter.
* Visa formulär för kreditkortsansökningar.

Obs! Formuläridentifiering har för närvarande bara stöd för Edge Delivery Services-formulär, och taggbaserad sökning är för närvarande inte tillgänglig för formulär.

## Sökresultat {#discovery-agent-search-results}

### Assets {#discovery-agent-search-results-assets}

Agenten för innehållsidentifiering returnerar de högsta resultaten för varje fråga, sorterade efter relevans för att säkerställa att de exakta matchningarna visas först. Agenten kombinerar metadatadrivna frågor med semantisk sökning för att sätta ihop en fokuserad uppsättning troliga matchningar, och använder sedan ett LLM för att rangordna dem baserat på användaravsikten. Den här blandningsmetoden ger korrekta, sammanhangsberoende resultat utan att vara helt beroende av en direkt nyckelordsmatchning.

Varje resultat innehåller resursnamn tillsammans med metadata för nyckelresurser som resurssökväg, skapare, skapandedatum, titel, beskrivning, format, senaste ändringsdatum, filstorlek, dimensioner, [URL för dynamiska media](/help/assets/dynamic-media/dynamic-media.md) och associerade taggar. Om en resurs är i ett godkänt tillstånd innehåller resultatet även [Dynamic Media med OpenAPI URL](/help/assets/dynamic-media-open-apis-overview.md).

Du kan klicka på resurssökvägen för att smidigt navigera till resursplatsen i AEM.

![Sök efter resurser med hjälp av agenten för innehållsidentifiering](/help/ai-in-aem/agents/content-advisor/assets/search-results-discovery-agent.png)

Du kan använda den här tillgångsinformationen för att snabbt utvärdera om en resurs uppfyller kraven utan att navigera till varje resurs för att visa dessa detaljer.

>[!NOTE]
>
>Fältet [Dynamisk media-URL](/help/assets/dynamic-media/dynamic-media.md) visas i sökresultatet endast om resursen är publicerad och du har en giltig Dynamic Media-licens. På samma sätt visas endast fältet [Dynamiska media med OpenAPI URL](/help/assets/dynamic-media-open-apis-overview.md) om du har en giltig Dynamic Media-licens och Dynamic Media med OpenAPI är aktiverat för din AEM as a Cloud Service-instans.

### Innehållsfragment {#discovery-agent-search-results-content-fragments}

Agenten för innehållsidentifiering innehåller funktioner för fulltextsökning för innehållsfragment, vilket returnerar de högsta resultaten som bäst matchar den angivna uppmaningen. Varje resultat innehåller innehållets fragmentnamn tillsammans med viktiga metadatafält, t.ex. sökvägen till innehållsfragmentet, skaparen, datum när det skapades, variationer, senaste modifiering och senast ändrade datumfält.

![Sök efter innehållsfragment med hjälp av agenten för innehållsidentifiering](/help/ai-in-aem/agents/content-advisor/assets/search-content-fragments-discovery-agent.png)

Du kan klicka på sökvägen för innehållsfragment för att smidigt navigera till platsen för innehållsfragment i AEM.

## Fråga efter bästa praxis {#prompting-best-practices-discovery-agent}

Ange kortfattade detaljer i dina naturliga språkfrågor så att agenten kan returnera korrekta och relevanta resultat. Ju tydligare du beskriver vad du söker, desto bättre kan agenten förfina och begränsa resultatet. Du kan till exempel:

* Definiera metadata för resurser som taggar, mappnamn, datum när de skapades, publiceringsstatus, författarnamn i dina uppmaningar för att filtrera resurser.

* Använd era organisationsspecifika metadata, t.ex. kategorier (löpande skor, elektronik), säsonger (höst, vår), händelser (svart fredag, produktlansering) och kanaler (webb, e-post, utskrift) för att filtrera innehållet ytterligare.

## Begränsningar {#limitations-discovery-agent}

* Content Discovery Agent stöder endast dimensionsbaserade uppmaningar för bild- och SVG-formattyper. Exempel: `Find images wider than 1080px`.

* Content Hub-administratörer har åtkomst till Content Discovery Agent via Content Hub-portalen, men resultaten hämtas bara från AEM författarinstans. Content Hub Limited-användare kan för närvarande inte utnyttja Content Discovery Agent (kommer snart).

* Funktionen Sök efter liknande fungerar bara för bilder med [förbättringarna Smarta taggar](/help/assets/ai-generated-metadata-assets-view.md).

---
title: Agent för innehållsoptimering
description: Lär dig hur du använder Content Optimization Agent för att förändra hur användare förfinar och anpassar resurser genom att tillämpa naturliga språkinstruktioner för att skapa kanalklara varianter.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b7bdb86c3d1b537b536173b6307c486fe436636
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---


# Agent för innehållsoptimering {#content-optimization-agent}

Agenten för innehållsoptimering omformar hur användare förfinar och anpassar resurser genom att tillämpa naturliga språkinstruktioner för att skapa kanalanpassade variationer. Vare sig det gäller att generera nya renderingar, justera visuella egenskaper, ändra bakgrunder eller förbereda material för specifika digitala kanaler tolkar agenten användaravsikten och utför komplexa redigeringsuppgifter automatiskt. Det fungerar smidigt ihop med Discovery Agent och tar de resurser som hittas och produceras optimerade varianter med [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) som uppfyller varumärkes-, kanals- och kampanjkraven utan manuell designinsats.

Några av fördelarna med Content Optimization:

* **Smidig resursomformning**: Konverterar enkla, konversationsbaserade uppmaningar till exakta bildåtgärder, som storleksändring, skärpa, spegling eller omfärgning, vilket eliminerar behovet av specialredigeringsverktyg.

* **Kanaloptimerade utdata**: Skapa snabbt renderingar som är anpassade för specifika plattformar som Instagram Stories, webbanderoller eller andra kontaktytor för marknadsföring, så att materialet är klart för omedelbar användning.

* **Förbättring av Creative i stor skala**: Använder visuella justeringar och förbättringar, t.ex. bakgrundsändringar eller grafiska överlägg, för att stödja kreativa arbetsflöden i stora volymer utan att teamen blir långsammare.

* **[Sömlöst samarbete med identifieringsagenten](/help/ai-in-aem/agents/discovery/using.md)**: Bygger på de resurser som identifieras av identifieringsagenten, vilket möjliggör fullständig hämtning och optimering av resurser genom naturlig konversation.

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Förutsättningar {#prerequisites-content-optimization-agent}

Generera variationer eller optimeringar för bildresurser. Du måste ha:

* En giltig Dynamic Media-licens

* Dynamic Media med OpenAPI aktiverat i AEM as a Cloud Service-miljö.

* Resurserna i [godkänt läge](/help/assets/manage-organize-assets-view.md#manage-asset-status) i din AEM as a Cloud Service-miljö.


## Kompetens {#skills-content-optimization-agent}

Innehållsoptimeringsagenten ger följande kunskaper:

* **Förstå återgivning via naturligt språk**

  Innehållsoptimeringsagenten tolkar användaravsikter från naturliga språkuppmaningar, redovisning av kanal, kampanj och målgruppskontext för att avgöra de mest relevanta optimeringsåtgärderna.

* **Genererar varianter för dynamiskt innehåll**

  Agenten för innehållsoptimering skapar optimerade varianter som dynamiska URL-adresser som är anpassade för olika kanaler och formattyper.

* **Optimerar bildinnehåll**

  Agenten för innehållsoptimering använder förbättringar som formatkonvertering, upplösningsjusteringar, beskärning och skärpa för att förbättra bildkvaliteten.

* **Optimering av flera varianter av resurser**

  Innehållsoptimeringsagenten kan generera flera optimerade bildvariationer från de resurser som returneras av Discovery Agent med en enda naturlig språkprompt, vilket gör att användarna kan producera kanalklara återgivningar snabbt och effektivt.

## Personas {#personas-content-optimization-agent}

Channel Marketers, nyckelpersonen för Content Optimization Agent, kan välja rätt högupplöst källinnehåll och begära optimerade format som är anpassade för deras kanaler och målgruppssegment.

Regional Marketers och Agency Workers kan också använda Content Optimization Agent för att snabbt generera kanalklara bildvarianter som stöder snabbare och enhetligare innehållsproduktion.

## Hur kommer jag åt Content Optimization Agent? {#access-content-optimization-agent}

Du kommer åt agenterna i AEM via AI-assistenten. Logga in på experience.adobe.com så kan du börja interagera med AI Assistant genom att ange din uppmaning på det naturliga språket i fältet `Ask AI Assistant anything`:

![Åtkomstidentifieringsagent](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

## Vanliga användningsområden och exempelfrågor {#use-cases-prompts}

Använd uppmaningar om innehållsoptimering genom att söka efter rätt resurser via [identifieringsagenten](/help/ai-in-aem/agents/discovery/using.md). När de relevanta bilderna visas kan användarna generera optimerade eller kanalspecifika varianter för en eller flera resurser direkt från sökresultatet. Detta arbetsflöde ger högkvalitativa indata och konsekvent bättre optimeringsresultat. [Se den fullständiga listan över tillgängliga optimeringar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/).

* **Skapa återgivning med hög upplösning**

  Agenten kan generera nya återgivningar av en mediefil med en angiven upplösning och kvalitetsnivå, vilket gör det enkelt att förbereda kanalklara variationer utan manuell redigering.


  Exempelfråga:

  Skapa en `2000px`-återgivning som `JPEG` med kvaliteten `80%`.

  Sök efter rätt resurs med [identifieringsagenten](/help/ai-in-aem/agents/discovery/using.md) och använd sedan följande uppmaningar om det finns flera sökresultat:

  För det tredje sökresultatet skapar du en `2000px`-återgivning som `JPEG` med `80%`-kvalitet.

  ELLER

  Generera en 2 000 px-rendering som `Asset ID` med `JPEG` kvalitet för `80%`

* **Bildförbättring**

  Agenten kan lägga in visuella förbättringar - som skärpa - för att säkerställa att materialet ser skarpt och väldefinierat ut innan det används i olika kampanjer.

  Exempelfråga:

  Öka skärpan i bilden.


* **Justeringar för bakgrundsfärg**

  Agenten kan uppdatera eller ersätta bakgrundsfärger i genomskinliga mediefiler, med stöd för varumärkesspecifika färgscheman eller kampanjdrivna visuella teman.

  Exempelfråga:

  Ändra bakgrundsfärgen för `PNG` till `#ff8932`.

* **Orienteringsomformningar**

  Agenten kan vända eller spegla bilder för att passa in i layouten eller den kreativa riktningen, utan att behöva använda externa redigeringsverktyg.

  Exempelfråga:

  Spegla bilden vågrätt.

* **Kanaloptimerade återgivningar**

  Agenten kan producera renderingar som är anpassade efter plattformsspecifika krav, som Instagram Stories, och säkerställa att materialet automatiskt uppfyller format, proportioner och kvalitetskrav.

  Exempelfråga:

  Skapa en återgivning för en `Instagram`-artikel.

* **Varumärkesövertäckningar och sammansatt generering**

  Agenten kan lägga in kampanjgrafik, överlägg eller märken i befintliga resurser med exakt placering, vilket gör det möjligt att snabbt skapa kampanjfärdiga montage.

  Exempelfråga:

  Täck över bilden med `30%` rabattbilder över kampanjbanderollen och placera den `100px` från mitten.

  >[!NOTE]
  >
  >Övertäckningspositionerna kanske inte är korrekta.


## Optimeringsresultat {#content-optimization-agent-results}

När du anger en optimeringsprompt returnerar Content Optimization Agent den förbättrade resursen tillsammans med praktiska åtkomstalternativ som baseras på resurstypen:

* **Bilder**: Svaret innehåller en miniatyrförhandsvisning och alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade bilden.

* **PDF-dokument**: Svaret innehåller en miniatyrförhandsvisning och alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade filen.

* **Videor**: Svaret innehåller alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade videon.

![Resultat av innehållsoptimering](/help/ai-in-aem/agents/content-optimization/assets/download-content-optimization.png)

Resultatet gör det enkelt att granska det optimerade resultatet och omedelbart använda det i efterföljande kanaler eller arbetsflöden.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some of the prompting best practices:

* Be explicit about the enhancement you want the Content Optimization Agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->

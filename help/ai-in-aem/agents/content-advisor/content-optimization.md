---
title: Agent för innehållsoptimering
description: Lär dig hur du använder innehållsoptimeringsagenten för att förändra hur användare förfinar och anpassar resurser genom att tillämpa naturliga språkinstruktioner för att skapa kanalanpassade variationer.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 896fc25b-7f60-47b8-9264-2ef6b85d954c
source-git-commit: 45c547a0a7372e5ebe23bd6b816798cd3b225872
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---


# Agent för innehållsoptimering {#content-optimization-agent}

Som en del av [AEM Content Advisor-agenten](/help/ai-in-aem/agents/content-advisor/overview.md) omvandlar innehållsoptimeringsagenten hur användare förfinar och anpassar resurser genom att tillämpa naturliga språkinstruktioner för att skapa kanalklara varianter. Vare sig det gäller att generera nya renderingar, justera visuella egenskaper, ändra bakgrunder eller förbereda material för specifika digitala kanaler tolkar agenten användaravsikten och utför komplexa redigeringsuppgifter automatiskt. Det fungerar sömlöst med [agenten för innehållsidentifiering,](/help/ai-in-aem/agents/content-advisor/discovery.md) tar de resurser som hittas och producerar optimerade variationer med [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) som uppfyller varumärkes-, kanals- och kampanjkraven utan manuell designinsats.

Några av fördelarna med innehållsoptimeringsagenten är:

* **Smidig resursomformning**: Konverterar enkla, konversationsbaserade uppmaningar till exakta bildåtgärder, som storleksändring, skärpa, spegling eller omfärgning, vilket eliminerar behovet av specialredigeringsverktyg.

* **Kanaloptimerade utdata**: Skapa snabbt renderingar som är anpassade för specifika plattformar som Instagram Stories, webbanderoller eller andra kontaktytor för marknadsföring, så att materialet är klart för omedelbar användning.

* **Förbättring av Creative i stor skala**: Använder visuella justeringar och förbättringar, t.ex. bakgrundsändringar eller grafiska överlägg, för att stödja kreativa arbetsflöden i stora volymer utan att teamen blir långsammare.

* **[Smidigt samarbete med innehållsidentifieringsagenten](/help/ai-in-aem/agents/content-advisor/discovery.md)**: Bygger på de resurser som identifieras av innehållsidentifieringsagenten, vilket möjliggör fullständig hämtning och optimering via naturlig konversation.

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

>[!VIDEO](https://video.tv.adobe.com/v/3480078)

## Förutsättningar {#prerequisites-content-optimization-agent}

Generera variationer eller optimeringar för bildresurser. Du måste ha:

* En giltig Dynamic Media-licens

* Dynamic Media med OpenAPI aktiverat i AEM as a Cloud Service-miljö.

* Resurserna i [godkänt läge](/help/assets/manage-organize-assets-view.md#manage-asset-status) i din AEM as a Cloud Service-miljö.

## Kompetens {#skills-content-optimization-agent}

Agenten för innehållsoptimering tillhandahåller följande färdigheter:

* **Förstå återgivning via naturligt språk**

  Agenten för innehållsoptimering tolkar användaravsikter från naturliga språkuppmaningar, redovisning av kanaler, kampanjer och målgruppskontext för att avgöra de mest relevanta optimeringsåtgärderna.

* **Genererar varianter för dynamiskt innehåll**

  Agenten för innehållsoptimering skapar optimerade varianter som dynamiska URL-adresser som är anpassade för olika kanaler och formattyper.

* **Optimerar bildinnehåll**

  Agenten för innehållsoptimering använder förbättringar som formatkonvertering, upplösningsjusteringar, beskärning och skärpa för att förbättra bildkvaliteten.

* **Optimering av flera varianter av resurser**

  Agenten för innehållsoptimering kan generera flera optimerade bildvariationer från de resurser som returneras av agenten för innehållsidentifiering med en enda naturlig språkprompt, så att användarna kan producera kanalklara återgivningar snabbt och effektivt.

## Personas {#personas-content-optimization-agent}

Kanalmarknadsförarna, nyckelpersonen för innehållsoptimeringsagenten, kan välja rätt högupplöst källinnehåll och begära optimerade format som är anpassade för deras kanaler och målgruppssegment.

Regionala marknadsförare och anställda på byråer kan också använda innehållsoptimeringsagenten för att snabbt generera kanalklara bildvariationer som stöder snabbare och enhetligare innehållsproduktion.

## Åtkomst {#access-content-optimization-agent}

Du kommer åt innehållsoptimeringsagenten i AEM via AI Assistant. Logga in på [`experience.adobe.com`](https://experience.adobe.com) så kan du börja interagera med AI Assistant genom att ange din uppmaning på det naturliga språket i fältet `Ask AI Assistant anything`:

![Åtkomst till agent för innehållsoptimering](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

## Vanliga användningsfall och exempelfrågor {#use-cases-prompts}

Använd agenten för innehållsoptimering genom att söka efter rätt resurser via agenten för innehållsidentifiering i [.](/help/ai-in-aem/agents/content-advisor/discovery.md) När de relevanta bilderna visas kan användarna generera optimerade eller kanalspecifika varianter för en eller flera resurser direkt från sökresultatet. Användarna kan också generera varianter genom att ange resursens UUID eller resurssökväg i prompten, utan att behöva göra en tidigare sökning. Detta arbetsflöde ger högkvalitativa indata och konsekvent bättre optimeringsresultat. [Se den fullständiga listan över tillgängliga optimeringar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) för mer information.

* **Skapa återgivning med hög upplösning**

  Agenten kan generera nya återgivningar av en mediefil med en angiven upplösning och kvalitetsnivå, vilket gör det enkelt att förbereda kanalklara variationer utan manuell redigering.


  Exempelfråga:

  Skapa en `2000px`-återgivning som `JPEG` med kvaliteten `80%`.

  Sök efter rätt resurs med [innehållsidentifieringsagenten](/help/ai-in-aem/agents/content-advisor/discovery.md) och använd sedan följande uppmaningar om det finns flera sökresultat:

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

När du anger en optimeringsprompt returnerar innehållsoptimeringsagenten den förbättrade resursen tillsammans med praktiska åtkomstalternativ som baseras på resurstypen:

* **Bilder**: Svaret innehåller en miniatyrförhandsvisning och alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade bilden.

* **PDF-dokument**: Svaret innehåller en miniatyrförhandsvisning och alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade filen.

* **Videor**: Svaret innehåller alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade videon.

![Resultat av innehållsoptimering](/help/ai-in-aem/agents/content-advisor/assets/download-content-optimization.png)

Resultatet gör det enkelt att granska det optimerade resultatet och omedelbart använda det i efterföljande kanaler eller arbetsflöden.


## Begränsningar {#limitations-content-optimization}

* Det går inte att ange bakgrundsfärg.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some prompting best practices:

* Be explicit about the enhancement you want the content optimization agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->

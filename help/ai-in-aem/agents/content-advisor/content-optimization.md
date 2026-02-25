---
title: Innehållsoptimeringsjobb
description: Lär dig hur du använder innehållsoptimeringsjobbet för att förändra hur användare förfinar och anpassar resurser genom att tillämpa naturliga språkinstruktioner för att skapa kanalklara varianter.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 896fc25b-7f60-47b8-9264-2ef6b85d954c
source-git-commit: a31cd8ea0ae02a51efb748097c195d68dc8b554d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# Innehållsoptimeringsjobb {#content-optimization-job}

Som en del av [AEM Content Advisor-agenten](/help/ai-in-aem/agents/content-advisor/overview.md) förändrar innehållsoptimeringsjobbet hur användare förfinar och anpassar resurser genom att tillämpa naturliga språkinstruktioner för att skapa kanalklara varianter. Vare sig det gäller att generera nya renderingar, justera visuella egenskaper, ändra bakgrunder eller förbereda material för specifika digitala kanaler, tolkar jobbet användaravsikten och utför komplexa redigeringsuppgifter automatiskt. Det fungerar sömlöst med [jobbet för innehållsidentifiering,](/help/ai-in-aem/agents/content-advisor/discovery.md) tar de resurser som hittas och producerar optimerade variationer med [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) som uppfyller varumärkes-, kanals- och kampanjkraven utan manuell designinsats.

Några av fördelarna med innehållsoptimeringsjobbet är:

* **Smidig resursomformning**: Konverterar enkla, konversationsbaserade uppmaningar till exakta bildåtgärder, som storleksändring, skärpa, spegling eller omfärgning, vilket eliminerar behovet av specialredigeringsverktyg.

* **Kanaloptimerade utdata**: Skapa snabbt renderingar som är anpassade för specifika plattformar som Instagram Stories, webbanderoller eller andra kontaktytor för marknadsföring, så att materialet är klart för omedelbar användning.

* **Förbättring av Creative i stor skala**: Använder visuella justeringar och förbättringar, t.ex. bakgrundsändringar eller grafiska överlägg, för att stödja kreativa arbetsflöden i stora volymer utan att teamen blir långsammare.

* **[Smidigt samarbete med innehållsidentifieringsjobbet](/help/ai-in-aem/agents/content-advisor/discovery.md)**: Bygger på de resurser som identifieras av innehållsidentifieringsjobbet och aktiverar hämtning och optimering av resurser från början till slut via naturlig konversation.

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

>[!VIDEO](https://video.tv.adobe.com/v/3480078)

## Förutsättningar {#prerequisites-content-optimization-job}

Generera variationer eller optimeringar för bildresurser. Du måste ha:

* En giltig Dynamic Media-licens

* Dynamic Media med OpenAPI aktiverat i AEM as a Cloud Service-miljö.

* Resurserna i [godkänt läge](/help/assets/manage-organize-assets-view.md#manage-asset-status) i din AEM as a Cloud Service-miljö.

## Kompetens {#skills-content-optimization-job}

Innehållsoptimeringsjobbet ger följande kunskaper:

* **Förstå återgivning via naturligt språk**

  Innehållsoptimeringsjobbet tolkar användaravsikter från naturliga språkuppmaningar, redovisning av kanal, kampanj och målgruppskontext för att avgöra de mest relevanta optimeringsåtgärderna.

* **Genererar varianter för dynamiskt innehåll**

  Innehållsoptimeringsjobbet skapar optimerade varianter som dynamiska URL:er som är anpassade för olika kanaler och formattyper.

* **Optimerar bildinnehåll**

  Innehållsoptimeringsjobbet använder förbättringar som formatkonvertering, upplösningsjusteringar, beskärning och skärpa för att förbättra bildkvaliteten.

* **Optimering av flera varianter av resurser**

  Innehållsoptimeringsjobbet kan generera flera optimerade bildvariationer från de resurser som returneras av jobbet för innehållsidentifiering med en enda naturlig språkprompt, så att användarna kan producera kanalklara återgivningar snabbt och effektivt.

## Personas {#personas-content-optimization-job}

Kanalmarknadsförare, nyckelpersonen för innehållsoptimeringsjobb, kan välja rätt högupplöst källinnehåll och begära optimerade format som är anpassade för deras kanaler och målgruppssegment.

Regionala marknadsförare och anställda på byråer kan också använda innehållsoptimeringsjobbet för att snabbt generera kanalklara bildvariationer som stöder snabbare och enhetligare innehållsproduktion.

## Åtkomst {#access-content-optimization-job}

Du kommer åt innehållsoptimeringsjobbet i AEM via AI-assistenten. Logga in på [`experience.adobe.com`](https://experience.adobe.com) så kan du börja interagera med AI Assistant genom att ange din uppmaning på det naturliga språket i fältet `Ask AI Assistant anything`:

![Åtkomst till innehållsoptimeringsjobb](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

## Vanliga användningsfall och exempelfrågor {#use-cases-prompts}

Använd innehållsoptimeringsjobbet genom att söka efter rätt resurser via innehållsidentifieringsjobbet [.](/help/ai-in-aem/agents/content-advisor/discovery.md) När de relevanta bilderna visas kan användarna generera optimerade eller kanalspecifika varianter för en eller flera resurser direkt från sökresultatet. Detta arbetsflöde ger högkvalitativa indata och konsekvent bättre optimeringsresultat. [Se den fullständiga listan över tillgängliga optimeringar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) för mer information.

* **Skapa återgivning med hög upplösning**

  Jobbet kan generera nya återgivningar av en mediefil med en angiven upplösning och kvalitetsnivå, vilket gör det enkelt att förbereda kanalklara variationer utan manuell redigering.


  Exempelfråga:

  Skapa en `2000px`-återgivning som `JPEG` med kvaliteten `80%`.

  Sök efter rätt resurs med [innehållsidentifieringsjobbet](/help/ai-in-aem/agents/content-advisor/discovery.md) och använd sedan följande uppmaningar om det finns flera sökresultat:

  För det tredje sökresultatet skapar du en `2000px`-återgivning som `JPEG` med `80%`-kvalitet.

  ELLER

  Generera en 2 000 px-rendering som `Asset ID` med `JPEG` kvalitet för `80%`

* **Bildförbättring**

  Jobbet kan applicera visuella förbättringar, som skärpa, för att säkerställa att materialet ser skarpt och väldefinierat ut innan det används i olika kampanjer.

  Exempelfråga:

  Öka skärpan i bilden.


* **Justeringar för bakgrundsfärg**

  Jobbet kan uppdatera eller ersätta bakgrundsfärger i genomskinliga resurser, vilket stöder varumärkesspecifika färgscheman eller kampanjdrivna visuella teman.

  Exempelfråga:

  Ändra bakgrundsfärgen för `PNG` till `#ff8932`.

* **Orienteringsomformningar**

  Jobbet kan vända eller spegla bilder för att passa in layoutbehoven eller den kreativa riktningen, utan att externa redigeringsverktyg behövs.

  Exempelfråga:

  Spegla bilden vågrätt.

* **Kanaloptimerade återgivningar**

  Jobbet kan producera renderingar som är anpassade efter plattformsspecifika krav - som Instagram Stories - och säkerställa att materialet automatiskt uppfyller format, proportioner och kvalitetskrav.

  Exempelfråga:

  Skapa en återgivning för en `Instagram`-artikel.

* **Varumärkesövertäckningar och sammansatt generering**

  Jobbet kan lägga in kampanjgrafik, överlägg eller emblem i befintligt material med exakt placering, vilket gör det möjligt att snabbt skapa kampanjfärdiga montage.

  Exempelfråga:

  Täck över bilden med `30%` rabattbilder över kampanjbanderollen och placera den `100px` från mitten.

  >[!NOTE]
  >
  >Övertäckningspositionerna kanske inte är korrekta.


## Optimeringsresultat {#content-optimization-job-results}

När du anger en optimeringsprompt returnerar innehållsoptimeringsjobbet den förbättrade resursen tillsammans med praktiska åtkomstalternativ som baseras på resurstypen:

* **Bilder**: Svaret innehåller en miniatyrförhandsvisning och alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade bilden.

* **PDF-dokument**: Svaret innehåller en miniatyrförhandsvisning och alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade filen.

* **Videor**: Svaret innehåller alternativ för att öppna URL:en för dynamiska media eller hämta den optimerade videon.

![Resultat av innehållsoptimering](/help/ai-in-aem/agents/content-advisor/assets/download-content-optimization.png)

Resultatet gör det enkelt att granska det optimerade resultatet och omedelbart använda det i efterföljande kanaler eller arbetsflöden.


## Begränsningar {#limitations-content-optimization}

* Det går inte att ange bakgrundsfärg.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-job}

The following are some prompting best practices:

* Be explicit about the enhancement you want the content optimization job to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->

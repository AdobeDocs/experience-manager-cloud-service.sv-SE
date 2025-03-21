---
title: Metadatahantering och bästa praxis
description: Lär dig mer om metadata och de effektivaste strategierna för att hantera digitala resurser.
role: User, Admin
exl-id: d90519df-55a6-4e23-81ad-ff2365d71c0d
feature: Metadata, Best Practices
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 0%

---

<!-- Keywords to focus on:
metadata best practices
aem metadata 
experience manager metadata-->

# Metadatahantering och bästa praxis {#metadata-best-practices}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

För att få ert företag att sticka ut och engagera fler kunder är det avgörande att ni använder högkvalitativa bilder, videor och andra digitala resurser. För att uppnå detta behöver ni en process där ni kan lägga till metadata i alla digitala resurser, så att de blir enkelt sökbara. Metadata är de data som innehåller viktig information om digitala resurser, inklusive resursens namn, typ, plats i en databas, ändringsdatum och associerade taggar. Metadata effektiviserar resurshanteringen, förbättrar sökbarheten och tillgängligheten samt säkerställer effektiv versionskontroll.

Lär dig hur du använder metadata i DAM-systemet (Digital Asset Management) för att effektivt [hantera metadata för dina digitala resurser](manage-metadata.md).

## Typer av metadata

Baserat på de olika aspekterna av data kategoriseras metadata som tekniska metadata, informativa metadata och administrativa metadata.

### Tekniska metadata

Tekniska metadata omfattar de tekniska aspekterna av en tillgång. Denna typ av metadata är avgörande för att användarna ska förstå de inneboende egenskaperna hos digitala resurser, vilket underlättar effektiv bearbetning och användning.
Den innehåller information om exempelvis:

* Filstorlek
* Format
* Upplösning
* Dimensioner
* Färgläge

### Informativa metadata

Informativa metadata innehåller beskrivande information som förbättrar förståelsen av en tillgångs innehåll. Metadata är viktiga när det gäller att hitta innehåll, söka och förstå resursens betydelse. Informativa metadata innehåller nyckelord, bildtexter och beskrivningar.

Om du till exempel hanterar en video i Experience Manager Assets kan vi inkludera följande informationsmetadata:

* **Nyckelord**: Marknadsföring, Produktstart, Promo
* **Bildtext**: Vi presenterar vår senaste produkt med spännande funktioner
* **Beskrivning**: En detaljerad översikt över videoinnehållet.

Användare som söker efter marknadsrelaterat innehåll kan enkelt hitta och förstå betydelsen av videon ovan.

### Administrativa metadata

Administrativa metadata hanterar de administrativa aspekterna av digitala resurser. Det säkerställer åtkomstkontroll, regelefterlevnad och hantering av den övergripande livscykeln för resurser inom det digitala resurshanteringssystemet. Den innehåller information om

* Tillgångsägare
* Användningsrättigheter
* Behörigheter
* Annan administrativ information

Administrativa metadata säkerställer korrekt resurshantering, kontroll av åtkomst och efterlevnad inom det digitala resurshanteringssystemet.

## Metadata best practices

### Definiera er metadatastrategi från början

Metadatahantering börjar med att definiera en metadatastrategi som ger en grund att bedöma det långsiktiga värdet.

Det är viktigt att du skapar ett anpassat metadatamatchema utifrån dina behov när du planerar en metadatastrategi. Ett väldesignat schema ger ett strukturerat ramverk för kategorisering och sortering av resurser inom Experience Manager.

#### Video: Lägg till anpassade fält i metadatarammet

>[!VIDEO](https://video.tv.adobe.com/v/3425977)

Din metadatastrategi kan innehålla följande:

* **Mål:** Beskriv tydligt mål och förväntade resultat för metadata. Identifiera vad du vill uppnå genom att lägga till metadata.

* **Syfte:** Definiera varför du hämtar metadata. Ange det värde som läggs till i processerna, systemen eller organisationen.

* **Hjälpmedelsplan:** Skapa en plan för att göra metadata lättillgängliga och identifierbara. Förklara vem som kommer att använda den och vilka verktyg och metoder som ska användas.

* **Metadataegenskaper:** Identifiera och definiera varje metadataegenskap noggrant. Se till att varje egenskap har en tydlig anledning att inkluderas, som är kopplad till målen och syftet.

Planera strategin noggrant för att säkerställa enhetliga resultat i hela databasen. Läs mer om [metadatamatcheman](metadata-schemas.md).

### Skapa en metadatastyrningsplan

Datastyrning säkerställer att organisationens metadatahantering är anpassad efter de övergripande affärsmålen.
Styrningsstrategin kan omfatta följande:

* Fastställa policyer och procedurer för hantering av data och metadata.
* Ställa in standarder för datakvalitet och integritet.
* Definiera roller och ansvarsområden inom datahantering.

Bestäm var informationen kommer från och granska detaljerna i metadatastrategin, inklusive egenskaperna och deras källor. Den kan skalas upp beroende på hur komplicerad strategin är. I större företag finns det ett system för hantering av metadata i master-stacken som övervakar flera system.

>[!NOTE]
>
>Lär dig hur du [hanterar metadata för dina digitala resurser](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html).

### Var konsekvent med metadatastrategin

En konsekvent metadatastrategi säkerställer effektiv organisation och hämtning av digitala resurser. Använd en strategisk strategi för att hämta in och implementera metadatavärden, vilket ger flexibilitet att utveckla utan onödiga ändringar. <br>

Vid namngivning och referering av resurser är det viktigt med konsekvent hantering av metadata i hela företaget. Om du till exempel hanterar flera resurser samtidigt bör du&quot;överväga att lägga till flera metadata samtidigt. <br>

Här är några av de bästa sätten att följa:

* **Undvik dubblettvärden:** Om du har en samling bilder från en marknadsföringskampanj bör du använda konsekventa namn och undvika dubbletter.<br>
I stället för att använda dubblettnamn som *campaign_image_001* och *campaign_image_002* kan du implementera en systematisk namnkonvention som *event_promotion* och *product_launch* för att säkerställa en tydlig och ordnad identifiering.

* **Använd kontrollerade vokabulärer effektivt:** Implementera kontrollerade vokabulärer genom att använda standardiserade termer för taggar. Lär dig hur du implementerar [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md) effektivt.  <br>
Använd till exempel termer som *product_launch* eller *event_Promotion* konsekvent när du taggar bilder med teman för att bibehålla en systematisk sekvens.

* **Bevara noggrannhet och fullständighet:** Det är viktigt att alla metadata är konsekventa, exakta, fullständiga och justerade mellan olika källor.
Om du till exempel lägger till metadata i ett PDF-dokument bör du kontrollera att information som författarnamn och nyckelord är korrekta och fullständiga.

#### Video: Lägga till massmetadata i resurser

>[!VIDEO](https://video.tv.adobe.com/v/3425978)

### Utvärdera och förbättra sökbarheten för metadata

Utvärdera er metadatastrategi för att förbättra sökbarheten för metadata. Förenkla arbetsflödena och förbättra sökfunktionerna för effektiv återanvändning. Undvik att hantera metadata som saknar ett tydligt syfte.

Du kan använda följande metodtips för att optimera sökbarheten för metadata:

* **Optimering av nyckelord:** Förbättra sökbarheten för metadata genom att optimera nyckelord som är associerade med resurser. Du kan förbättra nyckelordens relevans för vissa resurser i [!UICONTROL Assets Manager] genom att följa dessa steg:

   1. Gå till **[!UICONTROL Assets]** > **[!UICONTROL File]** > **[!UICONTROL [Asset folder]]**.
   1. Markera resursen som du vill uppdatera metadata för och klicka sedan på **[!UICONTROL Properties]**.
   1. Navigera till fliken **[!UICONTROL Advanced]** och klicka sedan på **[!UICONTROL Add]** under **[!UICONTROL Elevate for search keywords]**. <br>Du måste använda standardmetadataschemat för att höja söknyckelorden.
   1. Ange nyckelordet som du vill utöka sökningen för och klicka sedan på **[!UICONTROL Add]**.<br>
Du kan lägga till flera nyckelord och ordna dem efter din prioritet.
   1. Klicka på **[!UICONTROL Save & Close]**.
Sök efter resursen med de nyckelord du har lagt till. Resursen visas bland de översta sökresultaten.

  Lär dig hur du [förbättrar sökningen i Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

* **Anpassade metadatafält:** Anpassa metadatafälten för att hämta ytterligare information om resurser. Du kan till exempel lägga till specifika fält för projektinformation, copyrightinformation eller andra relevanta data som förbättrar sökfunktionerna. Lär dig [att redigera eller lägga till anpassade metadata](meta-edit.md) i Experience Manager Assets.


* **Metadatavalidering:** Implementera valideringskontroller för metadataposter för att säkerställa konsekvens och precision. Genom att använda kontrollerade vokabulärer blir valideringsprocessen smidigare och minskar risken för otydliga eller inkonsekventa poster. Detta kan innebära att du ställer in riktlinjer för vissa metadataegenskaper för att undvika tvetydig eller inkonsekvent information.

* **Användningsspårning:** Utvärderar relevansen och användningen av olika metadataegenskaper över tid. Identifiera och prioritera ofta använda metadata eller bidra avsevärt till söknings- och hämtningsprocesser.

#### Video: Förbättra sökbarheten genom att lägga till nyckelord

>[!VIDEO](https://video.tv.adobe.com/v/3425979)

### Enkelt och lättbegripligt att använda metadata

Förenkla metadata för bättre styrning och ökad användning av användarna. Se till att informationen är enkel och lättbegriplig och uppmuntrar användarna att lägga till viktig information.
Prova följande metodtips för att förenkla metadata:

* **Optimera egenskapsalternativ:** Fokusera på att markera viktiga egenskaper utan att belasta användarna med för många metadatafält för att fylla i dem. När du till exempel lägger till metadata för en bild ska du bara ta med nyckelfält som titel, beskrivning och taggar för effektiv kategorisering.

* **Ta bort onödiga standardegenskaper:** Förenkla metadataformuläret genom att ta bort standardegenskaper som inte är relevanta för ditt användningsfall. Ta bort sällan använda standardegenskaper för ett renare gränssnitt och en renare upplevelse.

* **Granska och uppdatera metadata regelbundet:** Uppdatera metadata regelbundet och anpassa till förändrade behov och tekniker för att se till att användarna tillhandahåller värdefull information över tid.

### Analysera innehållsresan

Undersök innehållsförsörjningskedjan för att hitta metadatakällor och engagera alla intressenter, från början till slut, för att få en grundlig strategi för bästa praxis. Involvera olika medarbetare för att säkerställa fullständigt stöd i hela organisationen. <br>Inkludera metadata i olika faser för att dela ansvaret för att tillhandahålla tillgångsinformation vid överföring. Att integrera [!DNL Experience Manager Assets] och [!DNL Workfront] ger till exempel avsevärda fördelar när det gäller metadatahantering, vilket förbättrar effektiviteten och samarbetet när det gäller att skapa och hantera innehåll. Den här integreringen säkerställer effektiv synkronisering av metadata för länkade resurser, och uppdaterar automatiskt projektinformationen när ändringar görs i [!DNL Workfront].

informera om mål, framsteg, milstolpar och utmaningar tidigt för att få synpunkter och samarbete från alla intressenter. Uppmuntra samarbete i hela organisationen för att skapa effektiva processer och värdefulla metadata.

Läs mer om [metadata och relaterade koncept](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-concepts.html) för att effektivt hantera dina Experience Manager-metadata.

---
title: Använd Content Advisor för att få åtkomst till AEM-material i Adobe-program
description: Content Advisor ger en enhetlig upplevelse av innehållsidentifiering i olika Adobe-program och ger intelligent, kontextmedveten identifiering direkt i redigeringsmiljön.
badgeSaas: label="AEM Assets" type="Positive" tooltip="Gäller AEM Assets)."
feature: Collaboration
role: User
source-git-commit: 76bdd819634e170a1012cea5ec9f480f17db5130
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 0%

---

# Använd Content Advisor för att få åtkomst till AEM-innehåll i Adobe-program{#content-advisor-aem-assets-adobe-applications}

Content Advisor ger en enhetlig upplevelse för innehållsidentifiering i olika Adobe-program. Content Advisor är inbyggt i program som Adobe Workfront (kommer snart), AJO B2C (kommer snart), AEM Sites med flera, och sammanför innehåll (resurser och innehållsfragment) i ett enda intelligent gränssnitt. Det gör att du enkelt kan hitta, bläddra bland och återanvända det mest relevanta innehållet, direkt i arbetsflödet, så att du kan gå snabbare utan att tappa sammanhanget.

>[!IMPORTANT]
> 
> Content Fragment-piller är för närvarande inte tillgängligt och kommer snart att stödjas för lämpliga Adobe-program.

Med Content Advisor får du en smart, sammanhangsberoende identifiering direkt i redigeringsmiljön, vilket hjälper dig att snabbt hitta relevant, godkänt innehåll baserat på dina avsikter. Med funktioner som smarta förslag, dynamiska medieåtergivningar och detaljerade metadata kan ni effektivt utvärdera och återanvända innehåll utan att lämna programgränssnittet, vilket snabbar upp framtagningen av innehåll samtidigt som varumärkets enhetlighet upprätthålls.

![Banderollbild för Content Advisor](assets/content-advisor-banner-image-updated.png)


## Förutsättningar {#prerequisites}

* Tillgång till AEM Assets as a Cloud Service.

* Tillgång till en AEM Sites-miljö där du har skapat innehållsfragment.

## Intelligent resursidentifiering med Content Advisor {#intelligent-asset-discovery-content-advisor}

Content Advisor hjälper er att identifiera relevant innehåll med hjälp av intelligenta, kontextmedvetna rekommendationer som baseras på ert Adobe-innehåll eller kampanjsammanfattningar. Du kan också välja kanalklara dynamiska medierenderingar som är optimerade för ditt användningssätt.

>[!IMPORTANT]
> 
>Se till att du väljer en **författardatabas** i listrutan **Databas** . En **leveransdatabas** visar inte Content Advisor-funktioner.
>
> Dessutom har databasen **delivery** inget innehåll organiserat i mappar och samlingar. Innehållet visas på rotnivån i en platt struktur.

Content Advisor innehåller följande viktiga funktioner:

* [AI-sökning för smartare tillgångsidentifiering](#content-advisor-ai-search)

* [Smarta förslag baserade på sammanhang och avsikter](#smart-suggestions-content-advisor)

* [Kampanjgenomgångar för att identifiera relevanta resurser](#campaign-briefs-content-advisor)

* [Dynamiska medierenderingar finns tillgängliga för användning](#dynamic-media-renditions-content-advisor)

* [Smidig integrering med Content Fragments](#content-fragments-integration-content-advisor)

* [Få åtkomst till metadata för resurser i enlighet med Assets-vyn](#asset-metadata-content-advisor)

* [Åtkomstfilter som överensstämmer med Assets-vyn](#filters-content-advisor)

* [Få åtkomst till och återanvända senaste och sparade sökningar](#saved-searches-content-advisor)

* [Sök efter resurser i och mellan samlingar](#search-collections-content-advisor)

### AI-sökning för smartare tillgångsidentifiering {#content-advisor-ai-search}

Content Advisor använder en avancerad sökfunktion som förstår innebörden och avsikten bakom en användarfråga i stället för att förlita sig på exakta nyckelordsmatchningar. Det använder artificiell intelligens (AI) och maskininlärning för att leverera mer korrekta och kontextmedvetna resultat.

Till skillnad från traditionell nyckelordsbaserad sökning, som söker efter exakta termer, tolkas relationerna mellan ord, begrepp och användarmetod i AI Search. Detta gör att användarna hittar det de söker efter, även om deras fråga är formulerad på ett annat sätt, innehåller stavfel eller är på ett annat språk.

![AI-sökning efter resurser i Content Advisor](assets/content-advisor-ai-search.png)

Några av fördelarna med den:

* Flerspråksstöd: Sök på flera språk utan exakta översättningar. Användarna kan hitta relevant innehåll oavsett frågespråk.

* Hantera felstavningar: Tolkar stavfel och stavfel, vilket ger korrekta resultat även om de inte är perfekta.

* Förstå synonymer: Ger resultat för relaterade termer och fraser, så användarna behöver inte gissa rätt nyckelord.

* Kontextmedveten sökning: Identifierar avsikten bakom en fråga, inte bara de exakta orden.

>[!IMPORTANT]
> 
>* Den lägsta version av AEM som krävs för att komma åt AI-sökning i Content Advisor är `21994`
>* Stöd för AI-sökning kommer snart för innehållsfragment.


### Smarta förslag baserade på sammanhang och avsikter {#smart-suggestions-content-advisor}

Content Advisor visar smarta förslag baserat på kontexten för Adobe-värdprogrammet. Detta hjälper er att snabbt identifiera och använda resurser som är anpassade till era innehållsbehov utan den tidskrävande manuella sökningen.

![Föreslaget innehåll för Content Advisor](assets/content-advisor-smart-suggestions.png)

>[!IMPORTANT]
> 
>* Du måste signera en GenAI-version för att komma åt den här funktionen i Content Advisor. Kontakta din Adobe-representant om du vill signera GenAI-version.
>* Den lägsta version av AEM som krävs för att få tillgång till den här funktionen är `21994`.
>* Content Advisor visar smarta förslag baserat på kontexten och avsikten med det innehåll som är tillgängligt i Adobe-värdprogrammet. Resultat baserade på bilder visas inte. Se [Funktionsstöd för Content Advisor i olika Adobe-program](#content-advisor-feature-support-adobe-applications) för en lista över Adobe-program som stöds och som stöder den här funktionen.


### Kampanjgenomgångar för att identifiera relevanta resurser {#campaign-briefs-content-advisor}

Med Content Advisor kan du ladda upp ett kampanjdokument för att upptäcka relevanta resurser utan att behöva ange söknyckelord manuellt. Content Advisor analyserar informationen i kampanjöversikten för att förstå kampanjens avsikt och rekommenderar relevanta resurser som är tillgängliga i AEM Assets.

![Inkludera resurser från Assets-tillägg](assets/content-advisor-upload-briefs.png)

>[!IMPORTANT]
>
>* Content Advisor analyserar informationen som är tillgänglig som text i kampanjöversikten för att rekommendera relevanta resurser. Den analyserar inte den information som finns som bilder i kampanjöversikten.
>* De filtyper som stöds och som du kan överföra som en kampanjrapport är bland annat PDF-, DOCX- och TXT-dokument.
>* Du måste signera en GenAI-version för att komma åt den här funktionen i Content Advisor. Kontakta din Adobe-representant om du vill signera GenAI-version.
>* Den lägsta version av AEM som krävs för att få tillgång till den här funktionen är `21994`.
>* Kortfattad support för Upload Campaign kommer snart för innehållsfragment.

### Dynamiska medierenderingar finns tillgängliga för användning {#dynamic-media-renditions-content-advisor}

Dynamiska mediaåtergivningar innehåller färdiga, kanaloptimerade versioner av resurser, inklusive [bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md), [smarta beskärningar](/help/assets/dynamic-media/image-profiles.md), formattyper och färgprofiler. Dessa renderingar säkerställer att den valda resursen uppfyller kraven på kanaler och design utan manuell redigering eller duplicering av resurser.

Du kan också använda modifierare för Dynamic Media för att förhandsgranska justeringar i realtid innan du väljer återgivningen för Adobe-värdprogrammet, vilket ger ett snabbare val av den lämpligaste återgivningen samtidigt som enhetlighet och kvalitet bevaras.

Klicka på ikonen ![Info](assets/info-icon.svg) på resurskortet och välj fliken **[!UICONTROL Dynamic Media]** för att visa tillgängliga återgivningar för en resurs. Du kan välja att visa [Dynamic Media Scene7](/help/assets/dynamic-media/dynamic-media.md)-renderingar eller [Dynamic Media med OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)-renderingar. När du väljer **[!UICONTROL OpenAPI]** för en resurs visas endast tillgängliga återgivningar om resursen har godkänts och är tillgänglig för Dynamic Media med OpenAPI.

Du måste ha en giltig licens för AEM Dynamic Media för att kunna visa fliken Dynamic Media.

![Visa dynamiska medieåtergivningar](assets/content-advisor-dm-renditions.png)

Klicka på ikonen för ![förhandsgranskning](assets/do-not-localize/preview-icon.svg) om du vill förhandsgranska återgivningen eller klicka på återgivningsnamnet och sedan på **[!UICONTROL Select]** om du vill göra återgivningen tillgänglig i värdprogrammet.

![Förhandsgranska dynamiska medierenderingar](assets/content-advisor-dm-preview.png)

Klicka på **[!UICONTROL Add Modifiers]**, ange en modifierare i textrutan och tryck på Retur för att använda omvandlingen på alla resursåtergivningar i realtid. På samma sätt kan du lägga till flera modifierare för återgivningar och förhandsgranska dessa omformningar. Klicka på återgivningsnamnet och klicka på **[!UICONTROL Select]** för att göra återgivningen tillgänglig i värdprogrammet. Återgivningen efter att dessa modifierare har använts sparas inte. Se listan över modifierare som stöds för [Dynamic Media Scene7](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference) och [Dynamic Media med OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat).

### Identifiering av innehållsfragment {#content-fragments-discovery-content-advisor}

Med Content Advisor kan du identifiera innehållsfragment så att du enkelt kan bläddra bland och införliva fragment i Adobe-program som stöds. Sök igenom en lista med innehållsfragment och välj det mest relevanta innehållet utan att lämna det aktuella arbetsflödet.

Varje Content Fragment representeras som ett kort med en förhandsvisning av en live-miniatyrbild som genereras av innehållet, vilket hjälper dig att snabbt identifiera rätt fragment. Kortet visar även viktig information, t.ex. titel och status (Utkast, Ändrad eller Publicerad). Om du vill ha mer information klickar du på ikonen ![Info](assets/info-icon.svg) för att visa detaljerade egenskaper, referenser till andra innehållsfragment och tillgängliga varianter, och på så sätt se till att innehållet markeras och återanvänds.

![Innehållsfragment i Content Advisor](assets/content-advisor-content-fragments.png)

>[!IMPORTANT]
> 
>* Funktionerna AI-sökning, Smarta förslag, Överför kampanjsammanfattningar och Förhandsgranska stöds ännu inte för innehållsfragment i Content Advisor.

### Få åtkomst till metadata för resurser i enlighet med Assets-vyn {#asset-metadata-content-advisor}

Content Advisor ger åtkomst till resursegenskaper som definieras i AEM Assets, inklusive metadata som är tillgängliga i Assets-vyn. Content Advisor använder samma metadatakonfiguration som i Assets View, vilket replikerar listan med metadataflikar och innehåll på sidan med information om Assets-resurser. På så sätt kan du granska viktig resursinformation som titel, beskrivning, format, storlek och andra metadata innan du väljer en resurs. Åtkomst till resursegenskaper hjälper dig att välja rätt och godkänd resurs för ditt innehåll.

![Assets visa metadata i Content Advisor](assets/content-advisor-metadata.png)

Klicka på ikonen ![Information](assets/info-icon.svg) på resurskortet och välj fliken **[!UICONTROL Basic]** för att visa metadata för resursen. Du kan även visa andra metadata för resurser, till exempel Produkt, Kampanj och Taggar, i enlighet med metadata för resursen som finns i Assets-vyn.

Content Advisor visar egenskaper (metadata) för filer i en skrivskyddad vy. Egenskaperna visas inte för samlingar och mappar.

### Åtkomstfilter som överensstämmer med Assets-vyn {#filters-content-advisor}

Content Advisor har samma filtreringsfunktioner i ditt Adobe-värdprogram som finns i Assets-vyn, vilket gör att du kan förfina resurser med fördefinierade filter. Samma filtreringsfunktioner som finns i Assets-vyn gäller också för filter som är specifika för innehållstyper som filer, mappar och samlingar. Detta ger en konsekvent upplevelse av tillgångsidentifiering och hjälper dig att effektivt hitta relevanta resurser i ditt Adobe-värdprogram.

Om du inte har ställt in filter i Assets-vyn via filterschema, visar Content Advisor färdiga filter som filtyp, Filformat, Resursstatus, Filstorlek, Bildbredd, Bildhöjd, Ändringsdatum och Skapat den.

Anpassat filterschema stöds för Assets (filer), men ännu inte för Mappar och samlingar.

### Få åtkomst till och återanvända senaste och sparade sökningar {#saved-searches-content-advisor}

Sparade sökningar som har skapats i Assets-vyn är också tillgängliga, vilket gör att du kan återanvända fördefinierade sökvillkor. Sparade sökningar fungerar på samma sätt i Assets-vyn och Content Advisor i olika webbläsare. På så sätt kan du effektivt hitta resurser med hjälp av enhetliga sökmönster i AEM Assets och andra Adobe-program.

Så här sparar du ofta använda sökningar med hjälp av Content Advisor:

1. Ange en sökterm (valfri), klicka på filterikonen och välj alternativ baserat på dina krav för att skapa en sökfråga.

1. Klicka på **Hantera sparade sökningar** > **Skapa ny sparad sökning**.

1. Ange namnet på sökningen och klicka på ![informationsikonen](assets/do-not-localize/checkmark-icon.svg) för att spara den. Sökningen visas i listan med objekt.

   ![Innehållsrådgivare för sparade sökningar](assets/content-advisor-saved-searches.png)

Om du vill använda något av de sparade sökobjekten väljer du sökobjektet i listrutan **[!UICONTROL Saved Searches]**. Content Advisor visar resultatet baserat på sökfrågan.

Content Advisor sparar dina senaste sökningar och gör det även möjligt att spara sökningar som du använder ofta för snabb åtkomst senare. Listan över de senaste sökningarna är inte konsekvent mellan Assets-vyn och Content Advisor. Samma användare kan ha olika uppsättningar av senaste sökningar i Assets-vyn och Content Advisor. Om du använder Incognito-läget för att komma åt Content Advisor är listan med senaste sökningar inte tillgänglig. Dessutom delas inte de senaste sökningarna mellan olika webbläsare för samma användare, utan sökningen är miljöspecifik för AEM.



Standardfunktionen för sparad sökning, som är tillgänglig i Assets-vyn, är inte tillgänglig än i Content Advisor.

### Sök efter resurser i och mellan samlingar {#search-collections-content-advisor}

Med Content Advisor kan du söka efter resurser eller samlingar i alla samlingar eller begränsa sökningen till en viss samling. På så sätt kan du snabbt hitta och använda resurser från välstrukturerade samlingar samtidigt som du bevarar deras avsedda organisationssammanhang.

## Funktionsstöd för Content Advisor i olika Adobe-program {#content-advisor-feature-support-adobe-applications}

Följande tabell visar hur Content Advisor fungerar i olika Adobe-program.

>[!IMPORTANT]
> 
> När Content Advisor utökas till ytterligare Adobe-program uppdateras den här tabellen med det senaste stödet.

| Program | Stöd för kortfattad överföring för sökning i Assets | Stöd för den föreslagna innehållspanelen när du söker i Assets | Stöd för Dynamic Media-panelen när du söker i Assets | Stöd för sökning av innehållsfragment |
|--------------------------------------|----------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------|------------------------------------------|
| AEM Sites (dokumentbaserad redigering) | ✓ | - | ✓ | - |
| AEM Sites (Document Authoring) | ✓ | ✓ | ✓ | - |
| AEM Sites (Content Fragment Editor) | ✓ | ✓ | ✓ | - |
| AEM Sites (Universal Editor) | ✓ | ✓ | ✓ | - |


---
title: Creating Accessible Content for Adobe Experience Manager as a Cloud Service (WCAG 2.1-överensstämmelse)
description: Använd AEM som Cloud Service för att göra webbinnehåll tillgängligt för och användbart för personer med funktionshinder
translation-type: tm+mt
source-git-commit: 9b52d37a5af866dfb1bce6ee18b524a0f6ede19e
workflow-type: tm+mt
source-wordcount: '14060'
ht-degree: 5%

---


# Skapa tillgängligt innehåll (WCAG 2.1-överensstämmelse) {#creating-accessible-content-wcag-conformance}

WCAG ( [Web Content Accessibility Guidelines) 2.1](https://www.w3.org/TR/WCAG/), som utarbetats av [en arbetsgrupp inom World Wide Wec Consortium](https://www.w3.org/Consortium/actions#Accessibility_guidelines_working_group), består av en uppsättning teknikoberoende riktlinjer och framgångskriterier som gör webbinnehåll tillgängligt för och användbart för personer med funktionshinder.

Som en introduktion tillhandahåller konsortiet en serie sektioner och styrkande dokument:

* [Nya funktioner i WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Så här uppfyller du WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Understanding WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Techniques for WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG-dokument](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Se även:

* Our [Quick Guide to WCAG 2.1](/help/onboarding/accessibility/quick-guide-wcag.md).
* The [Accessibility Conformance reports for Adobe solutions](https://www.adobe.com/accessibility/compliance.html).
* [Tillgänglighet i resurser](/help/assets/accessibility.md)
* [Konfigurera RTF-redigeraren för att skapa tillgängligt innehåll](/help/implementing/developing/extending/rte-accessible-content.md)

Riktlinjerna är indelade i tre överensstämmelsenivåer: Nivå A (lägst), Nivå AA och Nivå AAA (högst). Nivåerna definieras kortfattat enligt följande:

* **Nivå A:** Webbplatsen har en grundläggande, lägsta tillgänglighetsnivå. För att den här nivån ska uppnås måste alla kriterier på nivå A uppfyllas.
* **Nivå AA:** Detta är en idealisk nivå av hjälpmedel att eftersträva, där din webbplats når en grundläggande nivå av tillgänglighet, så att den är tillgänglig för de flesta människor i de flesta situationer som använder de flesta tekniker. För att den här nivån ska uppnås måste alla kriterier nivå A och nivå AA uppfyllas.
* **Nivå AAA:** Webbplatsen har mycket hög tillgänglighet. För att den här nivån ska uppnås måste alla kriterier på nivå A, nivå AA och nivå AAA uppfyllas.

När du skapar din webbplats bör du bestämma den övergripande nivån som du vill att din plats ska anpassas efter.

I följande avsnitt visas [lager i WCAG 2.1-riktlinjerna](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) med relaterade kriterier för att lyckas med nivå A och nivå AA- [överensstämmelsenivåer](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1).

>[!NOTE]
>
>I det här dokumentet använder vi:
>
>* The [short names for the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* Den [numrering som används i WCAG 2.1-riktlinjerna](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) för att underlätta korsreferering med WCAG-webbplatsen.


## Princip 1: Förväntningsbar {#principle-perceivable}

[Princip 1: Perfekt - Information och komponenter i användargränssnittet måste kunna presenteras för användarna på ett sätt som de kan uppfatta.](https://www.w3.org/TR/WCAG/#perceivable)

### Textalternativ (1.1) {#text-alternatives}

[Riktlinje 1.1 Textalternativ: Tillhandahåll textalternativ för allt innehåll som inte är text så att det kan ändras till andra formulär som användarna behöver, till exempel stor utskrift, blindskrift, tal, symboler eller enklare språk.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Innehåll som inte är text (1.1.1) {#non-text-content}

* Villkor för lyckat resultat 1.1.1
* Nivå A
* Innehåll som inte är text: Allt innehåll som inte är text och som visas för användaren har ett textalternativ som har samma syfte, förutom de situationer som anges nedan.

#### Syfte - Innehåll som inte är text (1.1.1) {#purpose-non-text-content}

Information på en webbsida kan tillhandahållas i många olika format som inte är text, till exempel bilder, videor, animeringar, diagram och diagram. Personer som är blinda eller har svårt nedsatt syn kan inte se icke-textbaserat innehåll, men de kan få åtkomst till textinnehåll genom att låta det läsas av skärmläsaren eller presenteras i taktisk form av en blindskriftsvisningsenhet. Genom att tillhandahålla textalternativ för innehåll i grafiskt format kan alltså de som inte kan se det grafiska innehållet få tillgång till en motsvarande version av den information som innehållet ger.

En annan fördel är att textalternativ gör det möjligt att indexera icke-textinnehåll med sökmotorteknik.

#### Så här möts du - innehåll som inte är text (1.1.1) {#how-to-meet-non-text-content}

För statisk grafik är det grundläggande kravet att tillhandahålla ett motsvarande textalternativ för grafiken. Detta kan göras i fältet **Alternativ text** . se t.ex. Core Component **[Image](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html)**.

>[!NOTE]
>
>Vissa färdiga kärnkomponenter, som **[Carousel](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)** , innehåller inte något **alternativt textfält** för att lägga till alternativa textbeskrivningar till enskilda bilder, men det finns ett **etikettfält** (fliken **[Tillgänglighet](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** ) för hela komponenten.
>
>När versioner av dessa implementeras för er AEM-instans måste ert utvecklingsteam konfigurera dessa komponenter så att de stöder attributet `alt`, så att författare kan lägga till det i innehållet (se Lägga till stöd för ytterligare HTML-element och attribut).
>
>Vissa färdiga kärnkomponenter, som **[Carousel](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)** , innehåller inte något **alternativt textfält** för att lägga till alternativa textbeskrivningar till enskilda bilder, men det finns ett **etikettfält** (fliken **[Tillgänglighet](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** ) för hela komponenten.
>
>När versioner av dessa implementeras för er AEM-instans måste ert utvecklingsteam konfigurera dessa komponenter så att de stöder attributet `alt`[, så att författare kan lägga till det i innehållet (se Lägga till stöd för ytterligare HTML-element och attribut](/help/implementing/developing/extending/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

AEM kräver att fältet **Alternativ text** ska fyllas i som standard. Om bilden är enbart dekorativ och alternativ text inte behövs kan alternativet **Bild** vara dekorativ kontrolleras.

#### Skapa bra textalternativ {#creating-good-text-alternatives}

Det finns olika former av innehåll som inte är text, så textalternativets värde beror på vilken roll bilden spelar på webbsidan. Några allmänna regler för tummen som ska följas är:

* Textalternativen bör vara kortfattade men ändå tydligt återge den viktiga information som icke-textinnehållet ger.
* För långa beskrivningar (över 100 tecken) bör undvikas. Om ett textalternativ kräver mer information:
   * ge en kort beskrivning i den alternativa texten
   * och har en längre beskrivning i text på en annan plats på samma sida eller på en separat webbsida. Länka till den här separata beskrivningen genom att göra bilden till en länk eller genom att placera en textlänk bredvid bilden.
* Alternativ text ska inte återge innehåll som finns i textformulär i närheten på samma sida. Kom ihåg att många bilder är illustrationer av punkter som redan finns på en sida, så det kanske redan finns ett detaljerat textalternativ.
* Om innehållet som inte är text är en länk till en annan sida eller ett annat dokument och det inte finns någon annan text som ingår i samma länk, måste den alternativa texten för bilden ange länkens mål, inte bilden.
* Om innehållet som inte är text finns i ett knappelement och det inte finns någon text som tillhör samma knapp, måste den alternativa texten i bilden ange knappens funktion, inte bilden.
* Det går bra att ge en bild en tom (null) alternativ text, men bara om bilden inte behöver någon alternativ text (t.ex. en rent dekorativ bild) eller om motsvarande text redan finns i sidtexten.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Specifika typer av icke-textinnehåll som kräver textalternativ kan vara:

* Illustrativa foton: Det här är bilder på människor, objekt eller platser. Det är viktigt att tänka på fotots roll på sidan och i allmänhet rekommenderas att beskriva bildinnehållet, eftersom hjälpmedelstekniken meddelar elementtypen (till exempel `graphic` eller `image`). det kan göra det klarare att använda `screenshot` eller `illustration` i de alternativa textbeskrivningarna, men detta beror på sammanhanget. Enhetlighet är en stor faktor, ett beslut bör fattas för ett helt redigeringsteam och det ska tillämpas i hela användarupplevelsen.
* Ikoner: Det är små bildspel (grafik) som förmedlar specifik information. De måste användas konsekvent på en sida och en webbplats. Alla förekomster av ikonen på en sida eller på en webbplats bör ha samma korta och koncisa textalternativ, såvida inte detta leder till onödig duplicering av intilliggande text.
* Diagram och diagram: Dessa representerar vanligtvis numeriska data. Ett alternativ för att tillhandahålla ett textalternativ kan vara att ta med en kort sammanfattning av huvudtrenderna som visas i diagrammet eller grafiken. Om det behövs kan du även ge en mer detaljerad beskrivning i texten med hjälp av fältet **Beskrivning** på fliken **Avancerade** bildegenskaper. Dessutom kan du tillhandahålla källdata i tabellformat någon annanstans på sidan eller webbplatsen.
* Kartor, diagram, flödesscheman: För grafik som tillhandahåller spatiala data (till exempel för att ge stöd för att beskriva relationer mellan objekt eller en process) måste du se till att nyckelmeddelandet tillhandahålls i textformat och att textinformationen placeras nära varje associerad datapunkt. För kartor är det troligtvis opraktiskt att ange en fullständig textmotsvarighet, men om kartan tillhandahålls som ett sätt att hjälpa människor att hitta rätt väg till en viss plats, kan kartbildens alternativa text kortfattat ange *karta över X* och sedan ge anvisningar till den platsen i text någon annanstans på sidan eller i fältet **Beskrivning** på fliken **Avancerat** i **bildkomponenten**.
* CAPTCHA: En CAPTCHA är ett *helautomatiserat offentligt kurstest för att skilja på datorer och människor*. Det är en säkerhetskontroll som används på webbsidor för att skilja människor från skadliga program, men som kan orsaka tillgänglighetshinder. Det är bilder som kräver att användarna beskriver vad de ser för att klara ett säkerhetstest. Det är uppenbart att det inte går att ange ett textalternativ för bilden, så du måste istället överväga alternativa icke-grafiska lösningar. W3C ger ett antal förslag, t.ex.: Alla dessa metoder har sina egna fördelar och nackdelar.
   * Logikpussel
   * Användning av ljudutdata i stället för bilder
   * Begränsade användningskonton och skräppostfilter.
* Bakgrundsbilder: Dessa uppnås med CSS (Cascading Style Sheets) i stället för HTML. Det innebär att det inte går att ange ett alternativt textvärde. Därför bör bakgrundsbilder inte innehålla viktig textinformation - om de gör det måste den informationen också anges i sidans text. Det är dock viktigt att en alternativ bakgrund visas när bilden inte kan visas.

>[!NOTE]
>
>Det bör finnas en lämplig kontrastnivå mellan bakgrunden och förgrundstexten. Detta beskrivs närmare i [Kontrast (minimum) (1.4.3)](#contrast-minimum).

#### Mer information - Innehåll som inte är text (1.1.1) {#more-information-non-text-content}

* [Förstå villkor 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Så här uppfyller du kriterierna 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [W3C-förklaring och alternativ till CAPTCHA](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Tidsbaserade media (1.2) {#time-based-media}

[Riktlinje 1.2 Tidsbaserade medier: Tillhandahåll alternativ för tidsbaserade medier.](https://www.w3.org/TR/WCAG/#time-based-media)

Detta gäller webbinnehåll som är *tidsbaserat*. Detta omfattar innehåll som användaren kan spela upp (t.ex. video, ljud och animerat innehåll) och som kan spelas in i förväg eller i en liveström.

### Endast ljud och endast video (inspelat i förväg) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Villkor för lyckat resultat 1.2.1
* Nivå A
* Endast ljud och endast video (inspelat i förväg): För förinspelat ljud och förinspelat videomaterial gäller följande, utom när ljudet eller videon är ett mediaalternativ för text och är tydligt märkt som sådan:
   * Endast inspelat ljud: Ett alternativ för tidsbaserade medier tillhandahålls som ger motsvarande information för förinspelat ljudinnehåll.
   * Endast inspelad video: Antingen är ett alternativ för tidsbaserade medier eller ett ljudspår som ger motsvarande information för förinspelat videomaterial.

#### Syfte - Endast ljud och endast video (inspelat i förväg) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Hjälpmedelsproblem för video och ljud kan uppstå om:

* Personer med nedsatt syn när det inte finns något ljudspår eller ljudspåret inte är tillräckligt för att informera dem om vad som händer i videon eller animeringen.
* Personer med nedsatt hörsel eller som är döva och som inte kan höra ljudspåret.
* Personer som kan höra ljudspåret, men som inte förstår vad som talas (till exempel för att det är på ett språk som de inte förstår).

Video eller ljud kan också vara otillgängligt för personer som använder webbläsare eller enheter som inte har stöd för uppspelning av innehåll i vissa medieformat, till exempel Adobe Flash.

Om du anger den här informationen i ett annat format, till exempel text (eller ljud för video utan ljud), kan det göra den tillgänglig för personer som inte kan komma åt det ursprungliga innehållet.

#### Så här möts du - endast ljud och endast video (inspelat i förväg) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Om innehållet spelas in i förväg utan video (till exempel en poddsändning):
   * Ange en länk omedelbart före eller efter innehållet till en textavskrift av ljudinnehållet. transkriberingen ska vara en HTML-sida med en textmotsvarighet till allt tal och viktigt icke-talat innehåll, plus en indikation på vem som talar, en beskrivning av inställningen, röstuttryck och en beskrivning av allt annat viktigt ljud.
* Om innehållet är en animering eller förinspelad video utan ljud:
   * Ange en länk omedelbart före eller efter innehållet till en motsvarande textbeskrivning av informationen som videon innehåller
   * Eller en motsvarande ljudbeskrivning i ett vanligt ljudformat som MP3.

>[!NOTE]
>
>Om ljud- eller videoinnehållet tillhandahålls som ett alternativ till innehåll som redan finns i ett annat format på samma webbsida kanske inget ytterligare alternativ krävs.
>
>Riktlinjerna, [Förstå WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html), innehåller mer information.

Att infoga multimedia i dina AEM webbsidor påminner om att infoga en bild. Men eftersom multimediainnehållet är mycket mer än en stillbild finns det olika inställningar och alternativ för att styra hur multimediainnehållet spelas upp.

>[!NOTE]
>
>När du använder multimedia med informativt innehåll måste du också skapa länkar till alternativ. Om du till exempel vill ta med en textutskrift skapar du en HTML-sida som visar utskriften och lägger sedan till en länk bredvid eller under ljudinnehållet.

#### Mer information - endast ljud och endast video (inspelat i förväg) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Förstå villkor 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Så här uppfyller du kriterierna 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Bildtexter (inspelade i förväg) (1.2.2) {#captions-prerecorded}

* Villkor för lyckat resultat 1.2.2
* Nivå A
* Bildtexter (inspelade i förväg): Bildtexter tillhandahålls för allt förinspelat ljudinnehåll i synkroniserade medier, utom när mediet är ett mediaalternativ för text och är tydligt märkt som sådant.

#### Syfte - Textning (inspelad i förväg) (1.2.2) {#purpose-captions-prerecorded}

Personer som är döva eller hörselskadade kan inte eller har stora svårigheter att komma åt ljudinnehållet. Bildtexter är textmotsvarigheter för tal och icke-tal ljud som visas på skärmen vid lämplig tidpunkt under videon. De gör det möjligt för personer som inte kan höra ljudet att förstå vad som händer.

#### Så här uppfyller du kraven - bildtexter (inspelade i förväg) (1.2.2) {#how-to-meet-captions-prerecorded}

Bildtexter kan antingen vara:

* Öppna: alltid synlig när videon spelas upp
* Stängd: bildtexterna kan aktiveras och inaktiveras av användaren

Använd undertextning där det är möjligt, eftersom det ger användarna möjlighet att välja om de vill visa undertexter eller inte.

För undertexter måste du skapa och tillhandahålla en synkroniserad bildtextfil i ett lämpligt format (till exempel [SMIL](https://www.w3.org/AudioVideo/)) tillsammans med videofilen (information om hur du gör detta ligger utanför handbokens räckvidd, men vi har tillhandahållit länkar till vissa självstudiekurser under [Mer information - Bildtexter (inspelade i förväg) (1.2.2)](#more-information-captions-prerecorded). Se till att du anger en anteckning, eller aktivera bildtextfunktionen i videospelaren, så att användarna vet att bildtexter är tillgängliga för videon.

Om du måste använda öppna bildtexter bäddar du in texten i videospåret. Detta kan du göra med videoredigeringsprogram som tillåter att titlar läggs över i videon.

#### Mer information - bildtexter (inspelade i förväg) (1.2.2) {#more-information-captions-prerecorded}

* [Förstå villkor 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [Så här uppfyller du kriterierna 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Ljudbeskrivning eller mediaalternativ (inspelat i förväg) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Villkor för lyckat resultat 1.2.3
* Nivå A
* Ljudbeskrivning eller mediaalternativ (inspelat i förväg): Ett alternativ för tidsbaserade medier eller ljudbeskrivning av det inspelade videoinnehållet tillhandahålls för synkroniserade medier, utom när mediet är ett mediaalternativ för text och är tydligt märkt som ett sådant.

#### Syfte - Ljudbeskrivning eller mediealternativ (inspelat i förväg) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Personer med nedsatt syn eller nedsatt syn kommer att uppleva tillgänglighetshinder om informationen i en video eller animering endast tillhandahålls visuellt, eller om ljudspåret inte ger tillräcklig information för att förstå vad som händer visuellt.

#### Så här möts - ljudbeskrivning eller mediaalternativ (inspelat i förväg) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Det finns två strategier som kan användas för att uppfylla detta kriterium. Båda är godtagbara:

1. Inkludera ytterligare ljudbeskrivning för videoinnehållet. Detta kan uppnås på ett av tre sätt:
   * Under pauser i den befintliga dialogen, lämna information om förändringar i scenen som inte presenteras som en del av det befintliga ljudspåret.
   * Skapa ett nytt, extra och valfritt ljudspår som innehåller det ursprungliga ljudspåret, men även extra ljudinformation om ändringar i scenen.
      * Detta gör att användare kan växla mellan det befintliga ljudspåret (som *inte* innehåller någon ljudbeskrivning) och det nya ljudspåret (som *inte* innehåller någon ljudbeskrivning).
      * Detta förhindrar avbrott för användare som inte behöver den ytterligare beskrivningen.
   * Skapa en andra version av videoinnehållet som tillåter utökade ljudbeskrivningar. Detta minskar de svårigheter som är förknippade med att tillhandahålla detaljerade ljudbeskrivningar i mellanrummen mellan de befintliga dialogrutorna genom att tillfälligt pausa ljudet och videon vid lämpliga tidpunkter. Därför kan en mycket längre ljudbeskrivning ges innan åtgärden startar om. Precis som i föregående exempel är detta det bästa sättet att tillhandahålla detta som ett extra ljudspår för att förhindra avbrott för användare som inte behöver den extra beskrivningen.
1. Ange en textavskrift som är en lämplig textmotsvarighet till ljud- och visuella element i videon eller animeringen. Detta bör i tillämpliga fall innehålla en uppgift om vem som talar, en beskrivning av inställningen, eventuella händelser eller uppgifter som presenteras visuellt samt röstuttryck. Beroende på längden kan du placera utskriften på samma sida som videon eller animeringen, eller på en separat sida; om du väljer det senare alternativet, anger du en länk till det utskrivna dokumentet som finns intill videon eller animeringen.

Exakta detaljer om hur du skapar ljudbeskrivad video ligger utanför den här handbokens räckvidd. Det kan ta lång tid att skapa videoklipp och ljudbeskrivningar, men med andra Adobe-produkter kan du göra detta.

#### Mer information - Ljudbeskrivning eller mediealternativ (inspelat i förväg) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Förstå villkor 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Så här uppfyller du kriterierna 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Bildtexter (Live) (1.2.4)  {#captions-live}

* Villkor för lyckat resultat 1.2.4
* Nivå AA
* Bildtexter (Live): Bildtexter finns för allt direktsänt ljudinnehåll i synkroniserade medier.

#### Syfte - Textning (live) (1.2.4) {#purpose-captions-live}

Detta kriterium är identiskt med [bildtexter (inspelade i förväg)](#captions-prerecorded) eftersom det åtgärdar tillgänglighetshinder som upplevs av döva eller hörselskadade, förutom att detta kriterium gäller live-presentationer som webbsändningar.

#### Så här fungerar det - bildtexter (Live) (1.2.4) {#how-to-meet-captions-live}

Följ anvisningarna för [bildtexter (inspelat i förväg)](#captions-prerecorded) ovan. På grund av mediernas aktiva natur måste dock bildtexter skapas så snabbt som möjligt och som svar på vad som händer. Därför bör du överväga att använda bildtexter i realtid eller tal-till-text-verktyg.

Detaljerade instruktioner ligger utanför det här dokumentets räckvidd, men med följande resurser får du användbar information:

* [WebAIM: Bildtext i realtid](https://www.webaim.org/techniques/captions/realtime.php)

* [AccessComputing project (University of Washington): Kan bildtexter genereras automatiskt med taligenkänning?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### Mer information - Bildtexter (Live) (1.2.4) {#more-information-captions-live}

* [Förstå villkor 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Så här uppfyller du kriterierna 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Ljudbeskrivning (inspelad i förväg) (1.2.5)  {#audio-description-prerecorded}

* Villkor för lyckat resultat 1.2.5
* Nivå AA
* Ljudbeskrivning (inspelad i förväg): Ljudbeskrivning ges för allt förinspelat videoinnehåll i synkroniserade media.

#### Syfte - ljudbeskrivning (inspelad i förväg) (1.2.5) {#purpose-audio-description-prerecorded}

Detta kriterium är identiskt med [Ljudbeskrivning eller Mediealternativ (inspelat i förväg)](#audio-description-or-media-alternative-prerecorded), förutom att författare måste ange en mycket mer detaljerad ljudbeskrivning för att uppfylla nivå AA.

#### Så här uppfyller du kraven - ljudbeskrivning (inspelad i förväg) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Följ anvisningarna för [Ljudbeskrivning eller Mediealternativ (inspelat i förväg)](#audio-description-or-media-alternative-prerecorded).

#### Mer information - ljudbeskrivning (inspelad i förväg) (1.2.5) {#more-information-audio-description-prerecorded}

* [Förstå villkor 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Så här uppfyller du kriterierna 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Anpassningsbar (1.3) {#adaptable}

[Riktlinje 1.3 Anpassningsbar: Skapa innehåll som kan presenteras på olika sätt (till exempel enklare layout) utan att förlora information eller struktur.](https://www.w3.org/TR/WCAG/#adaptable)

Denna riktlinje omfattar de krav som är nödvändiga för att stödja personer som

* kanske inte kan komma åt information som presenterats av en författare i standardpresentationen av det innehållet (t.ex. en layout med flera kolumner eller en sida där färg och/eller bilder används mycket).

* kan använda enbart ljud eller alternativ visuell visning som stor text eller hög kontrast.

### Information och relationer (1.3.1)  {#info-and-relationships}

* Villkor för lyckat resultat 1.3.1
* Nivå A
* Information och relationer: Information, struktur och relationer som förmedlas genom presentationen kan bestämmas programmatiskt eller vara tillgängliga i text.

#### Syfte - Information och relationer (1.3.1) {#purpose-info-and-relationships}

Många hjälpmedelstekniker som används av personer med funktionshinder är beroende av strukturinformation för att effektivt kunna visa eller *förstå* innehåll. Den här strukturinformationen kan ha formen av sidrubriker, tabellrader, kolumnrubriker och listtyper. En skärmläsare kan till exempel tillåta användaren att navigera på en sida från rubrik till rubrik. Men när sidinnehåll bara verkar ha en struktur genom visuell formatering, i stället för den underliggande HTML-koden, finns det ingen strukturinformation tillgänglig för hjälpmedelstekniker, vilket begränsar deras möjligheter att hantera enklare surfning.

Detta kriterium gäller för att se till att sådan strukturinformation tillhandahålls via HTML, eller andra kodningstekniker, så att webbläsare och hjälpfunktioner kan komma åt och dra nytta av informationen.

#### Hur man möter - Information och relationer (1.3.1) {#how-to-meet-info-and-relationships}

AEM gör det enkelt att skapa semantiskt meningsfullt webbinnehåll med lämpliga HTML-element. Öppna sidinnehållet i textredigeraren (en textkomponent) och använd menyn **Paraformat** (styckesymbol) för att ange lämpligt strukturelement (till exempel stycke, rubrik osv.).

Du kan se till att dina webbsidor får rätt struktur genom att använda följande element där det är tillämpligt:

* **Rubriker:** Så länge du har tillgänglighetsfunktionerna i textredigeraren aktiverade kan AEM erbjuda tre rubriknivåer. Du kan använda dessa för att identifiera avsnitt och underavsnitt för innehåll. Rubrik 1 är den högsta rubriknivån, rubrik 3 den lägsta. Systemadministratören kan konfigurera systemet så att fler rubriknivåer tillåts.

* **Listor**: Du kan använda HTML för att ange tre olika typer av listor:
   * Elementet `<ul>` används för *oordnade* punktlistor. Enskilda listobjekt identifieras med elementet `<li>`. Använd ikonen **Punktlista** i textredigeraren.
   * The `<ol>` element is used for *numbered* lists. Enskilda listobjekt identifieras med hjälp av `<li>` elementet. Använd ikonen **Numrerad lista** i textredigeraren.

   Om du vill ändra befintligt innehåll till en viss listtyp markerar du lämplig text och väljer lämplig listtyp. Precis som i det tidigare exemplet som visar hur stycketext skrivs in, läggs de rätta listelementen automatiskt till i HTML-koden.

   I helskärmsläge visas ikonerna **Punktlista** och **Numrerad lista**. Om du inte arbetar i helskärmsläge finns de två alternativen bakom den enda **Listor**-ikonen.

* **Tabeller**: Datatabeller måste identifieras med HTML-tabellelement:
   * ett `<table>` element
   * ett `<tr>` element för varje rad i tabellen
   * ett element `<th>` för varje rad och kolumnrubrik
   * ett `<td>` element för varje datacell

   Tillgängliga tabeller använder dessutom följande element och attribut:

   * Elementet `<caption>` används för att ge en synlig bildtext för tabellen. Bildtexter visas som standard centrerade ovanför tabellen, men kan placeras korrekt med CSS. Bildtexten är programmatiskt kopplad till tabellen och är därför en användbar metod för att ge en introduktion till innehållet.
   * Elementet gör det enklare för användare som inte är synkade att förstå den information som presenteras i en tabell genom att ge en sammanfattning av vad en synkad användare kan se. `<summary>` Detta är särskilt användbart när komplexa eller okonventionella tabellayouter används (det här attributet visas inte i webbläsaren, det läses bara ut för hjälpfunktioner).
   * Attributet `scope` för `<th>` elementet används för att ange om en cell representerar en rubrik för en viss rad eller för en viss kolumn. Ett liknande sätt är att använda attributen header och id i komplexa tabeller, där dataceller kan kopplas till en eller flera rubriker.

   >[!NOTE]
   >
   >Som standard är dessa element och attribut inte direkt tillgängliga, men systemadministratören kan lägga till stöd för dessa värden i dialogrutan **Tabellegenskaper**[ (se Lägga till stöd för ytterligare HTML-element och attribut](/help/implementing/developing/extending/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

   Så här öppnar du dialogrutan **Tabell** där du kan välja fliken **Tabellegenskaper** :

   * Definiera en lämplig **bildtext**.
   * Ta helst bort alla standardvärden för **Bredd**, **Höjd**, **Kant**, **Cellfyllnad** och **Cellmellanrum** eftersom dessa egenskaper kan anges i en global formatmall.

   Du kan sedan använda **cellegenskaperna** för att välja om cellen är en data- eller rubrikcell:

* **Betoning**: Använd elementet `<strong>` eller `<em>` för att ange betoning. Använd inte rubriker för att markera text i stycken.
   * Markera den text som du vill framhäva;
   * Klicka på ikonen **B** (för `<strong>`) eller ikonen **I** (för `<em>`) som visas på panelen **Egenskaper** (kontrollera att HTML är markerat).

      >[!NOTE]
      >
      >RTE i en AEM standardinstallation är konfigurerad att använda:
      >
      >* `<b>` for `<strong>`
      >* `<i>` for `<em>`

      >
      >De är i princip desamma, men `<strong>` och `<em>` är att föredra eftersom de är semantiskt korrekta i html. Utvecklingsteamet kan konfigurera RTE så att den används `<strong>` och `<em>` (i stället för `<b>` och `<i>`) när du utvecklar projektinstansen.


* **Komplexa datatabeller**: I vissa fall, där det finns komplexa tabeller med två eller flera rubriknivåer, kanske de grundläggande tabellegenskaperna inte räcker för att ge all nödvändig strukturinformation. För den här typen av komplexa tabeller måste direkta relationer skapas mellan rubrikerna och deras relaterade celler med hjälp av attributen **header** och **id.**

   >[!NOTE]
   >
   >Attributet id är inte tillgängligt i en körklar installation. Den kan aktiveras genom att HTML-regler och serialiseraren konfigureras i textredigeraren.

   I tabellen nedan matchas till exempel rubriker och ID:n för att skapa en programmatisk association för hjälpmedelsanvändare.

   ```xml
     <table>
       <tr>
         <th rowspan="2" id="h">Homework</th>
         <th colspan="3" id="e">Exams</th>
         <th colspan="3" id="p">Projects</th>
       </tr>
       <tr>
         <th id="e1" headers="e">1</th>
         <th id="e2" headers="e">2</th>
         <th id="ef" headers="e">Final</th>
         <th id="p1" headers="p">1</th>
         <th id="p2" headers="p">2</th>
         <th id="pf" headers="p">Final</th>
       </tr>
       <tr>
         <td headers="h">15%</td>
         <td headers="e e1">15%</td>
         <td headers="e e2">15%</td>
         <td headers="e ef">20%</td>
         <td headers="p p1">10%</td>
         <td headers="p p2">10%</td>
         <td headers="p pf">15%</td>
       </tr>
     </table>
   ```

   För att uppnå detta i AEM måste du lägga till koden direkt i källredigeringsläget.

   >[!NOTE]
   >
   >Den här funktionen är inte omedelbart tillgänglig i en standardinstallation. Den kräver konfiguration av RTE, HTML-regler och serialisering.

#### Mer information - Info och relationer (1.3.1) {#more-information-info-and-relationships}

* [Förstå villkor 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Så här uppfyller du kriterierna för lyckade resultat 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Betydelsefull sekvens (1.3.2)  {#meaningful-sequence}

* Villkor för lyckat resultat 1.3.2
* Nivå A
* Betydelsefull sekvens: När den sekvens i vilken innehållet presenteras påverkar dess betydelse, kan en korrekt lässekvens bestämmas programmatiskt.

#### Syfte - meningsfull sekvens (1.3.2) {#purpose-meaningful-sequence}

Syftet med detta villkor är att en användaragent ska kunna tillhandahålla en alternativ presentation av innehållet samtidigt som läsordningen som behövs för att förstå innebörden bevaras. Det är viktigt att det går att programmässigt avgöra minst en sekvens av innehållet som är lämplig. Innehåll som inte uppfyller detta villkor kan förvirra eller skada användare när hjälpmedelstekniken läser innehållet i fel ordning eller när alternativa formatmallar eller andra formateringsändringar tillämpas.

#### Så här möts du - meningsfull sekvens (1.3.2) {#how-to-meet-meaningful-sequence}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Mer information - meningsfull sekvens (1.3.2) {#more-information-meaningful-sequence}

* [Förstå villkor 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Så här uppfyller du kriterierna 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Sensoriska egenskaper (1.3.3)  {#sensory-characteristics}

* Villkor för lyckat resultat 1.3.3
* Nivå A
* Sensoriska egenskaper: Instruktioner för att förstå och använda innehåll är inte enbart beroende av de sensoriska egenskaperna hos komponenter som form, storlek, visuell placering, orientering eller ljud.

#### Syfte - Sensoriska egenskaper (1.3.3) {#purpose-sensory-characteristics}

Designers fokuserar ofta på visuella designfunktioner som färg, form, textstil eller innehållets absoluta eller relativa position när de presenterar information. Dessa kan vara mycket kraftfulla designtekniker för att förmedla information (och kan förbättra den övergripande tillgängligheten för synskadade med behov av kognitiv hjälpmedel), men personer med nedsatt syn eller blindhet kanske inte har tillgång till information som kräver visuell identifiering av attribut som position, färg eller form.

På samma sätt kommer information som kräver att man skiljer mellan olika ljud (t.ex. manligt eller kvinnligt talt innehåll) att medföra tillgänglighetshinder för personer med nedsatt hörsel, om den inte återspeglas i något textalternativ för ljudinnehållet.

>[!NOTE]
>
>Information om krav för alternativ till färg finns i [Använda färg](#use-of-color).

#### Hur man uppfyller kraven - sensoriska egenskaper (1.3.3) {#how-to-meet-sensory-characteristics}

Se till att all information som bygger på visuella egenskaper för sidinnehåll också presenteras i ett alternativt format.

* Förlita dig inte på visuell position för att ge information. Om du till exempel vill hänvisa användare till en meny till höger på sidan för att få tillgång till mer information, ska du inte hänvisa till *menyn till höger*. I stället ger du menyn ett namn (t.ex. via en rubrik) och refererar till namnet i texten.
* Förlita dig inte på att textformat (t.ex. fet eller kursiv text) är det enda sättet att förmedla information.

>[!NOTE]
>
>Beskrivande termer kan användas om de anses ha betydelse i en icke-visuell kontext. Att använda *ovan* och *nedan* skulle till exempel i allmänhet vara godtagbart eftersom de innebär innehåll före och efter en viss innehållspost. detta skulle fortfarande vara vettigt när innehållet talas högt.

#### Mer information - Sensoriska egenskaper (1.3.3) {#more-information-sensory-characteristics}

* [Förstå villkor 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Så här uppfyller du kriterierna för lyckade resultat 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Skiljbar (1.4) {#distinguishable}

[Riktlinje 1.4 Skiljbar: Gör det enklare för användarna att se och höra innehåll, inklusive att separera förgrunden från bakgrunden.](https://www.w3.org/TR/WCAG/#distinguishable)

### Användning av färg (1.4.1)  {#use-of-color}

* Villkor för lyckat resultat 1.4.1
* Nivå A
* Användning av färg: Färg används inte som det enda visuella sättet att förmedla information, ange en åtgärd, fråga ett svar eller ange ett visuellt element.

>[!NOTE]
>
>Detta kriterium gäller specifikt färguppfattningen. Andra former av uppfattningar omfattas av [adapterbar (1.3)](#adaptable). med programmatisk åtkomst till färg och annan visuell presentationskodning.

#### Syfte - Användning av färg (1.4.1) {#purpose-use-of-color}

Färg är ett uppenbart effektivt sätt att förbättra webbsidornas estetiska utseende och är också användbart för att förmedla information. Det finns dock en rad synstörningar, från blindhet till färgssynsbrist, som innebär att vissa personer inte kan skilja mellan olika färger. Detta gör färgkodning till ett otillförlitligt sätt att tillhandahålla information.

En person med synsbrist i rött-grönt kommer till exempel inte att kunna skilja på nyanser i grönt och röda nyanser. De kan se båda färgerna som en tredje färg (till exempel brunt), och då kan de inte skilja mellan rött, grönt och brunt.

Dessutom kan inte färger uppfattas av personer som använder webbläsare som bara innehåller text, enheter för monokrom visning eller som visar en svartvit utskrift av sidan.

Ett annat sätt att se på detta är det *valda* läget för ett gränssnittselement (t.ex. tabbar, alternativknappar), som måste förmedlas på något annat sätt än bara med färg och inte bara med en visuell presentation. För sådana element är den extra användningen av mönster, former och programmatisk information användbar när du skapar en helomfattande användarupplevelse som inte är beroende av en viss innebörd.

#### Hur man klarar - Färganvändning (1.4.1) {#how-to-meet-use-of-color}

Kontrollera att det finns information om färgen, oavsett var den används för att förmedla information, utan att du behöver se färgen.

Kontrollera till exempel att information som anges av färg också finns explicit i texten.

Om färg används som en referenspunkt för att ge information bör du ange ytterligare en visuell referenspunkt, som att ändra formatet (t.ex. fet, kursiv) eller teckensnitt. Detta hjälper personer med nedsatt syn eller som har nedsatt färgseende att identifiera informationen. Den kan dock inte användas helt eftersom den inte hjälper personer som inte kan se sidan alls. Därför är det (ibland) användbart att tillhandahålla dold text eller att använda programmatiska lösningar, som t.ex. [ARIA (Accessible Rich Internet Applications) för webbstandarder](https://www.w3.org/WAI/standards-guidelines/aria/), för att förmedla denna information till icke-synkade användare.

#### Mer information - Färganvändning (1.4.1) {#more-information-use-of-color}

* [Om villkor för att lyckas 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Så här uppfyller du kriterierna 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Ljudkontroll (1.4.2)  {#audio-control}

* Villkor för lyckat resultat 1.4.2
* Nivå A
* Ljudkontroll: Om något ljud på en webbsida spelas upp automatiskt i mer än 3 sekunder finns det antingen en mekanism som gör att ljudet pausas eller stoppas, eller så finns en mekanism som styr ljudvolymen oberoende av den totala systemvolymnivån.

#### Syfte - Ljudkontroll (1.4.2) {#purpose-audio-control}

Personer som använder skärmläsarprogram kan uppleva att det är svårt att höra talresultatet om det finns annat ljud som spelas upp samtidigt. Svårigheten förvärras om skärmläsarens tal är programbaserat (som de flesta är idag) och styrs via samma volymkontroll som ljudet. Dessutom kan vissa personer med kognitiva handikapp och personer som är neuroavvikande ha ljuskänslighet. De här personerna kommer att upptäcka att det inte går att ändra volymnivån på ljudinnehållet på ett riktigt störande sätt.

Därför är det viktigt att användaren kan stänga av bakgrundsljudet.

>[!NOTE]
>
>Att ha kontroll över volymen innebär bland annat att kunna minska volymen till noll.

#### Hur man klarar - ljudkontroll (1.4.2) {#how-to-meet-audio-control}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Mer information - Ljudkontroll (1.4.2) {#more-information-audio-control}

* [Förstå villkor 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Så här uppfyller du kriterierna 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Kontrast (minimal) (1.4.3) {#contrast-minimum}

* Villkor för lyckat resultat 1.4.3
* Nivå AA
* Kontrast (minimal): Den visuella presentationen av text och bilder av text har ett kontrastförhållande på minst 4,5:1, utom följande:
   * Stor text: Storskalig text och bilder av storskalig text har ett kontrastförhållande på minst 3:1.
   * Oavsiktlig: Text eller bilder av text som är en del av ett inaktivt användargränssnitt, som är [rena dekorationer](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), som inte är synliga för någon eller som är en del av en bild som innehåller annat visuellt innehåll, har inget kontrastkrav.
   * Logotyper: Text som är en del av en logotyp eller ett varumärkesnamn har inget minimikrav på kontrast.

   >[!NOTE]
   >
   >Mer information finns i [Förstå icke-textkontrast](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) , som hjälper dig att se till att innehållsförfattare förstår ytterligare krav runt icke-textelement (inklusive ikoner, gränssnittselement med flera).

#### Syfte - Kontrast (minimum) (1.4.3) {#purpose-contrast-minimum}

Personer med vissa nedsatt syn kanske inte kan skilja mellan vissa färgpar med låg kontrast. Tillgänglighetsproblem kan uppstå för dessa personer om något av följande:

* Texten har dålig kontrast mot bakgrundsfärgen.
* Färgkodningen för text (t.ex. länktext och icke-länktext) är viktig för att kunna skilja information åt.

>[!NOTE]
>
>Text som endast används för dekorationsändamål ingår inte i detta kriterium.

#### Hur man klarar - Kontrast (minimum) (1.4.3) {#how-to-meet-contrast-minimum}

Se till att texten kontrasterar tillräckligt med bakgrunden. Kontrastförhållanden beror på textens storlek och stil:

* För text som är mindre än 18 punkter (eller 14 punkter fet) bör kontrastförhållandet mellan text/bilder i texten och bakgrunden vara minst 4,5:1.
* För text som är minst 18 punkter (eller 14 punkter fet) bör kontrastförhållandet vara minst 3:1.
* Om en bakgrund är mönstrad ska bakgrunden runt all text skuggas så att proportionerna 4.5:1 eller 3:1 behålls.

>[!NOTE]
>
>Tänk på att teckensnitt kan skilja sig åt när det gäller hur de återger motsvarande PT/PX/EM-storlek.
>
>Vi rekommenderar att du använder god vana och felbenägenhet vid läsbarhet och användbarhet när du väljer rätt teckensnitt och anger storlek för webbinnehåll.

>[!NOTE]
>
>Följande sajter kan vara till hjälp vid konvertering till andra enheter:
>
>* [Px to Em Calculater - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [Konvertering av teckenstorlek: pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com: Konvertering från PX till EM på ett enkelt sätt](http://pxtoem.com)


Om du vill kontrollera kontrastförhållanden använder du ett färgkontrastverktyg, till exempel [Pacific Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) eller [WebAIM-färgkontrastkontrollen](https://www.webaim.org/resources/contrastchecker/). Med dessa verktyg kan du kontrollera färgpar och rapportera om eventuella kontrastproblem.

Om du inte är lika orolig för hur sidan ska se ut kan du välja att inte ange färg för bakgrunds- och förgrundstext. Ingen kontrastkontroll krävs eftersom användarens webbläsare bestämmer färgerna för texten och bakgrunden.

Om det inte går att följa de rekommenderade kontrastnivåerna måste du skapa en länk till en alternativ, likvärdig version av sidan (som inte har några färgkontrastproblem) eller låta användaren justera kontrasten i sidfärgschemat efter sina egna behov.

#### Mer information - Kontrast (minimum) (1.4.3) {#more-information-contrast-minimum}

* [Förstå villkor för framgång 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Så här uppfyller du kriterierna för framgång 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Ändra storlek på text (1.4.4)  {#resize-text}

* Villkor för lyckat resultat 1.4.4
* Nivå A
* Ändra storlek på text: Med undantag för bildtexter och bilder av text kan du ändra storlek på texten utan hjälpmedel upp till 200 procent utan att förlora innehåll eller funktioner.

#### Syfte - Ändra textstorlek (1.4.4) {#purpose-resize-text}

Syftet med detta kriterium är att säkerställa att visuellt återgiven text, inklusive textbaserade kontroller (texttecken som har visats så att de kan ses [jämfört med texttecken som fortfarande är i dataformat som t.ex. ASCII]), kan skalas så att de kan läsas direkt av personer med lindriga visuella funktionshinder, utan att hjälpteknik som skärmförstorare behöver användas. Det kan vara bra för användaren att skalförändra allt innehåll på webbsidan, men texten är viktigast.

#### Så här uppfyller du kraven - ändra storlek på text (1.4.4) {#how-to-meet-resize-text}

Förutom att följa riktlinjerna under [How to Meet Success Criteria 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) kan du uppmuntra skribenter att använda flytande, flexibla bredder och höjder i sin siddesign och sina teckenstorlekar (till exempel Responsiv webbdesign) för att ge läsarna möjlighet att ändra storlek på texten.

#### Mer information - Ändra textstorlek (1.4.4) {#more-information-resize-text}

* [Förstå villkor för framgång 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Så här uppfyller du kriterierna 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Bilder av text (1.4.5) {#images-of-text}

* Villkor för lyckat resultat 1.4.5
* Nivå AA
* Bilder av text: Om den teknik som används kan åstadkomma den visuella presentationen, används text för att förmedla information i stället för bilder av text, med undantag för följande:
   * Anpassningsbart: Textbilden kan anpassas visuellt efter användarens behov.
   * Grundläggande: En viss presentation av texten är väsentlig för den information som förmedlas.

>[!NOTE]
>
>Logotyper (text som är en del av en logotyp eller ett varumärkesnamn) anses vara viktiga.

#### Syfte - Textbilder (1.4.5) {#purpose-images-of-text}

Bilder av text används ofta när ett visst textformat är att föredra. t.ex. en logotyp eller om text har genererats från en annan källa (t.ex. en skanning av ett pappersdokument). Jämfört med text i HTML och formaterad med CSS saknar dock bilder av text flexibiliteten att ändra storlek och utseende som kan behövas för personer med nedsatt syn eller läsproblem.

#### Så här möts - bilder av text (1.4.5) {#how-to-meet-images-of-text}

Om bilder av text måste användas, använder du CSS för att ersätta bilder av text med motsvarande text i HTML så att texten blir tillgänglig på ett anpassningsbart sätt. Ett exempel på hur detta kan uppnås finns i [C30: Använda CSS för att ersätta text med bilder av text och tillhandahålla gränssnittskontroller för att växla](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Mer information - Textbilder (1.4.5) {#more-information-images-of-text}

* [Förstå villkor 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Så här uppfyller du kriterierna 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Princip 2: Operativ {#principle-operable}

[Princip 2: Operable - Användargränssnittets komponenter och navigering måste vara operabla.](https://www.w3.org/TR/WCAG/#operable)

### Tangentbord tillgängligt (2.1) {#keyboard-accessible}

[Riktlinje 2.1 Tangentbord tillgängligt: Gör alla funktioner tillgängliga via tangentbordet.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Det handlar om att se till att användarna har tillgång till alla funktioner via ett tangentbord.

### Tangentbord (2.1.1)  {#keyboard}

* Villkor för lyckat resultat 2.1.1
* Nivå A
* Tangentbord: All funktionalitet i innehållet kan utföras via ett tangentbordsgränssnitt utan att särskilda tidsinställningar krävs för enskilda tangenttryckningar, förutom där den underliggande funktionen kräver indata som beror på sökvägen till användarens rörelse och inte bara på slutpunkterna.

#### Syfte - Tangentbord (2.1.1) {#purpose-keyboard}

Syftet med detta villkor är att se till att innehåll, när det är möjligt, kan köras via ett tangentbord eller tangentbord (så att ett alternativt tangentbord kan användas). När innehåll kan användas via ett tangentbord eller alternativt tangentbord kan det hanteras av personer som inte har någon syn (som inte kan använda enheter som möss som kräver ögonkoordinering) samt av personer som måste använda alternativa tangentbord eller inmatningsenheter som fungerar som tangentbordsemulatorer. Emulatorer för tangentbord omfattar talinmatningsprogram, klipp-och-knapp-program, tangentbord på skärmen, skanningsprogram samt en mängd hjälpmedelstekniker och alternativa tangentbord. Individer med nedsatt syn kan också ha problem med att spåra en pekare och upptäcka att programvaran är mycket enklare (eller endast möjligt) om de kan styra den via tangentbordet.

#### Så här möts du - tangentbord (2.1.1) {#how-to-meet-keyboard}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### Mer information - Tangentbord (2.1.1) {#more-information-keyboard}

* [Om villkor för att lyckas 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Så här uppfyller du kriterierna för framgång 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Ingen tangentbordssvällning (2.1.2)  {#no-keyboard-trap}

* Villkor för lyckat resultat 2.1.2
* Nivå A
* Ingen tangentbordssvällning: Om tangentbordsfokus kan flyttas till en komponent på sidan med hjälp av ett tangentbordsgränssnitt, kan fokus flyttas bort från den komponenten med bara ett tangentbordsgränssnitt. Om det kräver mer än oförändrad pil- eller tabbtangent eller andra standardmetoder för att avsluta, informeras användaren om metoden för att flytta fokus bort.

#### Syfte - Ingen tangentbordssvällning (2.1.2) {#purpose-no-keyboard-trap}

Syftet med detta villkor är att se till att innehållet inte *fångar upp* tangentbordsfokus i underavsnitt av innehållet på en webbsida. Detta är ett vanligt problem när flera format kombineras på en sida och återges med plugin-program eller inbäddade program.

Det kan finnas tillfällen då webbsidans funktioner begränsar fokus till ett underavsnitt av innehållet (till exempel en modal dialogruta). I sådana fall bör du ange en metod som gör att en användare kan lämna det underavsnittet av innehållet (ESC-tangenten stänger den modala dialogrutan eller en stängningsknapp stänger den modala dialogrutan).

#### Så här möts - ingen tangentbordssvällning (2.1.2) {#how-to-meet-no-keyboard-trap}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### Mer information - Ingen tangentbordssvällning (2.1.2) {#more-information-no-keyboard-trap}

* [Om villkor för att lyckas 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Så här uppfyller du kriterierna för framgång 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Tillräcklig tid (2.2) {#enough-time}

[Riktlinje 2.2 Tillräcklig tid: Ge användarna tillräckligt med tid för att läsa och använda innehållet.](https://www.w3.org/TR/WCAG/#enough-time)

Det handlar om att se till att användarna har tillräckligt med tid för att läsa och vidta åtgärder.

### Tidsjustering (2.2.1)  {#timing-adjustable}

* Villkor för lyckat resultat 2.2.1
* Nivå A
* Tangentbord: Ge användarna tillräckligt med tid för att läsa och använda innehållet.

#### Syfte - Tidsjustering (2.2.1) {#purpose-timing-adjustable}

Syftet med detta kriterium är att se till att användare med funktionshinder får tillräckligt med tid för att interagera med webbinnehållet när det är möjligt. Personer med funktionshinder som blindhet, nedsatt syn, försämrad rörlighet och kognitiva begränsningar kan behöva mer tid för att läsa innehåll eller utföra funktioner som att fylla i onlineformulär. Om webbfunktionerna är tidsberoende är det svårt för vissa användare att utföra den nödvändiga åtgärden innan en tidsgräns inträffar. Detta kan göra tjänsten oåtkomlig för dem. Att utforma funktioner som inte är tidsberoende kommer att hjälpa personer med funktionshinder att slutföra dessa funktioner. Genom att tillhandahålla alternativ för att inaktivera tidsgränser, anpassa tidslängden eller begära mer tid innan en tidsgräns inträffar, kan de användare som behöver mer tid än förväntat sig för att kunna utföra uppgifter. De här alternativen visas i den ordning som passar användaren bäst. Det är bättre att inaktivera tidsgränser än att anpassa tidsgränslängden, vilket är bättre än att begära mer tid innan en tidsgräns inträffar.

#### Så här möts - Tidsjustering (2.2.1) {#how-to-meet-timing-adjustable}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Mer information - Tidsjustering (2.2.1) {#more-information-timing-adjustable}

* [Om villkor för att lyckas 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Så här uppfyller du kriterierna för framgång 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Pausa, Stoppa, Dölj (2.2.2)  {#pause-stop-hide}

* Villkor för lyckat resultat 2.2.2
* Nivå A
* Pausa, Stoppa, Dölj: Följande gäller för flyttning, blinkning, rullning och automatisk uppdatering:
   * Rörelse, blinkning, rullning: För information som rör sig, blinkar eller rullar och som (a) startar automatiskt, (b) varar mer än fem sekunder och (c) presenteras parallellt med annat innehåll, finns det en mekanism för användaren att pausa, stoppa eller dölja den, såvida inte rörelsen, blinkningen eller rullningen är en del av en verksamhet där den är nödvändig.
   * Automatisk uppdatering: För all information som uppdateras automatiskt och som (a) startas automatiskt och (b) presenteras parallellt med annat innehåll finns det en mekanism som användaren kan använda för att pausa, stoppa eller dölja den eller för att styra uppdateringens frekvens, såvida inte den automatiska uppdateringen är en del av en aktivitet där det är nödvändigt.

Poängen är:

1. Krav som rör flimmer eller blinkande innehåll finns i Designa inte innehåll på ett sätt som är känt för att orsaka kramper (2.3).
1. Eftersom innehåll som inte uppfyller detta kriterium kan påverka användarens möjlighet att använda hela sidan, måste allt innehåll på webbsidan (vare sig det används för att uppfylla andra kriterier för framgång eller inte) uppfylla detta kriterium. Se [Krav på överensstämmelse 5: Icke-interferens](https://www.w3.org/TR/WCAG20/#cc5).
1. Innehåll som uppdateras regelbundet av programvara eller som direktuppspelas till användaragenten behöver inte bevara eller presentera information som genereras eller tas emot mellan inledandet av paus och återupptagandet, eftersom detta kanske inte är tekniskt möjligt, och i många situationer kan det vara vilseledande.
1. En animering som är en del av en förinläsningsfas eller liknande situation kan anses vara nödvändig om interaktion inte kan ske under den fasen för alla användare och om inte förloppet visar sig kan det förvirra användarna eller få dem att tro att innehållet frystes eller förstörs.

#### Syfte - Pausa, stoppa, dölj (2.2.2) {#purpose-pause-stop-hide}

Vissa användare kan finna att flyttningar är störande, eller till och med fysiskt besvärliga, vilket gör det svårt att koncentrera sig på andra delar av sidan. Dessutom kan sådant innehåll vara svårt att läsa för personer som har svårt att hänga med i rörlig text.

#### Så här möts du - Pausa, stoppa, dölj (2.2.2) {#how-to-meet-pause-stop-hide}

Beroende på innehållets natur kan du använda ett eller flera av följande förslag när du skapar webbsidor som innehåller rörligt, blinkande eller blinkande innehåll:

* Tillhandahåll ett sätt att pausa rullning av innehåll så att användarna får tillräckligt med tid för att läsa det. Till exempel nyhetsmarkörer, autouppdaterad text och bildkaruseller som går automatiskt framåt.
* Se till att innehåll som blinkar slutar blinka efter fem sekunder.
* Använd lämplig teknik för att visa rörligt eller blinkande innehåll som kan inaktiveras av webbläsaren. Exempel: GIF- (Graphics Interchange Format) eller APNG-filer (Animated Portable Network Graphics).
* Gör det möjligt för användaren att inaktivera allt rörligt eller blinkande innehåll på sidan genom att tillhandahålla en formulärkontroll på webbsidan.
* Om något av ovanstående inte är möjligt kan du skapa en länk till en sida som innehåller allt innehåll, men utan att flytta eller blinka.

#### Mer information - Pausa, Stoppa, Dölj (2.2.2) {#more-information-pause-stop-hide}

* [Förstå villkor för framgång 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Hur man uppfyller kriterierna för framgång 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Kramper och fysiska reaktioner (2.3) {#seizures-and-physcial-reactions}

[Riktlinje 2.3 Kriser: Utforma inte innehåll på ett sätt som är känt för att orsaka kramper eller fysiska reaktioner.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Tre Flash eller under tröskelvärde (2.3.1) {#three-flashes-or-below-threshold}

* Villkor för lyckat resultat 2.3.1
* Nivå A
* Tre Flash eller under tröskelvärde: Webbsidor innehåller inte något som blinkar mer än tre gånger under en sekund, eller så är blixten under de allmänna tröskelvärdena för blixt och rött.

>[!NOTE]
>
>Eftersom innehåll som inte uppfyller detta kriterium kan påverka användarens möjlighet att använda hela sidan, måste allt innehåll på webbsidan (vare sig det används för att uppfylla andra kriterier för framgång eller inte) uppfylla detta kriterium. Se [Krav på överensstämmelse 5: Icke-interferens](https://www.w3.org/TR/WCAG/#cc5).

#### Syfte - Tre Flash eller under tröskelvärde (2.3.1) {#purpose-three-flashes-or-below-threshold}

I vissa fall kan blinkande innehåll orsaka fotokänsliga anfall. Detta kriterium ger användarna möjlighet att få tillgång till och uppleva allt innehåll utan att behöva oroa sig för att innehållet blinkar.

#### Så här möts du - tre Flash eller lägre tröskelvärde (2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

Du bör vidta åtgärder för att se till att följande tekniker används:

* Se till att komponenterna inte blinkar mer än tre gånger under en 1-sekundersperiod.
* Om villkoret ovan inte kan uppfyllas visas blinkande innehåll i ett *litet säkert område* i pixlar på skärmen. Detta område beräknas med hjälp av en komplex formel som omfattas av [G176: Se till att blinkningsområdet är tillräckligt](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)litet, så denna teknik bör endast följas om blinkande innehåll är *absolut* nödvändigt.

#### Mer information - tre Flash eller lägre tröskelvärde (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Förstå villkor för framgång 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Hur man uppfyller kriterierna för framgång 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navigeringsbar (2.4) {#navigable}

[Riktlinje 2.4 Navigeringsbart: Tillhandahåller sätt att hjälpa användare navigera, hitta innehåll och avgöra var de är.](https://www.w3.org/TR/WCAG/#navigable)

Det handlar om att säkerställa att innehållet är enkelt och enkelt att navigera i.

### Kringgå block (2.4.1)  {#bypass-blocks}

* Villkor för lyckat resultat 2.4.1
* Nivå A
* Kringgå block: Det finns en mekanism som du kan använda för att kringgå innehållsblock som upprepas på flera webbsidor.

#### Syfte - Kringgå block (2.4.1) {#purpose-bypass-blocks}

Syftet med detta villkor är att personer som navigerar sekventiellt genom innehållet ska få mer direkt åtkomst till det primära innehållet på webbsidan. Webbsidor och program har ofta innehåll som visas på andra sidor eller skärmar. Exempel på upprepade innehållsblock är bland annat navigeringslänkar, rubrikgrafik, menyer och reklamramar, men är inte begränsade till dem. Små upprepade avsnitt, t.ex. enskilda ord, fraser eller enstaka länkar, anses inte utgöra block i denna bestämmelse.

#### Så här möts du - kringgå block (2.4.1) {#how-to-meet-bypass-blocks}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Mer information - Kringgå block (2.4.1) {#more-information-bypass-blocks}

* [Om villkor för att lyckas 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Så här uppfyller du kriterierna för framgång 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Sida med rubriker (2.4.2)  {#page-titled}

* Villkor för lyckat resultat 2.4.2
* Nivå A
* Sidrubrik: Webbsidor har rubriker som beskriver ämne eller syfte.

#### Syfte - Sidtitlar (2.4.2) {#purpose-page-titled}

Detta kriterium hjälper alla att snabbt identifiera innehållet på en webbsida utan att behöva läsa hela sidan, oavsett eventuella försämringar. Detta är särskilt användbart när flera webbsidor öppnas på webbläsarflikar, eftersom sidrubriken visas på fliken och därför kan hittas snabbt.

#### Så här möts du - sida titel (2.4.2) {#how-to-meet-page-titled}

När en ny HTML-sida skapas i AEM kan du ange sidrubriken. Se till att titeln på rätt sätt beskriver sidans innehåll och syfte, särskilt eventuella unika aspekter, så att besökarna snabbt kan identifiera om innehållet faktiskt är relevant för deras behov eller inte.

Du kan också redigera sidans titel när du redigerar en sida, tillgänglig via **Sidinformation** – **Egenskaper**.

#### Mer information - sida titel (2.4.2) {#more-information-page-titled}

* [Förstå villkor för framgång 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Hur man uppfyller kriterierna för framgång 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Fokusordning (2.4.3)  {#focus-order}

* Villkor för lyckat resultat 2.4.3
* Nivå A
* Fokusordning: Om en webbsida kan navigeras sekventiellt och navigeringssekvenserna påverkar innebörden eller funktionen, får fokus i komponenter som kan fokuseras i en ordning som bevarar innebörden och användbarheten.

#### Syfte - Fokusordning (2.4.3) {#purpose-focus-order}

Syftet med detta villkor är att se till att användare som navigerar sekventiellt genom innehållet stöter på information i en ordning som överensstämmer med innehållets innebörd och kan användas från tangentbordet. Detta minskar förvirringen genom att användarna kan skapa en konsekvent mentalmodell av innehållet. Det kan finnas olika sorteringsordning som återspeglar logiska relationer i innehållet. Om du till exempel förflyttar dig mellan komponenter i ett onlineformulär som består av flera fält och/eller steg, återspeglas de logiska relationerna i innehållet.

#### Så här möts du - fokusordning (2.4.3) {#how-to-meet-focus-order}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Mer information - Fokusordning (2.4.3) {#more-information-focus-order}

* [Förstå villkor för framgång 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Så här uppfyller du kriterierna för framgång 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Länksyfte (i sitt sammanhang) (2.4.4)  {#link-purpose-in-context}

* Villkor för lyckat resultat 2.4.4
* Nivå A
* Länksyfte (i sammanhang): Syftet med varje länk kan avgöras av länktexten fristående eller av länktexten tillsammans med dess programmatiskt fastställda länkkontext, utom när länkens syfte skulle vara tvetydigt för användarna i allmänhet.

#### Syfte - Länksyfte (i sammanhang) (2.4.4) {#purpose-link-purpose-in-context}

För alla användare är det viktigt att tydligt ange riktningen på en länk genom lämplig länktext, oavsett om det finns någon försämring. Detta hjälper användarna att avgöra om de faktiskt vill följa en länk eller inte. För synkade användare är meningsfull länktext mycket användbar när det finns flera länkar på en sida (särskilt om sidan är texttung), eftersom meningsfull länktext ger en tydligare indikation på målsidans funktion. Användare av vissa hjälpmedelstekniker, som kan generera en lista över alla länkar på en sida, kan enklare förstå länktexten ur sitt sammanhang om länktexten är både unik och informativ. Synkroniserade individer med kognitiva funktionshinder kan dock bli förvirrade om en länk inte ger tillräckligt med information för att korrekt beskriva var länken ska ta dem.

#### Så här möts - länksyfte (i sammanhang) (2.4.4) {#how-to-meet-link-purpose-in-context}

Se framför allt till att länkens syfte tydligt beskrivs i länktexten.

* Felaktigt exempel:
   * Text: Om du vill ha information om våra kvällskurser för hösten 2010 klickar du här.
   * Orsak: den inte tydligt och otvetydigt anger sin destination.
* Exempel:
   * Text: Kvällsklasser för hösten 2010 - detaljer.
   * Orsak: Genom att justera texten och placeringen av länkelementet något kan länktexten förbättras:

Länkarna ska vara enhetliga på olika sidor, särskilt för navigeringsfält. Om till exempel en länk till en viss sida heter **Publikationer** på en sida kan du använda den texten på andra sidor för att säkerställa konsekvens.

När du skriver finns det vissa problem med användningen av rubrikattribut som säkerställer att liknande länkar som visas på en sida ger unik information om målet (t.ex. &quot;läs mer&quot; avser ofta en rad olika destinationer):

* Texten i rubrikattributet är i allmänhet bara tillgänglig för musanvändare som popup-fönster med verktygstips och kan inte öppnas konsekvent med tangentbordet eller av mobilanvändare.
* Skärmläsare kan läsa upp rubrikattribut, men denna funktion kanske inte är aktiverad som standard. så att användare kanske inte känner till att det finns ett rubrikattribut.
* Det är svårt att ändra utseendet på titeltexten, vilket innebär att det kan vara svårt eller omöjligt att läsa av vissa personer.

Titelattributet kan användas för att ge en länk extra kontext, men tänk på dess begränsningar och använd det inte som ett alternativ till lämplig länktext.

Där länken består av en bild kontrollerar du att den alternativa texten för bilden beskriver länkens mål. Om till exempel en bild av en bokhylla är inställd som en länk till en persons publikationer bör den alternativa texten läsa **Sven Smiths publikationer** och inte **Bookshelf**.

Om länkankarpunkten innehåller text som beskriver länkens syfte förutom bildelementet (och därmed texten visas bredvid bilden) använder du ett tomt alt-attribut för bilden:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>Ovanstående kodutdrag är en illustration. Vi rekommenderar att du använder **Image** -komponenten.

Även om det är tillrådligt att ange länktext som identifierar länkens syfte utan att behöva ha ytterligare kontext, är det inte alltid möjligt. Kontextfria länkar kan användas i följande fall, där HTML-exempel finns i [How to Meet Success Criterion 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Där länktexten är en del av en lista med närbesläktade länkar och när listobjektet som omger länken ger tillräckligt med kontext.
* Om syftet med en länk tydligt kan identifieras genom *föregående* (inte följande) stycketext.
* Om länken ingår i en datatabell och därmed tydligt kan syftet identifieras från tillhörande rubriker.
* Om en lista med länkar finns i en uppsättning rubriker och själva rubriken ger rätt sammanhang.
* Om en lista med länkar finns i en kapslad länk och det överordnade listobjektet ovanför den kapslade länken ger rätt kontext.

I vissa fall, där det finns flera länkar på en sida (där var och en innehåller länkens riktning i komplex men nödvändig detalj), kan det vara lämpligt att tillhandahålla en alternativ version av webbsidan som visar exakt samma innehåll men där länktexten inte är så detaljerad.

Du kan också använda skript så att en liten del av texten finns inuti själva länken, men när du aktiverar en lämplig kontroll som är placerad överst på sidan *utökas* länktexten ytterligare. Ett liknande sätt är att använda CSS för att *dölja* den fullständiga länken för synkade användare, men ändå visa den i sin helhet för skärmläsaranvändare. Detta ligger utanför det här dokumentets räckvidd, men mer information om hur detta kan uppnås finns i avsnittet [Mer information - Länksyfte (i kontext) (2.4.4)](#more-information-link-purpose-in-context) .

#### Mer information - Länksyfte (i sammanhang) (2.4.4) {#more-information-link-purpose-in-context}

* [Förstå villkor för framgång 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Hur man uppfyller kriterierna för framgång 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Flera sätt (2.4.5)  {#multiple-ways}

* Villkor för lyckat resultat 2.4.5
* Nivå AA
* Flera sätt: Det finns mer än ett sätt att söka efter en webbsida i en uppsättning webbsidor, förutom där webbsidan är resultatet av, eller ett steg i, en process.

#### Syfte - Flera sätt (2.4.5) {#purpose-multiple-ways}

Syftet med detta kriterium är att göra det möjligt för användare att hitta innehåll på det sätt som passar deras behov bäst. En teknik kan vara lättare att använda eller lättare att förstå än en annan.

Även små webbplatser bör ge användarna en viss orienteringsmetod. För en webbplats på tre eller fyra sidor, med alla sidor länkade från hemsidan, räcker det kanske bara att tillhandahålla länkar från och till hemsidan, där länkarna på hemsidan också kan fungera som en webbplatskarta.

#### Så här möts du - flera sätt (2.4.5) {#how-to-meet-multiple-ways}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### Mer information - Flera sätt (2.4.5) {#more-information-multiple-ways}

* [Förstå villkor för framgång 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Hur man uppfyller kriterierna för framgång 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Rubriker och etiketter (2.4.6)  {#headings-and-labels}

* Villkor för lyckat resultat 2.4.6
* Nivå AA
* Rubriker och etiketter: Rubriker och etiketter beskriver ämnet eller syftet.

#### Syfte - Rubriker och etiketter (2.4.6) {#purpose-headings-and-labels}

Syftet med detta kriterium är att hjälpa användarna att förstå vilken information som finns på webbsidorna och hur informationen är organiserad. När rubrikerna är tydliga och beskrivande kan användarna enklare hitta den information de söker, och de kan enklare förstå relationen mellan olika delar av innehållet. Beskrivande etiketter hjälper användarna att identifiera specifika komponenter i innehållet.

#### Hur man uppfyller kraven - rubriker och etiketter (2.4.6) {#how-to-meet-headings-and-labels}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### Mer information - Rubriker och etiketter (2.4.6) {#more-information-headings-and-labels}

* [Förstå villkor för framgång 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Hur man uppfyller kriterierna för framgång 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Synligt fokus (2.4.7)  {#focus-visible}

* Villkor för lyckat resultat 2.4.7
* Nivå AA
* Synligt fokus: Alla tangentbordsoperativa användargränssnitt har ett driftläge där indikatorn för tangentbordsfokus visas.

#### Syfte - Synligt fokus (2.4.7) {#purpose-focus-visible}

Syftet med detta kriterium är att hjälpa en person att veta vilket element som har tangentbordsfokus.

Det måste vara möjligt för en person att veta vilket element bland flera element som har tangentbordsfokus. Om det bara finns en tangentbordskontroll på skärmen är det kriterium som uppfylls eftersom den visuella designen endast innehåller ett objekt som kan användas av tangentbordet.

Om resultatvillkoret är&quot;driftssätt&quot;, ska detta beaktas för plattformar som kanske inte alltid visar en fokusindikator. I de flesta fall finns det bara ett driftsätt, så detta kriterium gäller.

#### Hur man möter - Synligt fokus (2.4.7) {#how-to-meet-focus-visible}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Mer information - Synligt fokus (2.4.7) {#more-information-focus-visible}

* [Förstå villkor för framgång 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Så här uppfyller du kriterierna för framgång 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Princip 3: Förstå {#principle-understandable}

[Princip 3: Förstå - Information och hur användargränssnittet fungerar måste vara begripligt.](https://www.w3.org/TR/WCAG/#understandable)

### Gör textinnehåll läsbart och begripligt (3.1) {#make-text-content-readable-and-understandable}

[Riktlinje 3.1 läsbar: Gör textinnehållet läsbart och begripligt.](https://www.w3.org/TR/WCAG/#readable)

### Sidans språk (3.1.1) {#language-of-page}

* Villkor för lyckat resultat 3.1.1
* Nivå A
* Sidans språk: Det mänskliga standardspråket för varje webbsida kan bestämmas programmatiskt.

#### Syfte - Sidans språk (3.1.1) {#purpose-language-of-page}

Syftet med detta kriterium är att säkerställa att text och annat språkligt innehåll återges korrekt. För skärmläsaranvändare säkerställer detta att innehållet uttalas korrekt, medan visuella webbläsare troligtvis visar vissa teckenuppsättningar korrekt.

#### Hur man uppfyller kraven - sidans språk (3.1.1) {#how-to-meet-language-of-page}

För att uppfylla det här kriteriet kan standardspråket på en webbsida identifieras med hjälp av attributet `lang` i `<html>` elementet högst upp på sidan. Till exempel:

* Om en sida är skriven på engelska ska `<html>` elementet vara:
   `<html lang = “en”>`

* En sida som skall återges på spanska bör anta följande standard:
   `<html lang = “es”>`

I AEM anges sidans standardspråk när du skapar sidan, men det kan också ändras när du redigerar [Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md).

>[!NOTE]
>
>AEM erbjuder ytterligare finjusteringar för variationer av ett rotspråk. till exempel amerikansk engelska - en-us, brittisk engelska - en-gb och kanadensisk engelska - en-ca. Denna detaljnivå är ofta överflödig för hjälpmedelstekniker, men kan användas för regionala variationer av sidinnehåll.

#### Mer information - Sidans språk (3.1.1) {#more-information-language-of-page}

* [Om villkor för att lyckas 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Hur man uppfyller kriterierna för framgång 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Koderna baseras på ISO 639-1. En mer omfattande lista över koder för varje språk finns på [W3 Schools-sajten](https://www.w3schools.com/tags/ref_language_codes.asp).

### Delarnas språk (3.1.2)  {#language-of-parts}

* Villkor för lyckat resultat 3.1.2
* Nivå AA
* Delarnas språk: Det mänskliga språket i varje stycke eller fras i innehållet kan fastställas programmatiskt, med undantag för egennamn, tekniska termer, ord av obestämt språk samt ord eller fraser som har blivit en del av språket i den omedelbart omgivande texten.

#### Syfte - Språk för delar (3.1.2) {#purpose-language-of-parts}

Syftet med det här kriteriet är att det fungerar på samma sätt som [Sidans](#language-of-page)språk, förutom att det gäller webbsidor som innehåller innehåll på flera språk på en sida (t.ex. på grund av citat eller ovanliga låneord).

Sidor som använder det här framgångsvillkoret tillåter:

* Programmet för blindskriftsövergång för att infoga tecken med accent.
* Skärmläsare använder för att uttala ord som har specialtecken eller som inte finns i standardspråket som identifierades på sidnivå.
* Översättningsverktyg som Google Translate för korrekt översättning av innehåll från ett språk till ett annat.

#### Hur man uppfyller kraven - Språk för delar (3.1.2) {#how-to-meet-language-of-parts}

Attributet `lang` kan användas för att identifiera ändringar i innehållsspråket. En offert på tyska (ISO 639-1-kod &quot;de&quot;) kan till exempel visas på följande sätt:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Blockcitattecken stöds inte i en körklar instans. En anpassad komponent kan utvecklas som stöd för funktionen.

På samma sätt kan webbläsaren återge ett ovanligt låneord eller en ovanlig fras korrekt om elementet `span` används enligt följande:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Det är inte nödvändigt att följa detta kriterium när man inkluderar namn eller städer på olika språk, eller när man använder låneord eller fraser som har blivit vanliga på standardspråket (t.ex. *schadenfreude* på engelska).

Om du vill lägga till intervallelementet med ett lämpligt språk kan du redigera HTML-koden manuellt i källredigeringsläget för textredigeraren så att den läses som ovan. Alternativt kan attributet inkluderas i textredigeringsfilen av en systemadministratör (se `lang` Lägga till stöd för ytterligare HTML-element och attribut [](/help/implementing/developing/extending/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

#### Mer information - Språk för delar (3.1.2) {#more-information-language-of-parts}

* [Förstå villkor för framgång 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Hur man uppfyller kriterierna för framgång 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Förutsägbar (3.2) {#predictable}

[Riktlinje 3.2 Förutsägbar: Gör webbsidorna synliga och fungerar på förutsägbara sätt.](https://www.w3.org/TR/WCAG/#predictable)

Det handlar om att säkerställa att webbsidorna ser likadana ut och fungerar som de ska.

### Vid fokus (3.2.1)  {#on-focus}

* Villkor för lyckat resultat 3.2.1
* Nivå A
* Vid fokus: När en användargränssnittskomponent får fokus initieras ingen kontextändring.

#### Syfte - Vid fokus (3.2.1) {#purpose-on-focus}

Syftet med detta kriterium är att säkerställa att funktionaliteten är förutsägbar när besökarna navigerar genom ett dokument. Komponenter som kan utlösa en händelse när de får fokus får inte ändra sammanhanget. Exempel på föränderliga sammanhang när en komponent får fokus är bland annat följande, men är inte begränsade till:

* formulär som skickas automatiskt när en komponent får fokus,
* nya fönster öppnas när en komponent får fokus,
* fokus ändras till en annan komponent när den komponenten får fokus,

Fokus kan flyttas till en kontroll antingen via tangentbordet (t.ex. genom att Tabb till en kontroll) eller med musen (t.ex. genom att klicka på ett textfält). Om du flyttar musen över en kontroll flyttas inte fokus om inte skriptet implementerar det här beteendet. Observera att för vissa typer av kontroller kan det även vara möjligt att aktivera kontrollen genom att klicka på en kontroll (t.ex. knapp), som i sin tur kan starta en ändring i sammanhanget.

#### Så här möts du - i fokus (3.2.1) {#how-to-meet-on-focus}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### Mer information - I fokus (3.2.1) {#more-information-on-focus}

* [Om villkor för att lyckas 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Så här uppfyller du kriterierna för framgång 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### Indata (3.2.2)  {#on-input}

* Villkor för lyckat resultat 3.2.2
* Nivå A
* Vid inmatning: Om du ändrar inställningen för en användargränssnittskomponent ändras inte sammanhanget automatiskt, såvida inte användaren har informerats om beteendet innan komponenten används.

#### Syfte - Vid inmatning (3.2.2) {#purpose-on-input}

Syftet med det här kriteriet är att säkerställa att det går att ange data eller välja en formulärkontroll. Om du ändrar inställningen för en användargränssnittskomponent ändras vissa delar i kontrollen som kvarstår när användaren inte längre interagerar med den. Om du markerar en kryssruta, skriver text i ett textfält eller ändrar det markerade alternativet i en lista ändras inställningen, men om du aktiverar en länk eller en knapp ändras inte inställningen. Ändringar i sammanhanget kan förvirra användare som inte lätt uppfattar ändringen eller som lätt distraheras av ändringar. Kontextändringar är bara lämpliga när det är tydligt att en sådan ändring kommer att ske som svar på användarens åtgärd.

#### Så här möts - Vid inmatning (3.2.2) {#how-to-meet-on-input}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### Mer information - Vid inmatning (3.2.2) {#more-information-on-input}

* [Om villkor för att lyckas 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Så här uppfyller du kriterierna för framgång 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Enhetlig navigering (3.2.3)  {#consistent-navigation}

* Villkor för lyckat resultat 3.2.3
* Nivå AA
* Enhetlig navigering: Navigeringsfunktioner som upprepas på flera webbsidor i en uppsättning webbsidor sker i samma relativa ordning varje gång de upprepas, såvida inte användaren påbörjar en ändring.

#### Syfte - Enhetlig navigering (3.2.3) {#purpose-consistent-navigation}

Syftet med detta kriterium är att uppmuntra till enhetlig presentation och layout för användare som interagerar med upprepat innehåll på en uppsättning webbsidor och behöver hitta specifik information eller funktionalitet mer än en gång. Personer med nedsatt syn som använder skärmförstoring för att visa en liten del av skärmen i taget använder ofta visuella ledtrådar och sidgränser för att snabbt hitta upprepat innehåll. Att presentera upprepat innehåll i samma ordning är också viktigt för visuella användare som använder rumsligt minne eller visuella ledtrådar i designen för att hitta upprepat innehåll.

Det är viktigt att komma ihåg att användningen av frasen&quot;samma ordning&quot; i detta avsnitt inte ska innebära att undernavigeringsmenyer inte kan användas eller att block av sekundär navigering eller sidstruktur inte kan användas. Istället är resultatvillkoret avsett att hjälpa användare som interagerar med upprepat innehåll på webbsidor att kunna förutse platsen för det innehåll de söker och hitta det snabbare när de stöter på det igen.

Användare kan initiera en ändring av ordningen med hjälp av adaptiva användaragenter eller genom att ange inställningar så att informationen presenteras på ett sätt som är mest användbart för dem.

#### Hur man möter - Enhetlig navigering (3.2.3) {#how-to-meet-consistent-navigation}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### Mer information - Enhetlig navigering (3.2.3) {#more-information-consistent-navigation}

* [Förstå villkor för framgång 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Så här uppfyller du kriterierna för framgång 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Konsekvent identifiering (3.2.4)  {#consistent-identification}

* Villkor för lyckat resultat 3.2.4
* Nivå A
* Konsekvent identifiering: Komponenter som har samma funktionalitet i en uppsättning webbsidor identifieras konsekvent.

#### Syfte - Konsekvent identifiering (3.2.4) {#purpose-consistent-identification}

Syftet med detta kriterium är att säkerställa en konsekvent identifiering av funktionskomponenter som visas upprepade gånger i en uppsättning webbsidor. En strategi som användare av skärmläsare använder när de använder en webbplats är att förlita sig mycket på att de känner till funktioner som kan visas på olika webbsidor. Om identiska funktioner har olika etiketter (eller mer allmänt ett annat namn) på olika webbsidor blir webbplatsen betydligt svårare att använda. Den kan också vara förvirrande och öka den kognitiva belastningen för personer med kognitiva begränsningar. Därför kommer konsekventa etiketter att hjälpa.

Den här konsekvensen omfattar även textalternativen. Om ikoner eller andra icke-textobjekt har samma funktioner bör deras textalternativ också vara konsekventa.

Om det finns två komponenter på en webbsida som båda har samma funktioner som en komponent på en annan sida i en uppsättning webbsidor, måste alla tre vara konsekventa. Därför kommer de båda på samma sida att vara konsekventa.

Det är önskvärt och bästa praxis att alltid vara konsekvent på en enda webbsida, men 3.2.4 behandlar endast konsekvens inom en uppsättning webbsidor där något upprepas på mer än en sida i uppsättningen.

#### Hur man uppfyller kraven - Konsekvent identifiering (3.2.4) {#how-to-meet-consistent-identification}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### Mer information - Konsekvent identifiering (3.2.4) {#more-information-consistent-identification}

* [Förstå villkor för framgång 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Så här uppfyller du kriterierna för framgång 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Ingångsstöd (3.3) {#input-assistance}

[Riktlinje 3.3 Ingångsstöd: Hjälp användarna att undvika och rätta till misstag.](https://www.w3.org/TR/WCAG/#input-assistance)

### Felidentifiering (3.3.1)  {#error-identification}

* Villkor för lyckat resultat 3.3.1
* Nivå A
* Felidentifiering: Om ett indatafel upptäcks automatiskt identifieras det felande objektet och felet beskrivs till användaren i texten.

#### Syfte - Felidentifiering (3.3.1) {#purpose-error-identification}

Syftet med detta villkor är att se till att användarna är medvetna om att ett fel har inträffat och kan avgöra vad som är fel. Felmeddelandet ska vara så specifikt som möjligt. Om ett formulär inte kan skickas räcker det att återvisa formuläret och ange felfälten för att vissa användare ska inse att ett fel har inträffat. Användare med skärmläsare vet till exempel inte om ett fel har inträffat förrän de stöter på en av indikatorerna. De kan hoppa över hela formuläret innan felindikatorn påträffas, eftersom de tror att sidan helt enkelt inte fungerar. Enligt definitionen i WCAG är ett [indatafel](https://www.w3.org/TR/WCAG/#dfn-input-error) information som användaren anger och som inte accepteras. Detta omfattar följande:

information som krävs av webbsidan men utelämnas av användaren, eller information som tillhandahålls av användaren men som ligger utanför det obligatoriska dataformatet eller tillåtna värden.
Till exempel:

* användaren inte anger rätt förkortning i till exempel delstat, provins eller region. fält;
* användaren skriver en lägesförkortning som inte är ett giltigt tillstånd,
* användaren anger ett postnummer som inte finns,
* Användaren skriver in ett födelsedatum två år i framtiden.
* användaren skriver in alfabetiska tecken eller parenteser i sitt telefonnummerfält som endast accepterar siffror,
* användaren lägger ett bud som är lägre än föregående bud eller den lägsta anbudsökningen.

#### Så här möts du - Felidentifiering (3.3.1) {#how-to-meet-error-identification}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### Mer information - Felidentifiering (3.3.1) {#more-information-error-identification}

* [Om villkor för att lyckas 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Så här uppfyller du kriterierna för framgång 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Etiketter eller instruktioner (3.3.2) {#labels-or-instructions}

* Villkor för lyckat resultat 3.3.2
* Nivå A
* Etiketter eller instruktioner: Etiketter eller instruktioner tillhandahålls när innehållet kräver användarindata.

#### Syfte - Etiketter eller instruktioner (3.3.2) {#purpose-labels-or-instructions}

Att ge instruktioner som hjälper människor att fylla i formulär är en grundläggande del av god praxis när det gäller gränssnittsanvändning. Detta är särskilt användbart för personer med nedsatt syn eller kognitiva funktionshinder som annars skulle kunna få svårt att förstå layouten i ett formulär och den typ av data som ska anges i ett visst formulärfält.

##### Forms

I AEM WKND-demoprojekt läggs en standardetikett till när du lägger till en formulärkomponent, till exempel ett **textfält**, på sidan. Den här standardtiteln beror på komponenttypen. Du kan lägga till en egen rubrik på fliken **Titel och Text** i redigeringsdialogrutan för det fältet. Det är viktigt att se till att etiketter hjälper användarna att förstå informationen som är kopplad till varje formulärkomponent.

Det här **titelfältet** måste användas för fältelement eftersom det innehåller en etikett som är tillgänglig för hjälpmedelsteknik. Det räcker inte att bara skriva en etikett bredvid fältet.

För vissa formulärkomponenter går det även att dölja etiketter visuellt med kryssrutan **Dölj titel**. Etiketter som döljs på det här sättet är fortfarande tillgängliga för hjälpfunktioner, men de visas inte på skärmen. Detta kan vara en bra metod i vissa situationer, men det är oftast bäst att ta med en visuell etikett om det går, eftersom vissa användare kanske tittar på en mycket liten del på skärmen (ett fält i taget) och behöver etiketterna för att identifiera fältet korrekt.

###### Bildknappar {#image-buttons}

Where image buttons are used (for example, the **Image Button** component of the WKND project) the **Title** field in the **Title and Text** tab of the edit dialog actually provides the alt text for the image, rather than the label. I exemplet nedan har bilden med texten `Submit` Alt-texten `Submit`, som lagts till med fältet **Titel** i redigeringsdialogrutan.

###### Grupper med formulärfält {#groups-of-form-fields}

In the WKND project, where there is a group of related controls, such as **Radio Group**, a title may be needed for the group, as well as individual controls. När du lägger till en uppsättning med alternativknappar i AEM visas den här grupptiteln i fältet **Titel**, medan enskilda titlar anges när alternativknapparna (**Objekt**) skapas.

Det finns dock ingen programmatisk koppling mellan grupptiteln och alternativknapparna själva. Mallredigerare måste kapsla in titeln i de nödvändiga `fieldset`- och `legend`-taggarna för att skapa den här kopplingen. Detta kan bara göras genom att redigera sidans källkod. En systemadministratör kan också lägga till stöd för dessa element så att de visas i dialogrutan **Fältegenskaper**[ (se Lägga till stöd för ytterligare HTML-element och attribut](/help/implementing/developing/extending/rte-accessible-content.md)).

###### Ytterligare överväganden för Forms {#additional-considerations-for-forms}

Om data ska matas in i ett visst format bör du göra detta tydligt i etikettexten. Om ett datum t.ex. måste anges i `DD-MM-YYYY` formatet, anger du det här som en del av etiketten. Det innebär att när skärmläsaranvändare stöter på fältet visas etiketten automatiskt tillsammans med ytterligare information om formatet.

Om indata för ett formulärfält är obligatoriska klargör du detta genom att använda ordet ”required” som en del av etiketten. AEM lägger till en asterisk när ett fält är obligatoriskt, men det är bra att inkludera ordet `required` i själva etiketten (i fältet **Titel** i redigeringsdialogrutan).

Placeringen av etiketter är också viktig eftersom den hjälper dem att hitta rätt fält. Detta är särskilt viktigt när användaren har ett komplext formulär. Följ konventionen nedan:

* Kryssrutor eller alternativknappar:
Etiketter placeras direkt till höger om fältet.
* Alla andra formulärkomponenter (t.ex. textrutor, kombinationsrutor):
Etiketterna placeras antingen direkt ovanför eller direkt till vänster om fältet.

I enkla formulär med mycket begränsad funktionalitet kan en lämplig etikett på en `Submit` knapp fungera som etikett för det intilliggande fältet (till exempel `Search`). Detta är användbart när det kan vara svårt att hitta plats för etikettexten.

#### Mer information - etiketter eller instruktioner (3.3.2) {#more-information-labels-or-instructions}

* [Förstå villkor för framgång 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Hur man uppfyller kriterium 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Felförslag (3.3.3)  {#error-suggestion}

* Villkor för lyckat resultat 3.3.3
* Nivå AA
* Tangentbord: Om ett indatafel upptäcks automatiskt och förslag på korrigering är kända, kommer förslag att ges till användaren, såvida det inte skulle äventyra innehållets säkerhet eller syfte.

#### Syfte - Felförslag (3.3.3) {#purpose-error-suggestion}

Syftet med detta villkor är att se till att användarna får lämpliga förslag på hur ett indatafel kan korrigeras om det är möjligt. WCAG-definitionen av [indatafel](https://www.w3.org/TR/WCAG/#dfn-input-error) anger att det är &quot;information som användaren tillhandahåller som inte accepteras&quot; av systemet. Några exempel på information som inte accepteras är information som är obligatorisk men utelämnad av användaren och information som tillhandahålls av användaren men som ligger utanför det obligatoriska dataformatet eller tillåtna värden.

Success Criterion 3.3.1 innehåller meddelanden om fel. Personer med kognitiva begränsningar kan dock finna det svårt att förstå hur felen ska korrigeras. Personer med visuella funktionshinder kanske inte kan komma på exakt hur felet ska korrigeras. Om formuläret inte kan skickas kan användaren överge det eftersom han/hon kanske inte vet hur felet ska åtgärdas trots att han/hon vet att det har inträffat.

Innehållsförfattaren kan ge en beskrivning av felet eller så kan användaragenten ge en beskrivning av felet baserat på teknikspecifik, programmässigt bestämd information.

#### Så här möts du - Felförslag (3.3.3) {#how-to-meet-error-suggestion}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### Mer information - Felförslag (3.3.3) {#more-information-error-suggestion}

* [Förstå villkor för framgång 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Så här uppfyller du kriterierna för framgång 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Förebygga fel (juridisk, finansiell, data) (3.3.4)  {#error-prevention-legal-financial-data}

* Villkor för lyckat resultat 3.3.4
* Nivå AA
* Felförebyggande (juridisk, finansiell, datarelaterad): För webbsidor som gör att juridiska åtaganden eller ekonomiska transaktioner för användaren inträffar, som ändrar eller tar bort användarstyrda data i datalagringssystem eller som skickar in testsvar från användaren, gäller minst något av följande:

   * ReversibleSubmissions är reversibel.
   * CheckedData som anges av användaren kontrolleras för indatafel och användaren ges möjlighet att korrigera dem.
   * BekräftatDet finns en mekanism för att granska, bekräfta och korrigera information innan överföringen är klar.

#### Syfte - Förebyggande av fel (rättsliga, finansiella, uppgifter) (3.3.4) {#purpose-error-prevention-legal-financial-data}

Syftet med detta kriterium är att hjälpa användare med funktionshinder att undvika allvarliga konsekvenser till följd av ett misstag när de utför en åtgärd som inte kan ångras. Exempel: köp av icke-återbetalningsbara flygbiljetter eller inlämning av en order om att köpa aktier på ett mäklarkonto är finansiella transaktioner med allvarliga följder. Om en användare har gjort ett misstag på flygresedagen kan han eller hon få en biljett för fel dag som inte kan bytas ut. Om användaren begick ett misstag i fråga om antalet aktier som skulle köpas kan det resultera i att han eller hon köper mer aktier än vad som är tänkt. Båda dessa typer av misstag innebär transaktioner som äger rum omedelbart och som inte kan ändras i efterhand, och som kan vara mycket dyra. På samma sätt kan det vara ett oåterkalleligt fel om användare oavsiktligt ändrar eller tar bort data som lagras i en databas som de senare behöver ha tillgång till, till exempel hela reseprofilen på en webbplats för resetjänster. När det gäller ändring eller borttagning av användarkontrollerbara data är avsikten att förhindra massförlust av data som att ta bort en fil eller post. Det är inte avsikten att kräva en bekräftelse för varje Spara-kommando eller att enkelt skapa eller redigera dokument, poster eller andra data.

Användare med funktionshinder kan vara mer benägna att göra misstag. Personer med lässvårigheter kan transponera siffror och bokstäver, och personer med motoriska funktionshinder kan råka ut för nycklar av misstag. Om användaren kan ångra åtgärder kan användaren rätta till ett misstag som kan få allvarliga följder. Genom att tillhandahålla möjligheten att granska och korrigera information kan användaren upptäcka ett misstag innan han eller hon vidtar en åtgärd som får allvarliga följder.

Användarstyrda data är användaranpassade data som användaren kan ändra och/eller ta bort genom en avsiktlig åtgärd. Exempel på användare som kontrollerar sådana data är att uppdatera telefonnumret och adressen för användarens konto eller att ta bort en post med tidigare fakturor från en webbplats. Det refererar inte till sådant som Internet-loggar och övervakningsdata från sökmotorn som användaren inte kan visa eller interagera med direkt.

#### Hur man ska uppfylla kraven - Förebyggande av fel (rättsliga, finansiella, uppgifter) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Mer information - Felförebyggande (Juridik, Finans, Data) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Förstå villkor för framgång 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Så här uppfyller du kriterierna för framgång 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Princip 4: Robust {#principle-robust}

[Princip 4: Robust - Innehållet måste vara tillräckligt robust för att kunna tolkas av ett stort antal användaragenter, inklusive hjälpmedelstekniker.](https://www.w3.org/TR/WCAG/#robust)

### Kompatibel (4.1) {#compatible}

[Riktlinje 4.1 Kompatibel: Maximera kompatibiliteten med nuvarande och framtida användaragenter, inklusive hjälpmedelstekniker.](https://www.w3.org/TR/WCAG/#compatible)

Maximera kompatibiliteten med nuvarande och framtida användaragenter, inklusive hjälpmedelstekniker.

### Analys (4.1.1)  {#parsing}

* Villkor för lyckat resultat 4.1.1
* Nivå A
* Analys: I innehåll som implementeras med hjälp av markeringsspråk har elementen fullständiga start- och sluttaggar, elementen är kapslade enligt deras specifikationer, elementen innehåller inte duplicerade attribut och alla ID:n är unika, förutom där specifikationerna tillåter dessa funktioner.

#### Syfte - Analys (4.1.1) {#purpose-parsing}

Syftet med detta kriterium är att se till att användaragenter, inklusive hjälpmedelstekniker, kan tolka och tolka innehåll korrekt. Om innehållet inte kan tolkas i en datastruktur kan olika användaragenter presentera det annorlunda eller helt inte kunna tolka det. Vissa användaragenter använder&quot;reparationstekniker&quot; för att återge dåligt kodat innehåll.

Eftersom reparationstekniken varierar mellan olika användaragenter kan man inte anta att innehållet tolkas korrekt i en datastruktur eller att det återges korrekt av specialiserade användaragenter, inklusive hjälpmedelstekniker, såvida inte innehållet skapas enligt reglerna som definieras i den formella grammatiken för den tekniken. I kodspråk leder fel i elementsyntax och attributsyntax samt misslyckande med att tillhandahålla korrekt kapslade start-/sluttaggar till fel som förhindrar att användaragenter tolkar innehållet på ett tillförlitligt sätt. Därför kräver resultatvillkoret att innehållet kan tolkas med enbart reglerna för den formella grammatiken.

#### Så här möts du - parsing (4.1.1) {#how-to-meet-parsing}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Mer information - Analys (4.1.1) {#more-information-parsing}

* [Om villkor för att lyckas 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Hur man uppfyller kriterierna för framgång 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Namn, roll, värde (4.1.2)  {#name-role-value}

* Villkor för lyckat resultat 4.1.2
* Nivå A
* Namn, roll, värde: För alla användargränssnittskomponenter (inklusive men inte begränsat till: formulärelement, länkar och komponenter som genereras av skript), kan namnet och rollen fastställas programmatiskt, tillstånd, egenskaper och värden som användaren kan ange kan ställas in programmatiskt, och meddelanden om ändringar av dessa objekt är tillgängliga för användaragenter, inklusive hjälpmedelstekniker.

#### Syfte - Namn, roll, värde (4.1.2) {#purpose-ame-role-value}

Syftet med detta villkor är att se till att hjälpfunktioner kan samla in information om, aktivera (eller ställa in) och hålla sig uppdaterade om statusen för användargränssnittskontrollerna i innehållet.

När standardkontroller från hjälpmedelstekniker används är den här processen enkel. Om elementen i användargränssnittet används enligt specifikationen är villkoren i denna bestämmelse uppfyllda. (Se exempel på villkor för att lyckas 4.1.2 nedan)

Om anpassade kontroller skapas, eller gränssnittselement programmeras (i kod eller skript) för att ha en annan roll och/eller funktion än vanligt, måste ytterligare åtgärder vidtas för att säkerställa att kontrollerna tillhandahåller viktig information för hjälpmedelstekniker och gör att de kan styras av hjälpmedelstekniker.

Ett särskilt viktigt läge för en användargränssnittskontroll är om den har fokus eller inte. Fokusläget för en kontroll kan fastställas programmatiskt och meddelanden om fokusändring skickas till användaragenter och hjälpmedelsteknik. Andra exempel på kontrollstatus för användargränssnittet är om en kryssruta eller alternativknapp har markerats eller om ett komprimeringsbart träd eller en listnod är expanderad eller komprimerad.

#### Så här möts du - namn, roll, värde (4.1.2) {#how-to-meet-ame-role-value}

Följ riktlinjerna under [Så här uppfyller du kriterierna för framgång 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Mer information - Namn, Roll, Värde (4.1.2 {#more-information-ame-role-value}

* [Om villkor för att lyckas 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Hur man uppfyller kriterierna för framgång 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)

---
title: Förstå universell redigerare
description: Den här självstudiekursen hjälper dig att komma igång med Universal Editor-gränssnittet. Det vägleder dig att förstå användargränssnittet för att skapa egna Edge Delivery Services-formulär i Universell redigerare.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 0%

---


# Exploring the Universal Editor (WYSIWYG) Interface

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) har ett enkelt, visuellt och intuitivt What You See Is What You Get-gränssnitt (WYSIWYG) för Adobe Edge Delivery Services Forms. Det har ett modernt gränssnitt med dra-och-släpp-funktioner för effektiv formulärutveckling.

![Användargränssnitt för Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Vad du kommer att lära dig

I slutet av den här självstudiekursen ska du:

- Förstå huvudkomponenterna i Universella redigeringsgränssnittet
- Navigera säkert mellan de olika gränssnittsavsnitten
- Lär dig använda de verktyg du behöver för att skapa formulär
- Bekanta dig med kortkommandon som ökar produktiviteten

## Förstå det universella redigeringsgränssnittet

När du redigerar ett formulär med Universal Editor öppnar konsolen ett interaktivt WYSIWYG-gränssnitt där du kan börja redigera direkt. Det här gränssnittet ger visuell feedback i realtid när du arbetar och visar exakt hur formuläret kommer att se ut för användarna.

>[!NOTE]
>
> Läs artikeln [Komma igång med Edge Delivery Services för AEM Forms med Universal Editor (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) om du vill lära dig hur du skapar formulär med den universella redigeraren.

![Användargränssnitt för Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

Gränssnittet för Universal Editor är uppdelat i fyra logiska delar:

- **[A: Experience Cloud Header](#experience-cloud-header)**
- **[B: Verktygsfältet Universal Editor](#universal-editor-toolbar)**
- **[C: Egenskapspanelen](#properties-panel)**
- **[D: Redigeraren](#editor)**

Låt oss utforska varje avsnitt i detalj.

### Experience Cloud Header

Experience Cloud Header visas högst upp i konsolen och ger navigeringsmöjligheter i det större Adobe Experience Cloud-ekosystemet. Här ser du var du befinner dig och du får snabb tillgång till andra Experience Cloud-program.

![Universal Editor Experience Cloud Header](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

Låt oss granska varje komponent:

- **Adobe Experience Cloud**

  Om du klickar på länken **Adobe Experience Cloud** till vänster på skärmen kan du navigera till roten på Experience Manager-lösningen. Därifrån har du tillgång till andra verktyg som Experience Manager Sites, Experience Manager Assets och Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **Organisationsnamn**

  **Organisationsnamn** visar namnet på den Identity Management System-organisation (IMS) som du är inloggad på. Om du har tillgång till flera organisationer kan du växla mellan dem med den här listrutan. I skärmbilden är till exempel den IMS-organisation som är vald för tillfället&quot;AEM Forms Internal01&quot;.

  ![Organisation](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **Hjälp**

  Ikonen Hjälp ger snabb åtkomst till utbildningsresurser och supportresurser. Detta är särskilt värdefullt när du stöter på problem eller behöver hjälp med specifika funktioner. Du kan även skicka feedback genom det här avsnittet.

  ![Hjälp](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **Meddelanden**

  Avsnittet **Meddelanden** visar antalet för närvarande tilldelade ofullständiga meddelanden, förfrågningar och aktuella uppgifter i IMS-organisationen. Genom att hålla ett öga på det här avsnittet kan du hålla dig à jour med ditt arbetsflöde.

  ![Meddelande](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **Lösningar**

  På menyn **Lösningar** kan du växla till andra Adobe Experience Cloud-lösningar, vilket gör det enkelt att växla mellan olika verktyg i arbetsflödet.

  ![Lösningar](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **Användarprofil**

  Den här ikonen visar din profilinformation tillsammans med namnet på den IMS-organisation som du är inloggad på just nu. Klicka på den här ikonen för att komma åt kontoinställningar och utloggningsalternativ.

  ![Författare](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### Verktygsfältet Universell redigerare

Verktygsfältet innehåller viktiga verktyg för navigering och redigering. Med den kan du gå mellan formulär, publicera eller avpublicera formulär, redigera formuläregenskaper och komma åt regelredigeraren för att lägga till dynamiska beteenden.

![Verktygsfältet Universal Editor](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Det här erbjuder varje komponent:

- **Hemknapp**

  Med hemknappen kommer du tillbaka till startsidan för Universal Editor. Detta är användbart när du behöver börja arbeta med ett annat formulär. Du kan också ange en URL direkt i platsfältet för att navigera till ett formulär som du vill redigera.

  ![Startsida för Universal Editor](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **Platsfält**

  **Platsfältet** visar adressen till det formulär som du redigerar just nu. Om du vill växla till ett annat formulär klickar du bara på platsfältet och anger dess URL. Kortkommandot för att fokusera på platsfältet är `l`.

  ![Platsfält](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **Regelredigeraren**

  Med **regelredigeraren** kan du lägga till dynamiska beteenden i formulär via ett intuitivt visuellt gränssnitt. Med det kan du skapa villkor, valideringar och åtgärder som svarar på användarens inmatningar, vilket gör formulären interaktiva och intelligenta.

  ![Regelredigeraren](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - Tillägget Regelredigeraren är inte aktiverat som standard i Universell redigerare. Om du vill aktivera den här kraftfulla funktionen kan du kontakta oss på [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) från din officiella e-postadress.
  > - Mer information om hur du skapar och hanterar regler finns i artikeln [Introduktion till regelredigeraren i WYSIWYG Authoring](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

- **Redigera formuläregenskaper**

  Med alternativet **Redigera formuläregenskaper** kan du konfigurera viktiga formulärinställningar, till exempel formulärdatamodellen (FDM) och publiceringsdatumet. Dessa egenskaper påverkar hur formuläret fungerar och integreras med datasystemen.

  ![Redigera formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **Inställningar för autentiseringshuvud**

  Med alternativet **Inställningar för autentiseringshuvud** kan du ange anpassade autentiseringshuvuden för lokal utveckling. Detta är särskilt användbart när du testar formulär som kräver inloggningsuppgifter.

  ![Autentiseringshuvud](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **Responsivt läge**

  Med funktionen **Responsivt läge** kan du testa hur formuläret kommer att visas på olika enheter. Som standard öppnas redigeraren i skrivbordslayout, men du kan växla till mobilvyn så att formuläret förblir användbart och tilltalande på mindre skärmar.

  ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **Förhandsgranskningsläge**

  **Förhandsgranskningsläge** visar formuläret exakt som det kommer att se ut när det publiceras. På så sätt kan du interagera med formuläret genom att klicka på länkar och knappar, precis som användarna skulle göra. Detta är ett viktigt steg innan publicering för att kontrollera att allt fungerar som det ska. Växla mellan redigerings- och förhandsgranskningslägena med kortkommandot `p`.

  ![Förhandsgranska](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **Öppna sida**

  Knappen **Öppna sida** öppnar formuläret på en ny webbläsarflik för förhandsgranskning. Detta ger en helskärmsvy av formuläret utan redigeringsgränssnittet. Kortkommandot för den här åtgärden är `o`.

  ![Öppna sida](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **Publicera**

  När formuläret är klart för användare gör knappen **Publicera** det tillgängligt för läsarna. Det här är det sista steget i arbetsflödet för att skapa formulär.

  ![Publicera](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **Ellips-menyn**

  Om du klickar på ellipsen (..) visas ytterligare alternativ, bland annat möjligheten att **Avpublicera** ett formulär som för närvarande är aktivt. Detta är användbart när du tillfälligt behöver ta bort ett formulär från den offentliga åtkomsten eller ersätta det med en uppdaterad version.

  ![Ellips](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### Egenskapspanelen

**Egenskapspanelen** visas till höger i gränssnittet och sammanhangsberoende information visas baserat på vad du har valt i formuläret. När ingen komponent är markerad visas den övergripande formulärstrukturen.

![Egenskapspanelen](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

Låt oss utforska de viktigaste komponenterna:

- **Egenskapsläge**

  I **egenskapsläget** visas inställningar och alternativ för den markerade komponenten. Här kan du anpassa enskilda element i formuläret efter dina specifika behov. Kortkommandot för att öppna egenskaper för en markerad komponent är `d`.

  ![Egenskaper](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **Innehållsträd**

  **Innehållsträdet** visar formulärets hierarkiska struktur. Den här visuella representationen hjälper dig att förstå hur komponenterna är kapslade i varandra. Om du klickar på ett objekt i trädet markeras det i redigeraren och rullas till dess plats. Detta är särskilt användbart i komplexa formulär. Växla vyn för innehållsträdet med kortkommandot `f`.

  ![Innehållsträdet](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **Generera variationer**

  Funktionen **Generera variationer** använder artificiell intelligens för att skapa olika versioner av ditt formulär baserat på specifika uppmaningar. Det gör att du kan experimentera med olika metoder och utformningar utan att behöva skapa varje enskild variation manuellt. Frågorna kan tillhandahållas av Adobe eller anpassas av dig.

  ![Generera variationer](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > Detaljerade instruktioner om hur du använder Generera variationer för formulär finns i artikeln [Generera variationer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations).

- **Experimentation**

  Med funktionen **Experimentation** kan du köra kontrollerade tester som jämför olika formulärdesigner och layouter. Genom att analysera hur användarna interagerar med varje variant kan ni fatta datadrivna beslut för att optimera konverteringsgraden och användarupplevelsen.

  ![Experimentation](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **Personalization**

  Med inställningarna för **Personalization** kan du ansluta dina formulär med Adobe Experience Platform (AEP) eller externa program. Med den här anslutningen kan ni skapa skräddarsydda formulärupplevelser baserat på användardata och beteenden, vilket ökar relevansen och engagemanget.

  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **A/B-testning**

  **A/B-testning** hjälper dig att jämföra specifika varianter av formuläret för att avgöra vilka som fungerar bäst. Till skillnad från bredare experiment fokuserar A/B-tester vanligtvis på att jämföra specifika element eller ändringar för att identifiera det mest effektiva alternativet.

  ![A/B-testning](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **Aktivitetshantering**

  Funktionen **Aktivitetshantering** effektiviserar samarbetet genom att hjälpa ditt team att organisera, spåra och slutföra uppgifter som rör skapande och optimering av formulär. Detta gör att projekten kan utvecklas effektivt med tydlig ansvarsskyldighet.

  ![Aktivitetshantering](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **Innehållsutkast**

  Med funktionen **Innehållsutkast** kan du skapa och spara preliminära versioner av textelement i formuläret. Du kan skapa utkast med befintlig formulärtext eller börja från början och sedan redigera eller ta bort dem efter behov. Som standard visas tre utkast, men om du klickar på **Visa alla** visas ytterligare utkast.

  ![Innehållsutkast](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **Data Source**

  Med alternativet **Data Source** kan du konfigurera och välja datakällor för din formulärdatamodell (FDM). Den här integreringen gör alla datamodellsobjekt, egenskaper och tjänster från de valda källorna tillgängliga för användning i formuläret, vilket möjliggör dynamisk hämtning och överföring av data.

  ![Data Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **Lägg till**

  Knappen **Lägg till** visar en listruta med komponenter som kan läggas till i den markerade behållaren. Om du t.ex. markerar ett avsnitt med adaptiva formulär visas alla komponenter som kan läggas till i det avsnittet. Kortkommandot för att öppna komponentlistan är `a`.

  ![Lägg till ikon](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **Duplicera**

  Med alternativet **Duplicera** skapas en exakt kopia av den markerade komponenten. Detta sparar tid när du behöver flera liknande element, eftersom du kan duplicera och sedan ändra i stället för att skapa från början.

  ![Duplicera ikon](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **Ta bort**

  Alternativet **Ta bort** tar bort den markerade komponenten från formuläret. Var försiktig när du använder det här alternativet eftersom elementet omedelbart tas bort utan att någon bekräftelsefråga visas.

  ![Ta bort](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### Redigerare

Redigeraren är den centrala arbetsytan där du skapar och ändrar formuläret. Formuläret som har angetts i platsfältet visas och en WYSIWYG-upplevelse visar exakt hur formuläret kommer att se ut för användarna. I förhandsgranskningsläget kan du interagera med formuläret på samma sätt som användarna gör och testa navigeringen med knappar och länkar.

![Redigeraren](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

Det är i redigeraren som du tillbringar mycket tid med att lägga till komponenter, konfigurera deras egenskaper och ordna dem för att skapa en intuitiv och effektiv formulärupplevelse.

## Sammanfattning av kortkommandon

Kom ihåg följande viktiga kortkommandon för att öka produktiviteten:

- `l` - Fokusera på platsfältet
- `p` - Växla mellan redigerings- och förhandsgranskningslägen
- `o` - Öppna formuläret på en ny flik
- `d` - Öppna egenskaper för den markerade komponenten
- `f` - Växla vyn för innehållsträdet
- `a` - Öppna listan över komponenter som ska läggas till



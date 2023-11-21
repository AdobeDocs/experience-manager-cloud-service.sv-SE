---
title: Responsiv layout
description: AEM kan du förverkliga en responsiv layout för dina sidor
exl-id: 87202742-5bed-4e87-a427-456a1a0e72cc
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 6%

---

# Responsiv layout {#responsive-layout}

AEM kan du använda en responsiv layout för dina sidor med **Layoutbehållare** -komponenten.

Detta ger ett styckesystem där du kan placera komponenter i ett responsivt rutnät. Rutnätet kan ändra layouten beroende på enhetens/fönstrets storlek och format. Komponenten används tillsammans med [**Layout** läge](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes), vilket gör att du kan skapa och redigera din responsiva layout beroende på enhet.

Layoutbehållaren:

* Tillhandahåller vågrät fäst mot rutnät, tillsammans med möjligheten att placera komponenter i rutnätet sida vid sida och definiera när de ska komprimeras/omformas.
* Använder fördefinierade brytpunkter (till exempel för telefon, surfplatta och så vidare) för att du ska kunna definiera önskat beteende för innehåll för relaterade enheter/orientering.
   * Du kan till exempel anpassa komponentstorleken eller om komponenten kan visas på särskilda enheter.
* Kan kapslas så att kolumnkontroll tillåts.

Användaren kan sedan se hur innehållet återges för specifika enheter med emulatorn.

AEM realiserar responsiv layout för dina sidor med en kombination av mekanismer:

* [**Layoutbehållare**](#adding-a-layout-container-and-its-content-edit-mode) komponent

  Den här komponenten är tillgänglig i [komponentwebbläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) och har ett rutnätsstyckesystem där du kan lägga till och placera komponenter i ett responsivt rutnät. Den kan också anges som standardstyckesystem på sidan.

* [**Layoutläge**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

  När layoutbehållaren är placerad på sidan kan du använda **Layout** läge för att placera innehåll i det responsiva rutnätet.

* [**Emulator**](#selecting-a-device-to-emulate)
På så sätt kan du skapa och redigera responsiva webbplatser som ändrar layouten beroende på enhetens/fönstrets storlek genom att ändra komponenternas storlek interaktivt. Användaren kan sedan se hur innehållet återges med emulatorn.

Med dessa responsiva rutnätsmekanismer kan du:

* Använd brytpunkter för att definiera olika innehållslayouter baserat på enhetens bredd (relaterat till enhetstyp och orientering).
* Använd samma brytpunkter och innehållslayouter för att se till att innehållet är anpassat till storleken på webbläsarfönstret på skrivbordet.
* Använd vågrät fäst mot rutnät för att placera komponenter i rutnätet, ändra storlek efter behov och definiera när de ska komprimeras/omformas så att de ligger sida vid sida eller ovanför/nedanför.
* Dölj komponenter för specifika enhetslayouter.
* Uppnå kolumnkontroll.

Beroende på vilket projekt du arbetar med kan Layoutbehållaren användas som standardstyckesystem för sidorna eller som en komponent som kan läggas till på sidan via komponentwebbläsaren (eller båda).

>[!TIP]
>
>Adobe tillhandahåller [GitHub-dokumentation](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) av den responsiva layouten som en referens som kan ges till gränssnittsutvecklare så att de kan använda det AEM rutnätet utanför AEM, till exempel när de skapar statiska HTML-modeller för en framtida AEM.

>[!NOTE]
>
>Användningen av ovanstående mekanismer aktiveras av mallens konfiguration. Mer information finns i Konfigurera responsiv layout. <!-- Use of the above mechanisms is enabled by configuration on the template. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.-->

## Layoutdefinitioner, enhetsemulering och brytpunkter {#layout-definitions-device-emulation-and-breakpoints}

När du skapar webbplatsinnehåll vill du se till att innehållet visas på rätt sätt för den enhet som används för att visa det.

Med AEM kan du definiera layouter beroende på enhetens bredd:

* Med emulatorn kan du emulera dessa layouter på en mängd olika enheter. Förutom enhetstypen är orienteringen vald av **Rotera enhet** kan påverka den markerade brytpunkten när bredden ändras.
* Brytpunkter är de punkter som skiljer layoutdefinitionerna åt.
   * De definierar effektivt den maximala bredden (i pixlar) för alla enheter med en viss layout.
   * Brytpunkterna är vanligtvis giltiga för ett urval enheter, beroende på vilken bredd de visas på.
   * Intervallet för en brytpunkt sträcker sig åt vänster till nästa brytpunkt.
   * Du kan inte markera brytpunkten specifikt. Om du väljer en enhet och orientering väljs automatiskt rätt brytpunkt.

Enheten **Skrivbord**, som inte har någon specifik bredd, relaterar till standardbrytpunkten (d.v.s. allt ovanför den senast konfigurerade brytpunkten).

>[!NOTE]
>
>Det skulle vara möjligt att definiera brytpunkter för varje enskild enhet, men detta skulle drastiskt öka den insats som krävs för att definiera och underhålla layout.

När du använder emulatorn väljer du en specifik enhet för emulerings- och layoutdefinition och den relaterade brytpunkten markeras också. Alla layoutändringar du gör gäller för andra enheter som brytpunkten gäller för. Det vill säga alla enheter som är placerade till vänster om den aktiva brytpunktsmarkören, men före nästa brytpunktsmarkör.

När du t.ex. väljer enheten **iPhone 6 Plus** (definierat med en bredd på 540 pixlar) för emulering och layout, brytpunkten **Telefon** (definierat som 768 pixlar) aktiveras också. Alla layoutändringar du gör för **IPHONE 6** är tillämpliga på andra enheter enligt **Telefoner** brytpunkt, som **IPHONE 5** (definierat som 320 pixlar).

![Emulatorer](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Välja en enhet som ska emuleras {#selecting-a-device-to-emulate}

1. Öppna den sida du vill redigera. Till exempel:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Välj **Emulator** ikonen i det övre verktygsfältet:

   ![Emulatorknapp](/help/sites-cloud/authoring/assets/emulator.png)

1. Emulatorverktygsfältet öppnas.

   ![Verktygsfältet Emulator](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   Emulatorverktygsfältet innehåller ytterligare layoutalternativ:

   * **Rotera enhet** - Du kan rotera en enhet från lodrät (stående) orientering till vågrät (liggande) orientering och tvärtom.

   ![Rotera enhetens liggande knapp](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Rotera enhetens stående knapp](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Välj enhet** - Definiera en specifik enhet som ska emuleras från en lista (mer information finns i nästa steg)

   ![Välj enhetsknapp](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Om du vill välja en specifik enhet som ska emuleras kan du antingen:

   * Använd ikonen Välj enhet och välj i en nedrullningsbar väljare.
   * Markera enhetsindikatorn i emulatorns verktygsfält.

   ![Listrutan Välj enhet](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. När en viss enhet har valts kan du:

   * Se den aktiva markören för den valda enheten, till exempel **iPad.**
   * Se den aktiva markören för lämplig [brytpunkt](#layout-definitions-device-emulation-and-breakpoints) som **Tablet.**
   * Den blå prickade linjen representerar *vika* för den valda enheten (här en **iPhone 6 Plus** i liggande).

   ![Flödet](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * Flödet kan också betraktas som sidradbrytningen (ska inte blandas ihop med [brytpunkter](#layout-definitions-device-emulation-and-breakpoints)) för innehållet. Detta visas för att underlätta för användaren att visa vilken del av innehållet som visas på enheten innan det rullas.
   * Flödets linje visas inte om höjden på den enhet som emuleras är högre än skärmstorleken.
   * Flödet visas för författarens bekvämlighet och visas inte på den publicerade sidan.

## Lägga till en layoutbehållare och dess innehåll (redigeringsläge) {#adding-a-layout-container-and-its-content-edit-mode}

A **Layoutbehållare** är ett styckesystem som

* Innehåller andra komponenter.
* Definierar layouten.
* Svar på ändringar.

>[!NOTE]
>
>Om den inte redan är tillgänglig **Layoutbehållare** måste aktiveras explicit för ett styckesystem/en styckesida. <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->

1. **Layoutbehållaren** är tillgänglig som en standardkomponent i [komponentläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Härifrån kan du dra den till önskad plats på sidan där du kan se **Dra komponenter hit** platshållare.
1. Du kan sedan lägga till komponenter i layoutbehållaren. De här komponenterna innehåller det faktiska innehållet:

   ![Layoutbehållare](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Markera och vidta åtgärder på en layoutbehållare (redigeringsläge) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Precis som med andra komponenter kan du markera och sedan agera på (klippa ut, kopiera, ta bort) en layoutbehållare (när de är **Redigera** läge):

>[!CAUTION]
>
>När en layoutbehållare är ett styckesystem tas både layoutstödrastret och alla komponenter (och deras innehåll) som finns i behållaren bort om komponenten tas bort.

1. Om du håller muspekaren över eller trycker på platshållaren för stödrastret visas åtgärdsmenyn.

   ![Lägg till i layoutbehållaren](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   Du måste välja **Överordnad** alternativ.

   ![Överordnad knapp](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Om layoutkomponenten är kapslad väljer du **Överordnad** Med det här alternativet visas en listruta där du kan välja den kapslade layoutbehållaren eller dess överordnade.

   När du för musen över behållarnamnen i listrutan visas deras konturer på sidan.

   * Den lägsta kapslade layoutbehållaren visas med blå kontur.
   * Varje efterföljande behållare kontureras med en ljusare nyans av blått.

   ![Kapslade behållare](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. Hela stödrastret markeras med dess innehåll. Åtgärdsverktygsfältet visas, där du kan välja en åtgärd som t.ex. **Ta bort.**

## Definiera layouter (layoutläget) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Du kan definiera en separat layout för varje [brytpunkt](#layout-definitions-device-emulation-and-breakpoints) (enligt emulerad enhetstyp och orientering).

Om du vill konfigurera layouten för ett responsivt rutnät som implementeras med layoutbehållaren måste du använda **Layout** läge.

**Layout** kan startas på två sätt.

* Genom att använda [lägesmenyn i verktygsfältet](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) och välja **layoutläget**
   * Välj **layoutläget** på samma sätt som du växlar till **redigeringsläget** eller **målinriktningsläget**.
   * **Layoutläget** är beständigt och du lämnar inte **layoutläget** förrän du väljer ett annat läge med lägesväljaren.
* När [redigera en enskild komponent](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout).
   * Genom att använda **Layout** på komponentens snabbåtgärdsmeny kan du växla till **Layout** läge.
   * **Layout** läget kvarstår när komponenten redigeras och återgår till **Redigera** när fokus ändras till en annan komponent.

I layoutläget kan du utföra olika åtgärder på ett rutnät:

* Ändra storlek på innehållskomponenterna med de blå punkterna. Storleksändring fästs alltid mot stödrastret. När du ändrar storlek visas bakgrundsstödrastret som stöd för justering:

  ![Ändra storlek på komponenter](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

  >[!NOTE]
  >
  >Proportioner och proportioner bevaras när komponenter som **Bilder** storleksändras.

* Markera en innehållskomponent och i verktygsfältet kan du:
   * **Överordnad** - Gör att du kan markera hela layoutbehållarkomponenten för att utföra en åtgärd i sin helhet.
   * **Flyt till ny rad** - Komponenten flyttas till en ny rad, beroende på vilket utrymme som är tillgängligt i stödrastret.
   * **Dölj komponent** - Komponenten är osynlig (den kan återställas från verktygsfältet i layoutbehållaren).

  ![Dölj komponent](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* I **Layout** det läge du kan välja **Dra komponenter hit** om du vill markera hela komponenten. Verktygsfältet visas för det här läget.

  Verktygsfältet har olika alternativ beroende på layoutkomponentens läge och vilka komponenter som tillhör det. Till exempel:

   * **Överordnad** - Markera den överordnade komponenten.

     ![Överordnad knapp](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Visa dolda komponenter** - Visa alla eller enskilda komponenter. Numret visar hur många dolda komponenter det finns för närvarande. Räknaren visar hur många komponenter som är dolda.

     ![Knappen Visa dolda komponenter](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Återställ brytpunktslayout** - Återgå till standardlayout. Ingen anpassad layout används.

     ![Återställ brytpunktslayoutknappen](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Flyt till ny rad** - Flytta komponenten uppåt en position om avstånd tillåter.

     ![Knappen Flyt till en ny rad](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Dölj komponent** - Dölj den aktuella komponenten.

     ![Dölj komponentknapp](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)

  >[!NOTE]
  >
  >I exemplet ovan är åtgärderna float och hide tillgängliga eftersom den här layoutbehållaren är kapslad i en överordnad layoutbehållare.

   * **Visa komponenter**
Välj de överordnade komponenterna för att visa åtgärdsverktygsfältet med **Visa dolda komponenter** alternativ. I det här exemplet är två komponenter dolda.

     ![Visa komponenter](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)

  Om du väljer alternativet **Visa dolda komponenter** visas de dolda komponenterna i blått i sina ursprungliga positioner.

  ![Knappen Återställ alla](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

  Markera **Återställ alla** visar alla dolda komponenter.

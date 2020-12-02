---
title: Responsiv layout
description: AEM gör att du kan förverkliga en responsiv layout för dina sidor
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 7%

---


# Responsiv layout {#responsive-layout}

AEM gör att du kan ha en responsiv layout för dina sidor med komponenten **Layoutbehållare**.

Detta tillhandahåller ett styckesystem som gör att du kan placera komponenter i ett responsivt rutnät. Rutnätet kan ändra layouten beroende på enhetens/fönstrets storlek och format. Komponenten används tillsammans med [**layoutläget**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes), som gör att du kan skapa och redigera din responsiva layout beroende på enhet.

Layoutbehållaren:

* Tillhandahåller vågrät fäst mot rutnät, tillsammans med möjligheten att placera komponenter i rutnätet sida vid sida och definiera när de ska komprimeras/omformas.
* Använder fördefinierade brytpunkter (t.ex. för telefon, surfplatta osv.) så att du kan definiera vad som krävs för innehåll för relaterade enheter/orientering.
   * Du kan till exempel anpassa komponentstorleken eller om komponenten kan visas på särskilda enheter.
* Kan kapslas så att kolumnkontroll tillåts.

Användaren kan sedan se hur innehållet återges för specifika enheter med emulatorn.

AEM realiserar responsiv layout för dina sidor med en kombination av mekanismer:

* [**Layout**](#adding-a-layout-container-and-its-content-edit-mode) Container-komponent

   Den här komponenten är tillgänglig i [komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) och innehåller ett rutnätsstyckesystem där du kan lägga till och placera komponenter i ett responsivt rutnät. Den kan också anges som standardstyckesystem på sidan.

* [**Layoutläge**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

   När layoutbehållaren har placerats på sidan kan du använda läget **Layout** för att placera innehåll i det responsiva rutnätet.

* [****](#selecting-a-device-to-emulate)
EmulatorMed den här funktionen kan du skapa och redigera responsiva webbplatser som ordnar om layouten enligt enhetens/fönstrets storlek genom att ändra storlek på komponenterna interaktivt. Användaren kan sedan se hur innehållet återges med emulatorn.

Med dessa responsiva rutnätsmekanismer kan du:

* Använd brytpunkter för att definiera olika innehållslayouter baserat på enhetens bredd (relaterat till enhetstyp och orientering).
* Använd samma brytpunkter och innehållslayouter för att säkerställa att innehållet är anpassat till storleken på webbläsarfönstret på skrivbordet.
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

AEM gör att du kan definiera layouter beroende på enhetens bredd:

* Med emulatorn kan du emulera dessa layouter på en mängd olika enheter. Förutom enhetstypen kan orienteringen, som väljs med alternativet **Rotera enhet**, påverka brytpunkten som markeras när bredden ändras.
* Brytpunkter är de punkter som skiljer layoutdefinitionerna åt.
   * De definierar effektivt den maximala bredden (i pixlar) för alla enheter med en viss layout.
   * Brytpunkterna är vanligtvis giltiga för ett urval enheter, beroende på vilken bredd de visas på.
   * Intervallet för en brytpunkt sträcker sig åt vänster till nästa brytpunkt.
   * Du kan inte markera brytpunkten specifikt. Om du väljer en enhet och orientering väljs automatiskt rätt brytpunkt.

Enheten **Skrivbord**, som inte har någon specifik bredd, relaterar till standardbrytpunkten (d.v.s. allt ovanför den senast konfigurerade brytpunkten).

>[!NOTE]
>
>Det skulle vara möjligt att definiera brytpunkter för varje enskild enhet, men detta skulle drastiskt öka den insats som krävs för att definiera och underhålla layout.

När du använder emulatorn väljer du en specifik enhet för emulerings- och layoutdefinition och den relaterade brytpunkten markeras också. Alla layoutändringar du gör gäller för andra enheter som brytpunkten gäller för, dvs. enheter som är placerade till vänster om den aktiva brytpunktsmarkören, men före nästa brytpunktsmarkör.

När du t.ex. väljer enheten **iPhone 6 Plus** (definierad med en bredd på 540 pixlar) för emulering och layout, aktiveras även brytpunkten **Telefon** (definierad som 768 pixlar). Alla layoutändringar du gör för **iPhone 6** gäller för andra enheter under brytpunkten **Telefoner**, till exempel **iPhone 5** (definieras som 320 pixlar).

![Emulatorer](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Välja en enhet som ska emuleras {#selecting-a-device-to-emulate}

1. Öppna den sida du vill redigera. Till exempel:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Välj ikonen **Emulator** i det övre verktygsfältet:

   ![Emulatorknapp](/help/sites-cloud/authoring/assets/emulator.png)

1. Emulatorverktygsfältet öppnas.

   ![Verktygsfältet Emulator](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   Emulatorverktygsfältet innehåller ytterligare layoutalternativ:

   * **Rotera enhet**  - Gör att du kan rotera en enhet från lodrät (stående) orientering till vågrät (liggande) orientering och tvärtom.

   ![Rotera enhetens liggande knapp](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Rotera enhetens stående knapp](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Välj Enhet**  - Definiera en specifik enhet som ska emuleras från en lista (se nästa steg för mer information)

   ![Välj enhetsknapp](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Om du vill välja en specifik enhet som ska emuleras kan du antingen:

   * Använd ikonen Välj enhet och välj i en nedrullningsbar väljare.
   * Tryck/klicka på enhetsindikatorn i emulatorns verktygsfält.

   ![Listrutan Välj enhet](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. När en viss enhet har valts kan du:

   * Se den aktiva markören för den valda enheten, till exempel **iPad.**
   * Se den aktiva markören för rätt [brytpunkt](#layout-definitions-device-emulation-and-breakpoints), t.ex. **surfplatta.**
   * Den blå prickade linjen representerar *vikningen* för den valda enheten (här en **iPhone 6 Plus** i liggande).

   ![Flödet](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * Flödet kan också betraktas som sidradbrytningen (ska inte blandas ihop med [brytpunkterna](#layout-definitions-device-emulation-and-breakpoints)) för innehållet. Detta visas för att underlätta för användaren att visa vilken del av innehållet som kommer att visas på enheten före rullning.
   * Flödets linje visas inte om höjden på den enhet som emuleras är högre än skärmstorleken.
   * Flödet visas för författarens bekvämlighet och visas inte på den publicerade sidan.


## Lägga till en layoutbehållare och dess innehåll (redigeringsläge) {#adding-a-layout-container-and-its-content-edit-mode}

En **layoutbehållare** är ett styckesystem som:

* Innehåller andra komponenter.
* Definierar layouten.
* Svar på ändringar.

>[!NOTE]
>
>Om den inte redan är tillgänglig måste **layoutbehållaren** aktiveras explicit för ett styckesystem/en styckesida. <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->

1. **Layoutbehållaren** är tillgänglig som en standardkomponent i [komponentläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Härifrån kan du dra den till önskad plats på sidan och sedan ser du platshållaren **Dra komponenter hit**.
1. Du kan sedan lägga till komponenter i layoutbehållaren. De här komponenterna innehåller det faktiska innehållet:

   ![Layoutbehållare](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Markera och vidta åtgärder på en layoutbehållare (redigeringsläge) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Precis som med andra komponenter kan du markera och sedan vidta åtgärder för (klippa ut, kopiera, ta bort) en layoutbehållare (i **redigeringsläget**):

>[!CAUTION]
>
>När en layoutbehållare är ett styckesystem tas både layoutstödrastret och alla komponenter (och deras innehåll) som finns i behållaren bort om komponenten tas bort.

1. Om du för musen över eller trycker på platshållaren för stödrastret visas åtgärdsmenyn.

   ![Lägg till i layoutbehållaren](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   Du måste välja alternativet **Överordnad**.

   ![Överordnad knapp](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Om layoutkomponenten är kapslad och du väljer alternativet **Överordnad** visas en listruta där du kan välja den kapslade layoutbehållaren eller dess överordnade.

   När du för musen över behållarnamnen i listrutan visas deras konturer på sidan.

   * Den lägsta kapslade layoutbehållaren visas med blå kontur.
   * Varje efterföljande behållare linjeras med en ljusare nyans av blått.

   ![Kapslade behållare](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. Då markeras hela stödrastret med dess innehåll. Åtgärdsverktygsfältet visas, där du kan välja en åtgärd som t.ex. **Ta bort.**

## Definiera layouter (layoutläget) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Du kan definiera en separat layout för varje [brytpunkt](#layout-definitions-device-emulation-and-breakpoints) (utifrån emulerad enhetstyp och orientering).

Om du vill konfigurera layouten för ett responsivt rutnät som implementeras med layoutbehållaren måste du använda läget **Layout**.

**Du kan starta** layoutläget på två sätt.

* Genom att använda [lägesmenyn i verktygsfältet](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) och välja **layoutläget**
   * Välj **layoutläget** på samma sätt som du växlar till **redigeringsläget** eller **målinriktningsläget**.
   * **Layoutläget** är beständigt och du lämnar inte **layoutläget** förrän du väljer ett annat läge med lägesväljaren.
* När [redigerar en enskild komponent.](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)
   * Genom att använda alternativet **Layout** i komponentens snabbåtgärdsmeny kan du växla till läget **Layout**.
   * **Layoutläget** kvarstår när komponenten redigeras och återgår till  **** redigeringsläget när fokus har ändrats till en annan komponent.

I layoutläget kan du utföra olika åtgärder på ett rutnät:

* Ändra storlek på innehållskomponenterna med de blå punkterna. Storleksändring fästs alltid mot stödrastret. När du ändrar storlek på bakgrundsstödrastret visas det för att underlätta justeringen:

   ![Ändra storlek på komponenter](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

   >[!NOTE]
   >
   >Proportioner och proportioner bevaras när komponenterna som **Bilder** storleksändras.

* Klicka/peka på en innehållskomponent så kan du göra följande i verktygsfältet:
   * **Överordnad**  - Gör att du kan markera hela layoutbehållarkomponenten för att utföra en åtgärd i sin helhet.
   * **Flyt till ny rad**  - Komponenten flyttas till en ny rad, beroende på vilket utrymme som är tillgängligt i stödrastret.
   * **Dölj komponent** - Komponenten blir osynlig (den kan återställas från layoutbehållarens verktygsfält).

   ![Dölj komponent](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* I **Layout**-läget kan du trycka/klicka på **Dra komponenter hit** för att markera hela komponenten. Då visas verktygsfältet för det här läget.

   Verktygsfältet har olika alternativ beroende på layoutkomponentens läge och vilka komponenter som tillhör det. Till exempel:

   * **Överordnad**  - Välj den överordnade komponenten.

      ![Överordnad knapp](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Visa dolda komponenter**  - Visa alla eller enskilda komponenter. Numret visar hur många dolda komponenter det finns för närvarande. Räknaren visar hur många komponenter som är dolda.

      ![Knappen Visa dolda komponenter](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Återställ brytpunktslayout**  - Återgå till standardlayout. Det innebär att ingen anpassad layout kommer att användas.

      ![Återställ brytpunktslayoutknapp](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Flyt till ny rad**  - Flytta komponenten uppåt till en position om avstånd tillåter.

      ![Knappen Flyt till en ny rad](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Dölj komponent** - Dölj den aktuella komponenten.

      ![Dölj komponentknapp](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)
   >[!NOTE]
   >
   >I exemplet ovan är åtgärderna float och hide tillgängliga eftersom den här layoutbehållaren är kapslad i en överordnad layoutbehållare.

   * **Visa**
komponenterMarkera de överordnade komponenterna för att visa åtgärdsverktygsfältet med 
**Visa dolda** komponenter, alternativ. I det här exemplet är två komponenter dolda.

      ![Visa komponenter](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)
   Om du väljer alternativet **Visa dolda komponenter** visas de dolda komponenterna i blått i sina ursprungliga positioner.

   ![Knappen Återställ alla](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

   Om du väljer **Återställ alla** visas alla dolda komponenter.

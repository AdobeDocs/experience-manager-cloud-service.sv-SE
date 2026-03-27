---
title: Anpassa adaptiva formulärteman med Theme Editor
description: Lär dig hur du använder Theme Editor för att skapa och anpassa visuella teman för Core Component-baserad Adaptive Forms i Adobe Experience Manager.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: f1b318803b9b854ec2ce800670f6484799113599
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 0%

---


# Anpassa formulärteman {#customizing-form-themes}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html) |
| AEM as a Cloud Service | Den här artikeln |

Theme Editor i Adobe Experience Manager (AEM) Forms är ett visuellt gränssnitt där du kan skapa och anpassa teman för din adaptiva Forms utan att behöva skriva kod manuellt. Ett tema definierar utseendet på formulärkomponenter och paneler, inklusive bakgrundsfärger, teckensnittsformat, kanter, dimensioner och mellanrum. När du använder ett tema återspeglas de angivna formaten i motsvarande komponenter, och du kan återanvända samma tema i flera adaptiva Forms.

Med Theme Editor slipper du skapa en dedikerad utvecklarprofil för grundläggande formulärformatering. Med bara en fungerande kunskap om CSS kan du formatera formulär med den visuella sidofältet eller skriva avancerade CSS-åsidosättningar direkt i redigeraren.

## Förutsättningar {#prerequisites}

* Behörigheter på författarnivå i Adobe Experience Manager Forms.
* Grundläggande förståelse för CSS-formateringsprinciper. En fullständig CSS-referens finns i [MDN Web Docs CSS-referensen](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

## Navigera till temamappen {#navigate-to-themes}

1. Logga in på din AEM-författarinstans.
1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Themes]**.

   I katalogen Teman visas alla tillgängliga teman, inklusive alla standardteman från AEM Canvas, tillsammans med anpassade teman som du eller din organisation har skapat.

### Skapa ett nytt tema {#create-a-new-theme}

1. I katalogen Teman väljer du den mapp där du vill spara det nya temat.
1. Klicka på **[!UICONTROL Create]** > **[!UICONTROL Theme]**.

   ![Skapa nytt tema](/help/forms/assets/custom-theme-create.png)

1. Ange följande information i dialogrutan **[!UICONTROL Create Theme]**:
   * **[!UICONTROL Title]**: En beskrivande rubrik för temat.
   * **[!UICONTROL Name]**: Temats nodnamn.
   * **[!UICONTROL Adaptive form to preview the theme]**: Välj ett Core Component-baserat adaptivt formulär för ett Core Component-tema. **[!UICONTROL Use default adaptive form]** använder en grundläggande adaptiv form, inte kärnkomponenter. Det markerade formuläret visas på arbetsytan i temeredigeraren för förhandsgranskning i realtid medan du redigerar.
   * **[!UICONTROL Description]** *(Valfritt)*: En kort beskrivning av temat.
   * **[!UICONTROL Configuration Container]** *(Valfritt)*: Konfigurationsbehållaren som innehåller konfigurationsinformation för Adobe Font.
   * **[!UICONTROL Tags]** *(Valfritt)*: Taggar kopplade till temat för identifiering och sökning.
1. Klicka på **[!UICONTROL Create]**.

   ![konfigurerar anpassat tema](/help/forms/assets/custom-theme-name.png)

   Temat skapas. Du kan nu klicka på **[!UICONTROL Edit]** för att öppna den i temeredigeraren.

### Redigera ett befintligt tema {#edit-an-existing-theme}

1. I katalogen **Teman** väljer du det tema som du vill ändra.
1. Klicka på **[!UICONTROL Edit]** i åtgärdsfältet för att öppna temat i temeredigeraren.

   ![Redigera ett tema](/help/forms/assets/custom-theme-edit.png)

### Överför ett tema {#upload-a-theme}

Du kan importera ett temapaket (till exempel ett som har exporterats från en annan miljö) till temakatalogen:

1. I katalogen **Themes** klickar du på **[!UICONTROL Create]** > **[!UICONTROL File Upload]**.
1. Bläddra till och välj temapaketet (ZIP-fil) på datorn och klicka sedan på **[!UICONTROL Upload]**.

   ![Överför tema - Skapa meny med alternativet Filöverföring](/help/forms/assets/custom-theme-upload.png)

Det överförda temat visas i katalogen Teman och kan redigeras som vilket tema som helst.

### Hämta ett tema {#download-a-theme}

Du kan exportera ett tema som ett paket (ZIP-fil) och återanvända det i en annan AEM Forms-miljö eller säkerhetskopiera det:

1. Välj ett eller flera teman i katalogen **Teman** (använd kryssrutorna på temakorten).
1. Klicka på **[!UICONTROL Download]** i åtgärdsfältet. En dialogruta kan visas med information om de valda temana.
1. Bekräfta eller klicka på **[!UICONTROL Download]** i dialogrutan. Temapaketet hämtas som en ZIP-fil till datorn.

   ![Hämta tema - välj tema och klicka på Hämta](/help/forms/assets/custom-theme-download.png)

Du kan överföra den här ZIP-filen senare med [Överför ett tema](#upload-a-theme) i samma eller en annan miljö.

## Förstå gränssnittet för Theme Editor {#understand-the-theme-editor}

När du öppnar ett tema i Theme Editor visas två huvudområden:

![Temeredigeraren](/help/forms/assets/custom-theme-editor.png)

* **Arbetsyta** (höger sida): Visar en förhandsgranskning av det adaptiva formuläret som är länkat till temat. Alla formatändringar återspeglas här direkt, så du kan se effekten av dina redigeringar i realtid.
* **Sidofält** (vänster sida): Innehåller panelen **Väljare** som listar alla formaterbara formulärkomponenter i en trädstruktur, till exempel Sida, Formulär, Fält, Knapp, Panel, Bild, Hämta och reCaptcha.

### Verktygsfältet Arbetsyta {#canvas-toolbar}

![Verktygsfältet för arbetsytan i temaredigeraren med alternativen Växla sida vid sida, Ångra, Gör om, Emulator, Redigera/Förhandsgranska och Tema &#x200B;](/help/forms/assets/custom-theme-toolbar-utilities.png)

Från vänster till höger:
* **A: Växla sidopanel**: Visa eller dölj sidofältet för väljare. Använd det här alternativet om du vill maximera förhandsvisningsområdet för formuläret när du vill fokusera på arbetsytan, eller visa sidofältet igen när du behöver markera eller formatera komponenter.
* **B: Temaalternativ** (listruta): Öppnar en meny med fyra alternativ. Klicka på den när du behöver ändra förhandsgranskningsformuläret, visa CSS, hantera sparade format eller få hjälp i redigeraren. När du öppnar listrutan Temaalternativ visas:

  ![Listrutan Temaalternativ som visar Konfigurera, Visa tema-CSS, Hantera format och Hjälp](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL Configure]**: Byt det formulär som visas på arbetsytan till ett annat anpassat formulär. Använd detta för att kontrollera hur temat ser ut på ett annat formulär utan att lämna redigeraren.
     ![Konfigurera anpassat formulär för förhandsgranskning av tema](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL View Theme CSS]**: Öppna en dialogruta med fullständig kompilerad CSS för temat. Om du bara vill se CSS för den markerade komponenten använder du **[!UICONTROL View CSS]** i sidofältet i stället (praktisk för att felsöka eller kopiera regler).
     ![Visa slutlig CSS](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL Manage Styles]**: Öppna dialogrutan för att spara, namnge och återanvända text- och bildformat. Sparade format kan användas på andra komponenter. Nyligen använda format kan också visas för snabb återanvändning.
   * **[!UICONTROL Help]**: Starta den guidade genomgången av temeredigeraren.
* **C: Ångra/Gör om**: Återgå eller återanvänd dina senaste formatändringar. Användbart om du provar ett format och vill gå tillbaka utan att förlora andra redigeringar.
* **D: Emulator**: Välj en enhet eller brytpunkt (till exempel Skrivbord, Surfplatta eller Mobil) om du vill förhandsgranska formuläret med den skärmstorleken. Förhandsgranskningen av formuläret ändrar storlek så att det matchar den markerade brytpunkten. Alla format som du anger när en brytpunkt är markerad tillämpas bara på brytpunkten, så att du kan definiera responsiva format. Mer information finns i [Format för olika skärmstorlekar](#styling-for-different-screen-sizes).
* **E: Redigera/förhandsgranska**: Växla mellan två lägen. **Redigera** är standard: du kan klicka på komponenter på arbetsytan för att markera dem och ändra deras format i sidofältet. **Förhandsgranska** visar formuläret så som en slutanvändare skulle kunna se det utan markeringsgränser, komponentetiketter eller formatmallens sidofält, så att du kan kontrollera hur temaformuläret ser ut och fungerar innan det publiceras.

<!--**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).-->

### Formatera en komponent

Du kan markera en komponent som du vill formatera på två sätt:
* **Från arbetsytan**: Klicka direkt på en komponent i formuläret (till exempel ett textfält, en knapp eller en listruta). Det markerade elementet markeras med en ram och en komponentetikett (till exempel &quot;Textinmatningswidget&quot;) visas ovanför det. Formateringsalternativen för den komponenten visas i sidofältet.

  ![Redigera tema från arbetsytan](/help/forms/assets/custom-theme-field-level.png)

* **Från panelen Väljare**: Använd trädstrukturen i det vänstra sidofältet för att gå ned i specifika komponenter. Expandera till exempel **[!UICONTROL Field]** > **[!UICONTROL Widget]** > **[!UICONTROL Text Input]** för att ange textrutewidgeten som mål.

  ![Redigera tema från panelen Väljare](/help/forms/assets/custom-theme-selector.png)

#### Använda format på en komponent {#apply-styles-to-a-component}

När en komponent är markerad visas de tillgängliga formategenskaperna i sidofältet ordnade i följande kategorier:

* **[!UICONTROL Dimensions & Position]**: Styr justering, storlek, utfyllnad, marginal, bredd, höjd och Z-index.
* **[!UICONTROL Text]**: Konfigurera teckensnittsfamilj, vikt, färg, storlek, radhöjd, justering, teckenavstånd, textdekoration och omformning. En fullständig lista över CSS-textegenskaper som stöds finns i [MDN CSS-textdokumentationen](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text).
* **[!UICONTROL Background]**: Ange en bakgrundsfärg, bild eller övertoning. Se [MDN CSS-bakgrunder &#x200B;](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders).
* **[!UICONTROL Border]**: Definiera kantlinjebredd, stil, radie och färg.
* **[!UICONTROL Effects]**: Lägg till opacitet, blandningslägen och skuggor.

Så här använder du ett format:

1. Markera komponenten på arbetsytan eller på panelen Väljare.
1. Ange önskade visuella egenskaper i sidofältet. Välj till exempel en **[!UICONTROL Background Color]** och justera **[!UICONTROL Font Color]**.
1. Klicka på bockmarkeringsikonen **[!UICONTROL OK]** för att bekräfta egenskapsändringen.

   ![Använder format](/help/forms/assets/custom-theme-applying-style.png)

<!--#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.-->

### Formatering på formulärnivå {#form-level-styling}

Med formatering på formulärnivå tillämpas formatet i stort sett på alla komponenter av samma typ. Om du till exempel väljer **[!UICONTROL Field]** på panelen **Väljare** och anger en bakgrundsfärg som blå, ärver alla fält i formuläret (textrutor, numeriska rutor, datumväljare och nedrullningsbara listor) den blå bakgrunden.

**Exempel:** Så här anger du en enhetlig bakgrundsfärg för alla fält i formuläret:

1. Välj **på panelen** Väljare **[!UICONTROL Field]**.
1. I sidofältet anger du **[!UICONTROL Background Color]** till blå.
1. Klicka på **[!UICONTROL OK]**.

   ![Formatering på formulärnivå](/help/forms/assets/custom-theme-form-level-styling.png)

Alla fältkomponenter i formuläret visas nu med en blå bakgrund.

### Formatering på komponentnivå {#component-level-styling}

Formatering på komponentnivå avser en viss komponenttyp och åsidosätter ett bredare format på formulärnivå. Om du till exempel bara vill att widgeten Textruta ska ha en annan bakgrundsfärg medan alla andra fält ska vara blå, anger du textrutewidgeten som mål.

**Exempel:** Så här anger du en grön bakgrund och ett lila teckensnitt på enbart textrutewidgeten:

1. Expandera **[!UICONTROL Field]** > **[!UICONTROL Widget]** > **[!UICONTROL Text Input]** på panelen Väljare.
1. Ställ in **[!UICONTROL Font Color]** på lila.
   ![Formatering på fältnivå](/help/forms/assets/custom-theme-field-level-styling1.png)
1. Ställ in **[!UICONTROL Background Color]** på grönt.
   ![Formatering på fältnivå](/help/forms/assets/custom-theme-field-level-styling2.png)
1. Klicka på **[!UICONTROL OK]**.

Widgeten Textruta visar nu en grön bakgrund med lila text, medan alla andra fält förblir blå på formulärnivå.

>[!NOTE]
>
> **Formatering på komponentnivå har alltid högre prioritet än formatering på formulärnivå.** När ett format definieras på båda nivåerna åsidosätter den mer specifika väljaren på komponentnivå den bredare väljaren på formulärnivå. Detta följer standard [CSS-specificitetsregler](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity). Om du till exempel anger en blå bakgrund i alla fält (formulärnivå) och en grön bakgrund i textrutewidgeten (komponentnivå) visas en grön bakgrund i textrutan.

## Formatera för olika skärmstorlekar {#styling-for-different-screen-sizes}

Du kan definiera olika format för olika enhetsstorlekar så att temat är responsivt. I verktygsfältet för temeredigeraren visas **enhetsalternativ** (till exempel iPhone 5, iPad, Skrivbord, Surfplatta, Mindre skärm) för att förhandsgranska och formatera formuläret med den skärmstorleken.

1. Använd **enhetsemulatorn** i verktygsfältet på arbetsytan: klicka på någon av enhetsetiketterna (till exempel **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]**, **[!UICONTROL iPad]**, **[!UICONTROL Smaller Screen]**). En linjal ovanför formuläret visar den valda enhetens pixelbredd.
1. När den enheten är markerad använder du sidofältet för att ställa in eller justera format. Formaten gäller bara för den valda enhetsvyn.
1. Växla till en annan enhet och definiera format för den efter behov.
1. Klicka på **[!UICONTROL OK]** och spara temat när du är klar.

   ![Enhetsemulatorn i temeredigeraren - linjaler och enhetsalternativ (Skrivbord, Surfplatta, iPad, Mindre skärm)](/help/forms/assets/custom-theme-emulator.png)

Samma tema kan därför ha olika mellanrum, teckenstorlekar eller layoutrelaterade format per enhet, vilket matchar [AEM 6.5 Theme Editor-beteendet](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html) för responsiv formatering.

## Använd avancerade CSS-åsidosättningar {#use-advanced-css-overrides}

För format som inte är tillgängliga via den visuella sidofältet kan du skriva anpassad CSS direkt i redigeraren.

1. Markera komponenten.
1. Expandera avsnittet **[!UICONTROL Advanced]** i sidlisten.
1. Skriv dina anpassade CSS-regler i området **[!UICONTROL CSS Override]**. Dessa regler åsidosätter alla egenskaper som anges via de visuella kontrollerna om det finns en konflikt.

En fullständig CSS-egenskapsreferens finns i [MDN Web Docs CSS-referensen](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

### Lägg till CSS-pseudoelement {#add-css-pseudo-elements}

Avsnittet **[!UICONTROL Advanced]** har också stöd för CSS-pseudoelement som `::before` och `::after`. Med dessa kan du injicera innehåll eller dekorativa format runt en komponent utan att ändra formulärstrukturen. Så här lägger du till en visuell indikator före en textrutekomponent:

1. Markera komponenten (till exempel `CMP Textbox`).
1. Expandera avsnittet **[!UICONTROL Advanced]**.
1. I pseudoelementfälten i `::before` lägger du till CSS-egenskaper som:

   ```css
   color: #B10DC9;
   ```

   ![Före CSS](/help/forms/assets/custom-theme-before-css.png)

1. I pseudoelementfälten i `::after` lägger du till CSS-egenskaper som:

   ```css
   color: #006400;
   ```

   ![Efter CSS](/help/forms/assets/custom-theme-after-css.png)


Dessa pseudoelement följer standard-CSS-beteende. Mer information finns i [MDN CSS Pseudoelement](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements).

## God praxis {#best-practices}

* **Använd panelen Väljare för exakt målinriktning**: Använd panelen Väljare till vänster i stället för att klicka på arbetsytan när du formaterar kapslade element som en fältetikett eller en lång beskrivning. Detta garanterar att rätt CSS-väljare genereras med rätt specificitet.
* **Undvik resurser från andra teman**: Bläddra inte bland och lägg inte till resurser (till exempel bilder) från andra teman när du redigerar ett tema. Om källtemat flyttas eller tas bort bryts det aktuella temat.
* **Ändra inte behållarpanelens layoutbredd**: Om du anger en fast bredd på behållarpaneler blir de statiska och förhindrar att de anpassas till olika skärmstorlekar.

## Se även {#see-also}

{{see-also}}
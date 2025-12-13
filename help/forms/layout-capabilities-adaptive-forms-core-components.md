---
title: Vilka layoutfunktioner har Adaptive Forms som bygger på kärnkomponenterna?
description: Layout och utseende för Adaptive Forms på olika enheter styrs av layoutinställningarna. Förstå de olika layouterna och hur de ska användas.
feature: Adaptive Forms, Core Components
keywords: Layout för adaptiv form baserad på kärnkomponenter, olika layouter för formulär, dynamiska formulärlayouter AEM, AEM Cloud-formulärlayouter, formulärlayouttyper i AEM Core-komponenter, anpassade formulärlayouter
role: User, Developer, Admin
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# Layoutfunktioner i Adaptive Forms baserat på kärnkomponenter


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html?lang=sv-SE) |
| AEM as a Cloud Service (Foundation Components) | [Klicka här](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service (kärnkomponenter) | Den här artikeln |

Adaptiv Forms innehåller förstklassiga komponenter för effektiv layout och design av blanketterna. Layouten styr hur komponenter visas i ett formulär. Adaptiv Forms har stöd för olika layouter: panel, guide, dragspelspanel, flikar på översta/vågräta flikar samt tabbar på vänster/lodräta flikar.

<!-- ![Types of Layout](/help/forms/assets/generic-layout-hero-image.png){align="center"}-->

## Tillämplighet och användningsfall

### Försäkring

## Har AEM Forms stöd för blanketter för försäkringsanspråk i flera steg?

Ja. AEM Forms har stöd för anpassade blanketter i flera steg med villkorsstyrd logik, vilket gör att försäkringsbolagen kan samla in kravinformation stegvis baserat på anspråkstyp och sammanhang.

## Kan kunderna på ett säkert sätt överföra anspråksdokument med AEM Forms?

Ja. AEM Forms hanterar säker dokumentöverföring som en del av inskickandet av blanketter med åtkomstkontroll och säker datahantering som är anpassad efter företagets säkerhetskrav.

## Förutsättning

Innan du utforskar de olika funktionerna i en layout måste du se till att kärnkomponenterna är aktiverade för din miljö. Installera den senaste versionen för att aktivera adaptiva Forms Core-komponenter för din AEM Cloud-tjänstmiljö.

## Anpassade layouttyper i Forms

Adaptiv form baserad på kärnkomponenter har stöd för följande typer av layouter:

* **Panellayout**
* **Guidelayout**
* **Lodrät layout**
* **Vågrät layout**
* **Dragspelslayout**

>[!BEGINTABS]

>[!TAB Panellayout]

Panelayout är användbart när du vill ordna relaterade fält på ett sätt som gör det enklare att navigera och hitta motsvarande innehåll. Panelayouten ordnar komponenterna inom distinkta avsnitt eller paneler i ett adaptivt format.

![Panellayout](/help/forms/assets/panel-layout.png)

Panellayout

Du kan använda [panelkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) för att lägga till panellayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar olika egenskaper för panelkomponenten finns i artikeln [panelkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

>[!TAB Guidelayout]

Med hjälp av guidelayouten kan du förenkla ett komplext formulär genom att dela upp det i distinkta steg. Varje steg representerar en annan del av processen och användarna navigerar genom stegen sekventiellt, ofta med knapparna **Nästa** och **Föregående** . Du kan använda guidelayouten för att skapa ett formulär som innehåller flera avsnitt eller steg.

![Guidelayout](/help/forms/assets/wizard-layout-compare.gif)

Guidelayout

Du kan använda [guidekomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) för att lägga till guidelayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för guidekomponenten finns i artikeln [wizard component](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

>[!TAB Lodrät tabblayout]

Layouten för de lodräta flikarna kallas även för tabbar i den vänstra layouten. Med den lodräta fliklayouten ordnas paneler och avsnitt längs formulärets vänstra sida. Det är en vanlig layout för formulär där paneler/avsnitt staplas lodrätt för enkel läsning och navigering.

![Lodrät layout](/help/forms/assets/vertical-tab.gif)

Lodrät tabblayout

Du kan använda den [lodräta flikkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) för att lägga till den lodräta tabblayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för komponenten med lodräta flikar finns i artikeln [för komponenten med lodräta flikar](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs).


>[!TAB Vågrät fliklayout]

Layouten för de vågräta flikarna kallas även för Tabbar i den översta layouten. Med den vågräta fliklayouten ordnas paneler eller avsnitt sida vid sida på en rad. I den här layouten visas formuläravsnitten linjärt över formulärets eller panelens bredd.


![Vågrät layout](/help/forms/assets/horizontal-layout.gif)

Vågrät fliklayout

Du kan använda den [vågräta flikkomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) för att lägga till den vågräta tabblayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för den vågräta flikkomponenten finns i artikeln [vågräta flikar](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) .


>[!TAB Dragspelslayout]

Dragspelslayouten visar innehåll i komprimerbara avsnitt eller paneler i ett adaptivt formulär. När ett avsnitt är expanderat visas innehållet i det, medan andra avsnitt förblir komprimerade. Den här layouten är idealisk för att visa stora mängder information i ett kompakt format.

![Dragspelslayout](/help/forms/assets/accordion-layout-compare.gif)

Dragspelets layout

Du kan använda [dragspelskomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) för att lägga till dragspelslayouten i ett formulär. Detaljerade instruktioner om hur du konfigurerar de olika egenskaperna för dragspelskomponenten finns i artikeln om [dragspelskomponenten](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

>[!ENDTABS]

Mer information om hur du infogar en layout och lägger till formulärkomponenter finns i avsnittet [Infoga en layout och lägga till formulärkomponenter i den?](#how-to-insert-a-layout-and-add-form-components-to-it)

### Hur väljer man den rätta anpassade formulärlayouten?

Det är viktigt att välja rätt anpassad formulärlayout för att optimera användarupplevelsen och formulärfunktionerna. Tabellen hjälper dig att förstå de olika layoutalternativen som finns och hjälper dig att välja den lämpligaste layouten baserat på dina specifika behov och användningsexempel:

| Funktion | Panellayout | Guidelayout | Flikar på fliklayouten Överkant/Lodrät | Tabbar på vänster/vågrät tabblayout | Dragspelets layout |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **Syfte** | Grupperar relaterat innehåll i distinkta avsnitt | Hjälper användarna genom en flerstegsprocess eller ett formulär | Möjliggör växling mellan avsnitt/vyer på samma sida | Liknar de övre flikarna, men ordnade lodrätt till vänster | Ordnar innehållet i komprimerbara avsnitt |
| **Struktur** | Distinkta avsnitt | Sekventiella steg/sidor | Vågräta flikar överst | Lodräta tabbar till vänster | Komprimerbara paneler/avsnitt |
| **Navigering** | Klicka på panelrubrikerna för att navigera | - Framåt: Nästa-knappen <br>- Bakåt: Bakåt-knappen <br> - Valfria hoppsteg | Klicka på flikar för att växla avsnitt | Klicka på flikar för att växla avsnitt | Klicka på rubriker för att expandera/komprimera avsnitt |
| **Användarupplevelse** | Organiserar stora mängder innehåll på ett hanterbart sätt | Stegvisa anvisningar som minskar överväldigande | Tydlig, lättillgänglig växling mellan vyer | Effektiv användning av lodrätt utrymme, alltid synliga flikar | Komprimerad vy med expanderade/komprimerade avsnitt |
| **Använd skiftläge** | Komplexa formulär med kategoriserade avsnitt | Konfigurera processer, komplexa formulär | Ordna inställningar eller innehållskategorier | Kontrollpaneler, komplexa datavyer | Vanliga frågor, inställningsmenyer, avsnitt med detaljerat innehåll |


## Hur infogar man en layout och lägger in formulärkomponenter?

Diagrammet nedan visar stegen för att infoga en layout i ett formulär och lägga till formulärkomponenter i det:

![Arbetsflöde för att lägga till en layout och formulärkomponenter](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

Ta en titt på **IT-begärandeformuläret** som visas i avsnittet [Adaptiva Forms-layouttyper](#adaptive-forms-layout-types). Formuläret samlar in information från anställda som har tekniska problem med sitt nätverk eller sin bärbara dator. Den innehåller tre paneler:

* **Information om medarbetare**: Panelen samlar in information om medarbetaren och innehåller tre textrutor med etiketten Namn, E-post-ID och Avdelning.

* **Probleminformation**: Panelen innehåller information om problemet. Den innehåller en kryssruta för problemkategorin med tre alternativ: Nätverk, Dator eller Annan. Den innehåller även två textrutor med etiketten Ange och kommentera.

* **Bifogade filer**: På panelen kan användare överföra stöddokument som är relaterade till problemet.

Låt oss utforska den stegvisa processen för att infoga en layout och lägga till komponenter i den. I det här exemplet infogas en vågrät tabblayout i ett formulär.

### &#x200B;1. Infoga en layoutkomponent i ett formulär

1. Logga in på din [!DNL Experience Manager Forms]-instans.
1. I det övre vänstra hörnet väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Öppna ett befintligt anpassat formulär i redigeringsläge om det redan har skapats.

   ![Öppna ett anpassat formulär](/help/forms/assets/insert-layout.png)

   Du kan också [skapa ett nytt adaptivt formulär](/help/forms/creating-adaptive-form-core-components.md).

1. Leta reda på det avsnitt i formulärbyggaren som gör att du kan lägga till en layout.

   ![Formulärverktyget](/help/forms/assets/form-editor.png)
1. Klicka på ikonen **Lägg till** . Ikonen är ett plustecken (+) som anger att du kan lägga till nya komponenter.

   ![Infoga layout](/help/forms/assets/insert-layout-add-icon.png)

   Om du klickar på ikonen **Lägg till** visas dialogrutan **Infoga ny komponent** som visar olika komponenter som ska infogas.

   >[!NOTE]
   >
   > Du kan också [dra och släppa layoutkomponenten](#extra-bytes).

1. Bläddra bland de tillgängliga komponenterna i dialogrutan och välj önskad layout i listan. I det här fallet väljer vi komponenten Vågräta flikar för att infoga den vågräta tabblayouten.

   ![Markera vågräta flikar](/help/forms/assets/select-horizontal-tab.png)

   När du lägger till den vågräta flikkomponenten i formuläret består den till att börja med av två tomma paneler, som heter Item1 och Item2. Du måste lägga till formulärkomponenter manuellt till dessa paneler.

   ![Vågräta flikar](/help/forms/assets/insert-tabs-on-top.png)

1. Öppna egenskaperna för den vågräta flikkomponenten och ange komponentens namn.
I det här fallet lägger vi till namnet på den horisontella flikkomponenten som IT-frågeformulär.

   ![Lägg till namn för vågräta flikar](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. Klicka på **Klar**.

   ![Vågräta flikar](/help/forms/assets/tabs-on-top-rename-component.png)

När layoutkomponenten har lagts till i formuläret ändrar du antalet paneler enligt kraven.

### &#x200B;2. Lägg till paneler i layouten

Lägg till ny panel i komponenten för vågräta flikar:

1. Öppna de vågräta flikkomponentegenskaperna och klicka på fliken **Objekt** .

   ![Fliken Objekt för vågräta flikar](/help/forms/assets/tabs-on-top-items-tab.png)

1. Klicka på ikonen **Lägg till** för att lägga till en ny panel.

   ![Lägg till ny panel](/help/forms/assets/tabs-on-top-add-panel.png)

   När du klickar på ikonen **Lägg till** visas dialogrutan **Infoga ny komponent** .

1. Markera panelkomponenten.

   ![Lägg till ny panel](/help/forms/assets/tabs-on-top-new-panel.png)

   När du markerar panelkomponenten läggs den nya panelen till i den vågräta layouten.

   ![Lägg till ny panel](/help/forms/assets/tabs-on-top-add-new-panel.png)

   Ange ett namn för den nya panelen, annars kan du inte spara egenskaperna för den vågräta flikkomponenten.

1. Ange namnen på panelerna enligt figuren nedan:

   ![Panelnamn](/help/forms/assets/tabs-on-tops-panel-name.png)

1. Klicka på **Klar**.

   När du klickar på **Klar** visas de tre panelerna sida vid sida i en rad. Panelnamnen visas som rubriker för varje panel, och du kan lägga till formulärkomponenter för varje panel.

   ![Panelnamn](/help/forms/assets/tabs-on-top-initial-view.png)

   Du kan konfigurera panelkomponentens egenskaper. IT-frågeformuläret innehåller till exempel inga paneltitlar. Här är stegen för att konfigurera egenskaper för panelkomponenten.

1. Öppna egenskaperna för den första panelen.

   ![Egenskaper för panel 1](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. Markera kryssrutan **Dölj titel** på fliken **Grundläggande**.

   ![Dölj titel](/help/forms/assets/tabs-on-top-hide-panel.png)

1. Klicka på **Klar**.

På samma sätt kan du dölja titlar för de andra två panelerna. När du är klar kan du fortsätta med att lägga till formulärkomponenter på varje panel.

### &#x200B;3. Lägga till formulärkomponenter på panelen

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. Leta reda på det avsnitt på panelen där du kan lägga till komponenter.
1. Klicka på ikonen **Lägg till** . Ikonen är ett plustecken (+) som anger att du kan lägga till nya komponenter.
   ![Infoga layout](/help/forms/assets/tabs-on-top-add-component.png)

   Om du klickar på ikonen **Lägg till** visas dialogrutan **Infoga ny komponent** som visar olika komponenter som ska infogas.

   ![Dialogrutan Infoga ny komponent](/help/forms/assets/insert-new-component.png)

1. Bläddra bland de tillgängliga komponenterna i dialogrutan som visas och markera önskad komponent. I vårt fall väljer du komponenten Textruta.
1. Öppna egenskaperna för den tillagda komponenten och ange dess namn. Här kan du redigera egenskaperna för den tillagda textrutekomponenten och ange dess namn.
   ![Infoga layout](/help/forms/assets/tabs-on-top-textbox-component.png)
1. Lägg på samma sätt till ytterligare två textrutekomponenter och ange ett namn för komponenterna som e-post-ID och avdelningsnamn.\
   ![Första panelen](/help/forms/assets/tabs-on-tops-first-panel.png)

   Nu när komponenterna på den första panelen har lagts till kan du fortsätta med att lägga till komponenterna på den andra panelen.

1. Klicka på **Välj panel** i verktygsfältet för att växla panelen.

   ![Växla panel](/help/forms/assets/tabs-on-top-select-panel.png)

   När du klickar på **Välj panel** visas listan med paneler som lagts till i komponenten Vågräta flikar.

   ![Växla panel](/help/forms/assets/tabs-on-tops-panel2.png)

1. Välj **2 Panel** i panellistan och vyn ändras från den första panelen till den andra panelen.

   ![Andra panelen](/help/forms/assets/tabs-on-top-panel2-component.png)

1. Upprepa stegen som beskrivs från steg 2 till steg 4 för att lägga till de önskade komponenterna i panel 2 enligt bilden nedan:

   ![Andra panelkomponenter](/help/forms/assets/panel-2-components.png)

1. Växla till **3-panelen** genom att följa stegen som beskrivs i steg 6 och steg 7.

1. Upprepa stegen som beskrivs från steg 2 till steg 4 för att lägga till den önskade komponenten i panel 3:

   ![Komponenter i den tredje panelen](/help/forms/assets/panel-3-component.png)

1. Klicka på **[!UICONTROL Preview]** i det övre högra hörnet av redigeringsmiljön.
   ![Vågrät layout](/help/forms/assets/horizontal-layout.gif)

Du kan också [dra och släppa komponenter](#extra-bytes) för att lägga till formulärkomponenterna på varje panel.


<!-- #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



Du kan också ta bort en formulärkomponent från panelen med ikonen ![Ta bort](/help/forms/assets/Smock_Delete_18_N.svg) .

![Tar bort en komponent](/help/forms/assets/delete-component.png)

Du kan också lägga till de valideringar som krävs för komponenterna efter behov.

## Hur ersätter man en befintlig layout med en ny layout?

Du kan ersätta en layout för ett formulär med en ny layout, som bland annat innebär att ändra hur komponenterna ordnas och visas i ett formulär.

Utför följande steg för att ersätta den befintliga layouten för ett formulär:

1. Klicka på ikonen Ersätt i verktygsfältet för layoutkomponenten så visas dialogrutan **[!UICONTROL Replace Component]**.

   ![Ersätt layout](/help/forms/assets/replace-layout.png)

1. Välj önskad layout i dialogrutan **[!UICONTROL Replace Component]**.

   ![Dialogrutan Ersätt komponent](/help/forms/assets/replace-component.png)

   När du har valt layouten ändras komponenternas placering i layouten därefter. Välj till exempel komponenten för lodräta tabbar i dialogrutan **[!UICONTROL Replace Component]**. Placeringen av panelen ändras till tabbar till vänster:

   ![Lodrät layout](/help/forms/assets/vertical-tab.gif)

## Extra byte

Så här drar och släpper du komponenter i formulärverktyget:

1. Leta reda på det avsnitt där du kan lägga till komponenter.
1. Navigera till den vänstra panelen i redigeringsmiljön och klicka på **Komponenter**.

   ![Komponentpanelen](/help/forms/assets/add-new-component.png)

   När du klickar på alternativet **Komponenter** visas listan med tillgängliga komponenter.

   ![Komponentpanelen](/help/forms/assets/add-new-component2.png)

1. Bläddra bland de tillgängliga komponenterna och markera önskad komponent.

1. Dra komponenten genom att klicka och hålla ned den markerade komponenten och dra den sedan över till panelområdet för att montera den.

1. Släpp komponenten på panelen genom att släppa musknappen.

## Nästa steg

När du känner till de olika layoutfunktionerna för ett adaptivt formulär baserat på kärnkomponenter kan du gå vidare till nästa steg:

* [Skapa ditt första adaptiva formulär baserat på kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md)
* [Skapa och använda adaptiva formulärteman](/help/forms/using-themes-in-core-components.md)



## Se även

{{see-also}}

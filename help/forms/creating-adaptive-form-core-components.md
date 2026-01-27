---
title: 'Form builder: Skapa blanketter med komponenter'
description: Lär dig använda AEM Forms formulärbyggare för att skapa adaptiva formulär med kärnkomponenter. Perfekt för blankettskapare som behöver responsiva HTML5-blanketter som effektiviserar informationsinsamling och -bearbetning.
keywords: formulärbyggare, kärnkomponenter, skapa formulär, formulärskapare, adaptiva formulär, skapa formulär, AEM-formulär, responsiva formulär
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '2280'
ht-degree: 0%

---

# Form builder: Skapa blanketter med komponenter {#creating-an-adaptive-form-core-components}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html) |
| AEM as a Cloud Service | Den här artikeln |


Med AEM Forms formulärbyggare kan du skapa formulär som är engagerande, responsiva, dynamiska och anpassningsbara. Vare sig du är formulärskapare och bygger upp professionella formulär eller snabbt behöver skapa responsiva formulär, har AEM Forms en användarvänlig guide. Guiden har snabb fliknavigering för att enkelt välja förkonfigurerade mallar, format, fält och alternativ för att skicka.

Innan du börjar får du lära dig mer om vilken typ av Forms-komponenter du kan använda:

* [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en): Dessa är standardiserade datainhämtningskomponenter. Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser. En utvecklare kan enkelt anpassa och utforma dessa komponenter. Adobe rekommenderar att du använder dessa moderna och utbyggbara komponenter för att utveckla Adaptiv Forms.

* [Adaptiva Forms Foundation-komponenter](creating-adaptive-form.md): Dessa är klassiska (gamla) datainhämtningskomponenter. Du kan fortsätta att använda dessa för att redigera dina befintliga grundläggande komponentbaserade adaptiva formulär. Om du skapar nya formulär rekommenderar Adobe att du använder [adaptiva Forms Core-komponenter](creating-adaptive-form-core-components.md) för att skapa en adaptiv Forms.

![Guiden för att skapa ett anpassat formulär](/help/release-notes/assets/wizard.png)


## Krav

Du behöver följande för att skapa ett adaptivt formulär:



* **En mall för adaptiva formulär**: En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur. Här finns också alternativ för att definiera ett tema och en skicka-åtgärd. Temat definierar utseendet, känslan och skickaåtgärden definierar vilken åtgärd som ska vidtas när ett adaptivt formulär skickas in. Du kan till exempel skicka insamlade data till en datakälla. Molntjänsten tillhandahåller en OOTB-mall med namnet blank:

   * Mallen `blank` ingår i alla nya AEM Forms as a Cloud Service-program.
   * Du kan installera referenspaketet via Package Manager för att lägga till mallen `blank` i ditt AEM Forms as a Cloud Service-program.
   * Du kan även [skapa en anpassad Forms-mall (kärnkomponenter)](/help/forms/template-editor-core-components.md) från början.
   * Du kan också distribuera [exempelmallar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) till din miljö. Med dessa kan du snabbt börja skapa formulär.

* **Ett adaptivt formulärtema**: Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter.  Mallen `Canvas` ingår i alla nya AEM Forms as a Cloud Service-program. Du kan också distribuera [exempelteman](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) till din miljö. Dessa hjälper dig att börja utforma formulären och skapa en grundstruktur för att skapa eller anpassa ett tema efter företagets behov.

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Behörigheter**: Lägg till dina användare i gruppen [!DNL forms-users]. Medlemmarna i gruppen [!DNL forms-users] har behörighet att skapa ett anpassat formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Bygg ett anpassningsbart formulär  {#create-an-adaptive-form-core-components}

1. Logga in på din [!DNL Experience Manager Forms] Author-instans. Det kan vara en molninstans eller en lokal utvecklingsinstans.

1. Ange dina inloggningsuppgifter på Experience Manager inloggningssida. När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** i det övre vänstra hörnet.

1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas. På fliken Source väljer du en mall:

   ![Kärnkomponentmall](/help/forms/assets/core-components-template.png)

   När du väljer en mall markeras automatiskt ett tema och en skicka-åtgärd som anges i mallen och knappen **[!UICONTROL Create]** aktiveras. Du kan gå till flikarna **[!UICONTROL Style]** eller **[!UICONTROL Submission]** och välja ett annat tema eller skicka-åtgärd. Om den valda mallen inte anger något tema förblir knappen Skapa inaktiverad. Du kan gå till fliken **[!UICONTROL Styles]** och välja ett tema manuellt.

   >[!NOTE]
   >
   >
   > Om du inte har det, **Adaptiv Forms-mall (Core Component)** i din miljö, [Aktivera adaptiva Forms Core-komponenter för din miljö](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). När du aktiverar kärnkomponenterna för din miljö läggs mallen **Adaptive Forms (Core Component)** till i din miljö.

1. Välj ett tema på fliken **[!UICONTROL Style]**:

   * När den valda mallen anger ett tema väljs temat automatiskt i guiden. Du kan också välja ett annat tema på fliken Format.

   * Om den valda mallen inte anger något tema kan du använda fliken Format för att välja ett tema. Knappen **[!UICONTROL Create]** aktiveras först när ett tema har valts.

1. (Valfritt) Välj en datamodell på fliken Data:

   * **Formulärdatamodell (FDM)**: Med en [formulärdatamodell](data-integration.md) kan du integrera entiteter och tjänster från olika datakällor i ett adaptivt formulär. Välj FDM (Form Data Model) om det adaptiva formulär du skapar inbegriper att hämta och skriva data från och till flera datakällor.

   * **JSON-schema**: [JSON-schema](adaptive-form-json-schema-form-model.md) Med vår Core-Components-baserade adaptiva form kan du smidigt integrera med din organisations back-end-system genom att tillhandahålla möjligheten att associera ett JSON-schema, som representerar strukturen för de data som produceras eller förbrukas. Den här kopplingen gör det möjligt för författare att dynamiskt lägga till innehåll i det adaptiva formuläret med elementen i schemat. Elementen i schemat är enkelt tillgängliga på fliken Datamodellsobjekt i innehållsläsaren under redigeringsprocessen, och alla fält läggs automatiskt till i alla skapade adaptiva formulär.

   Som standard markeras alla fält i det associerade JSON-schemat automatiskt och konverteras till motsvarande adaptiva formulärkomponenter, vilket effektiviserar redigeringsprocessen. I guiden kan du välja vilka fält som ska inkluderas i det anpassade formuläret med hjälp av kryssrutor.

1. Välj en sändningsåtgärd på fliken **[!UICONTROL Submission]**:

   * När du väljer en mall markeras åtgärden Skicka som anges i mallen automatiskt. Du kan välja en annan skickaåtgärd på fliken Skicka. Fliken **[!UICONTROL &#x200B; Submission]** visar alla tillgängliga skicka-åtgärder.

   * När den valda mallen inte anger någon skicka-åtgärd kan du använda fliken **[!UICONTROL Submission]** för att välja en skicka-åtgärd

1. (Valfritt) På fliken **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett adaptivt formulär.

1. Välj **[!UICONTROL Create]**. En dialogruta där du kan ange namn, namn och plats för att spara det adaptiva formuläret visas:

   * **[!UICONTROL Title]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i användargränssnittet för [!DNL Experience Manager Forms].
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.
   * **[!UICONTROL Path:]** Anger platsen där det adaptiva formuläret ska sparas. Du kan spara det adaptiva formuläret direkt på `/content/dam/formsanddocuments` eller skapa en mapp som `/content/dam/formsanddocuments/adaptiveforms` om du vill spara ett adaptivt formulär. Se till att du skapar mappen innan du använder den i sökvägen. Fältet **[!UICONTROL Path]** skapar inte en mapp automatiskt.

1. Välj **[!UICONTROL Create]**. Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen.  Baserat på typen av anpassat formulär visas formulärelementen i det associerade <!--XFA form template, XML schema or --> JSON-schemat eller formulärdatamodellen (FDM) på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten. Du kan också dra och släppa dessa element för att skapa ett anpassat formulär.

Nu kan du dra och släppa [adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) till en adaptiv Forms-behållare för att utforma och skapa formuläret. Du kan även besöka [https://aemcomponents.dev/](https://aemcomponents.dev/) för att se hur de tillgängliga kärnkomponenterna fungerar i praktiken.

>[!NOTE]
>
> Du kan också [skapa adaptiv Forms med XFA-formulärmallar (*.XDP-filer)](/help/forms/create-adaptive-form-using-xfa-templates.md). Du sparar tid genom att återanvända fält från XDP-filer direkt i Adaptive Forms.

## Konfigurera skicka-åtgärd för ett anpassat formulär {#configure-submit-action-for-form}

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på knappen Skicka på ett anpassat formulär. Anpassade formulär innehåller några av de åtgärder som har vidtagits för att skicka in. Du kan också utöka en standardåtgärd för att skicka för att skapa en egen anpassad åtgärd. Så här konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.

1. Klicka på fliken **[!UICONTROL Submission]**.

   ![Klicka på skiftnyckelsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera en sändningsåtgärd](/help/forms/assets/adaptive-forms-submit-message.png)

1. Välj och konfigurera en **[!UICONTROL Submit action]** utifrån dina krav. Mer information om Skicka-åtgärder finns i [Åtgärden Skicka anpassat formulär](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Dirigera om användaren till en sida eller visa ett tackmeddelande när formuläret skickas

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller ett meddelande. Så här omdirigerar du användaren eller konfigurerar tackmeddelandet:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna fliken **[!UICONTROL Submission]**.

   ![Klicka på skiftnyckelsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera en omdirigeringssida eller tacka dig för meddelandet](/help/forms/assets/adaptive-forms-redirect-message.png)

   * Om du vill konfigurera en omdirigerings-URL, för alternativet Skicka, markerar du alternativet **[!UICONTROL Redirect to URL]** och bläddrar och väljer en AEM Sites-sida, eller anger en URL för en extern sida.

   * Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande för alternativet Skicka markerar du alternativet **[!UICONTROL Show Message]** och anger ett meddelande i rutan **[!UICONTROL Message content]**. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.

## Konfigurera ett schema eller en formulärdatamodell (FDM) för ett anpassat formulär{#configure-schema-or-data-model-for-form}

Du kan använda formulärdatamodellen (FDM) för att ansluta ett formulär till en Data Source för att skicka och ta emot data baserat på användaråtgärder. Du kan också ansluta ett formulär till ett JSON-schema för att ta emot skickade data i ett fördefinierat format. Beroende på behovet kan du ansluta formuläret till ett JSON-schema eller en FDM-modell (Form Data Model):

* [Skapa ett JSON-schema och överför det till din miljö](/help/forms/adaptive-form-json-schema-form-model.md)
* [Skapa en formulärdatamodell (FDM)](/help/forms/create-form-data-models.md)

### Konfigurera ett JSON-schema eller en formulärdatamodell (FDM) för formuläret

Så här konfigurerar du ett JSON-schema eller en formulärdatamodell (FDM) för formuläret:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna fliken **[!UICONTROL Data Model]**.

   ![Klicka på skiftnyckelsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera ett JSON-schema eller en formulärdatamodell (FDM)](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Välj och konfigurera ett JSON-schema eller en formulärdatamodell (FDM) utifrån dina krav:

   * När du väljer alternativet **[!UICONTROL Form Model]** använder du alternativet **[!UICONTROL Select Form Data Model]** för att välja en förkonfigurerad formulärdatamodell (FDM).
   * När du väljer alternativet **[!UICONTROL Schema]** använder du alternativet **[!UICONTROL Schema]** för att välja ett JSON-schema för formuläret.

1. Klicka på **[!UICONTROL Done]**.

## Konfigurera en förifyllningstjänst  {#configure-prefill-service-for-form}

Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Du kan:

* [Skapa en anpassad förifyllningstjänst](/help/forms/prepopulate-adaptive-form-fields.md)
* [Använd förifyllningstjänsten för formulärdatamodell](#fdm-prefill-service)

### Använd förifyllningstjänst för formulärdatamodell för att fylla i fält i ett anpassat formulär i förväg {#fdm-prefill-service}

Du kan använda förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär i förväg med hjälp av en formulärdatamodell eller en anpassad förifyllningstjänst. Tjänsten för förifyllning av formulärdatamodell använder tjänsten [Hämta tjänst för den konfigurerade formulärdatamodellen](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) för att hämta data. Så här använder du förifyllningstjänsten för formulärdatamodell för ett adaptivt formulär:

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på skiftnyckelsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera en omdirigeringssida eller tacka dig för meddelandet](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. Välj en formulärdatamodell (FDM). Öppna fliken **[!UICONTROL Basic]**. Välj **[!UICONTROL Form Data Model Prefill Service]** i förifyllningstjänsten.
1. Klicka på **[!UICONTROL Done]**. Ditt adaptiva formulär har nu konfigurerats för att använda förifyllning av formulärdatamodell. Du kan nu använda [regelredigeraren](rule-editor.md) för att skapa regler för att fylla i formulärfält i förväg.

## Redigera formulärmodellegenskaper för ett anpassat formulär {#edit-form-model}

1. Markera det adaptiva formuläret och välj ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Open Properties]**. Sidan Formuläregenskaper öppnas.

1. Gå till fliken **[!UICONTROL Form Model]** och välj en formulärmodell. Om det adaptiva formuläret inte har någon formulärmodell kan du välja antingen ett JSON-schema eller en formulärdatamodell (FDM). Om det adaptiva formuläret däremot redan är baserat på en formulärmodell kan du växla till en annan formulärmodell av samma typ. Om formuläret till exempel använder ett JSON-schema kan du enkelt växla till ett annat JSON-schema, och om formuläret använder en formulärdatamodell (FDM) kan du på liknande sätt växla till en annan formulärdatamodell (FDM).

1. Välj **[!UICONTROL Save]** om du vill spara egenskaperna.


## Hur byter jag namn på ett anpassningsbart AEM-formulär? {#rename-an-AEM-Adaptive-Form}

Så här byter du namn på ett anpassat formulär:

1. Välj ett anpassningsbart formulär i AEM Forms användargränssnitt.
1. Klicka på **Egenskaper** i den övre listen.
1. Ändra namnet på formuläret på fliken **Titel**, så som visas i bilden nedan.
1. Klicka på **Spara och stäng**.

![Byt namn på ett anpassat AEM-formulär](/help/forms/assets/change-af-name.png)



## Tillämplighet och användningsfall

### Försäkring

## Kan AEM Forms användas både för kundcentrerade och interna försäkringsprocesser?

Ja. AEM Forms stöder kundcentrerade digitala formulär samt interna, personalstyrda eller agentstyrda processer som granskningar, godkännanden och assisterad datainhämtning.

## Kan AEM Forms användas för inlämning av försäkringsanspråk?

Ja. AEM Forms har stöd för anpassningsbara blanketter i flera steg som gör det möjligt för försäkringstagarna att lämna in försäkringskrav digitalt, inklusive inhämtning av strukturerade data och styrkande dokumentation.

## Har AEM Forms stöd för skadeståndsanspråk på mobilförsäkringar?

Ja. AEM Forms har stöd för responsiva och mobilvänliga formulär, så att kunder och agenter kan lämna in försäkringsinformation från mobila enheter.

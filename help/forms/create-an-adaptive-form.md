---
title: Hur skapar man ett adaptivt formulär?
description: Lär dig använda AEM Forms formulärbyggare för att skapa mobilkänsliga adaptiva formulär. Perfekt för formulärskapare och utvecklare som behöver formulär som kan anpassas sömlöst mellan olika enheter.
keywords: formulärbyggare, formulärskapare, skapa formulär, formulärskapare, adaptiva formulär, responsiva formulär, HTML5-formulär, skapa formulär, AEM-formulär
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: 6f1c3fe7-b61e-47ce-b565-15b4904db092
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '2625'
ht-degree: 0%

---

# Starthandbok för Form Builder {#creating-an-adaptive-form}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html) |
| AEM as a Cloud Service | Den här artikeln |

Med AEM Forms formulärbyggare kan du skapa formulär som är engagerande, responsiva, dynamiska och anpassningsbara. Vare sig du är formulärskapare och bygger upp professionella formulär eller snabbt behöver skapa responsiva formulär, har AEM Forms en användarvänlig guide. Guiden har snabb fliknavigering för att enkelt välja förkonfigurerade mallar, format, fält och alternativ för att skicka.

![Guiden för att skapa ett anpassat formulär](/help/release-notes/assets/wizard.png){width="100%" align="center"}

Innan du börjar får du lära dig mer om vilken typ av Forms-komponenter du kan använda:

* [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en): Dessa är standardiserade datainhämtningskomponenter. Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser. En utvecklare kan enkelt anpassa och utforma dessa komponenter. Du kan besöka [https://aemcomponents.dev/](https://aemcomponents.dev/) om du vill visa tillgängliga kärnkomponenter i praktiken **Adobe rekommenderar att du använder dessa moderna och utbyggbara komponenter för att utveckla adaptiva Forms**.

* [Adaptiva Forms Foundation-komponenter](creating-adaptive-form.md): Dessa är klassiska (gamla) datainhämtningskomponenter. Du kan fortsätta att använda dessa för att redigera dina befintliga grundläggande komponentbaserade adaptiva formulär. Om du skapar nya formulär rekommenderar Adobe att du använder [adaptiva Forms Core-komponenter för att skapa en adaptiv Forms](#create-an-adaptive-form-core-components).

>[!BEGINTABS]

>[!TAB Skapa adaptiv Forms med kärnkomponenter (rekommenderas)]

Du behöver följande för att skapa ett adaptivt formulär:

* **Aktivera adaptiva Forms Core-komponenter för din miljö**: När du skapar ett program är de adaptiva Forms Core-komponenterna redan aktiverade för din miljö. Installera den senaste versionen för att aktivera adaptiva Forms Core-komponenter för din AEM Cloud-tjänstmiljö. När du aktiverar kärnkomponenterna för din miljö läggs mallen och arbetsytetemat **Adaptive Forms (Core Component)** till i din miljö. Om din version av AEM SDK är äldre än 2023.02.0 bör du [kontrollera att du har `prerelease` -flaggan aktiverad i din miljö](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#new-features) eftersom adaptiva Forms Core-komponenter ingick i förversionen före version 2023.02.0.

* **En mall för adaptiva formulär**: En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur. Här finns också alternativ för att definiera ett tema och en skicka-åtgärd. Temat definierar utseendet, känslan och skickaåtgärden definierar vilken åtgärd som ska vidtas när ett adaptivt formulär skickas in. Du kan till exempel skicka insamlade data till en datakälla. Molntjänsten tillhandahåller en OOTB-mall med namnet blank:

   * Mallen `blank` ingår i alla nya AEM Forms as a Cloud Service-program.
   * Du kan installera referenspaketet via Package Manager för att lägga till mallen `blank` i ditt AEM Forms as a Cloud Service-program.
   * Du kan även [skapa en anpassad Forms-mall (kärnkomponenter)](template-editor.md) från början.

* **Ett adaptivt formulärtema**: Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter.  Mallen `Canvas` ingår i alla nya AEM Forms as a Cloud Service-program.
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Behörigheter**: Lägg till dina användare i gruppen [!DNL forms-users]. Medlemmarna i gruppen [!DNL forms-users] har behörighet att skapa ett anpassat formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).


## Skapa ett anpassat formulär {#create-an-adaptive-form-core-components}

1. Logga in på din [!DNL Experience Manager Forms] Author-instans. Det kan vara en molninstans eller en lokal utvecklingsinstans.

1. Ange dina inloggningsuppgifter på Experience Manager inloggningssida. När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** i det övre vänstra hörnet.

1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas. På fliken Source väljer du en mall:

   ![Kärnkomponentmall](/help/forms/assets/core-components-template.png){width="100%" align="center"}

   När du väljer en mall markeras automatiskt ett tema och en skicka-åtgärd som anges i mallen och knappen **[!UICONTROL Create]** aktiveras. Du kan gå till flikarna **[!UICONTROL Style]** eller **[!UICONTROL Submission]** och välja ett annat tema eller skicka-åtgärd. Om den valda mallen inte anger något tema förblir knappen Skapa inaktiverad. Du kan gå till fliken **[!UICONTROL Styles]** och välja ett tema manuellt.

   >[!NOTE]
   >
   >
   > Om du inte har det, **Adaptiv Forms-mall (Core Component)** i din miljö, [Aktivera adaptiva Forms Core-komponenter för din miljö](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). När du aktiverar kärnkomponenterna för din miljö läggs mallen **Adaptive Forms (Core Component)** till i din miljö.

1. Välj ett tema på fliken **[!UICONTROL Style]**:

   * När den valda mallen anger ett tema väljs temat automatiskt i guiden. Du kan också välja ett annat tema på fliken Format.

   * Om den valda mallen inte anger något tema kan du använda fliken Format för att välja ett tema. Knappen **[!UICONTROL Create]** aktiveras först när ett tema har valts.

1. (Valfritt) Välj en datamodell på fliken Data:

   * **Formulärdatamodell**: Med en [formulärdatamodell(FDM)](data-integration.md) kan du integrera entiteter och tjänster från olika datakällor i ett adaptivt formulär. Välj FDM (Form Data Model) om det adaptiva formulär du skapar inbegriper att hämta och skriva data från och till flera datakällor.

   * **JSON-schema**: [JSON-schema](adaptive-form-json-schema-form-model.md) Med vår Core-Components-baserade adaptiva form kan du smidigt integrera med din organisations back-end-system genom att tillhandahålla möjligheten att associera ett JSON-schema, som representerar strukturen för de data som produceras eller förbrukas. Den här kopplingen gör det möjligt för författare att dynamiskt lägga till innehåll i det adaptiva formuläret med elementen i schemat. Elementen i schemat är enkelt tillgängliga på fliken Datamodellsobjekt i innehållsläsaren under redigeringsprocessen, och alla fält läggs automatiskt till i alla skapade adaptiva formulär.

   Som standard markeras alla fält i det associerade JSON-schemat automatiskt och konverteras till motsvarande adaptiva formulärkomponenter, vilket effektiviserar redigeringsprocessen. I guiden kan du välja vilka fält som ska inkluderas i det anpassade formuläret med hjälp av kryssrutor.

1. Välj en sändningsåtgärd på fliken **[!UICONTROL Submission]**:

   * När du väljer en mall markeras åtgärden Skicka som anges i mallen automatiskt. Du kan välja en annan skickaåtgärd på fliken Skicka. Fliken **[!UICONTROL  Submission]** visar alla tillgängliga skicka-åtgärder.

   * När den valda mallen inte anger någon skicka-åtgärd kan du använda fliken **[!UICONTROL Submission]** för att välja en skicka-åtgärd

1. (Valfritt) På fliken **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett adaptivt formulär.

1. Välj **[!UICONTROL Create]**. En dialogruta där du kan ange namn, namn och plats för att spara det adaptiva formuläret visas:

   * **[!UICONTROL Title]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i användargränssnittet för [!DNL Experience Manager Forms].
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.
   * **[!UICONTROL Path:]** Anger platsen där det adaptiva formuläret ska sparas. Du kan spara det adaptiva formuläret direkt på `/content/dam/formsanddocuments` eller skapa en mapp som `/content/dam/formsanddocuments/adaptiveforms` om du vill spara ett adaptivt formulär. Se till att du skapar mappen innan du använder den i sökvägen. Fältet **[!UICONTROL Path]** skapar inte en mapp automatiskt.

1. Välj **[!UICONTROL Create]**. Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen.  Baserat på typen av anpassat formulär visas formulärelementen i det associerade <!--XFA form template, XML schema or --> JSON-schemat eller formulärdatamodellen (FDM) på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten.

Nu kan du dra och släppa [adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components) eller schemaelement för att skapa ditt adaptiva formulär.


## Redigera formulärmodellegenskaper för ett anpassat formulär {#edit-form-model-core-components-based-adaptive-forms}

1. Markera det adaptiva formuläret och välj ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Open Properties]**. Sidan Formuläregenskaper öppnas.

1. Gå till fliken **[!UICONTROL Form Model]** och välj en formulärmodell. Om det adaptiva formuläret inte har någon formulärmodell kan du välja antingen ett JSON-schema eller en formulärdatamodell (FDM). Om det adaptiva formuläret däremot redan är baserat på en formulärmodell kan du växla till en annan formulärmodell av samma typ. Om formuläret till exempel använder ett JSON-schema kan du enkelt växla till ett annat JSON-schema, och om formuläret använder en formulärdatamodell (FDM) kan du på liknande sätt växla till en annan formulärdatamodell (FDM).

1. Välj **[!UICONTROL Save]** om du vill spara egenskaperna.

>[!TAB Skapa adaptiv Forms med Foundation Components]

Du behöver följande för att skapa ett adaptivt formulär:

* **Behörigheter**: Lägg till dina användare i [!DNL forms-users] för att ge dem behörighet att skapa ett anpassat formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

* **Ett adaptivt formulärtema**: Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter. Du kan [skapa ett tema](themes.md) eller [importera ett befintligt tema](import-export-forms-templates.md#uploading-a-theme). Du kan också distribuera den [senaste arketypen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) för vissa exempelteman.

* **En mall för adaptiva formulär**: En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur. Här finns också alternativ för att definiera ett tema och en skicka-åtgärd. Temat definierar utseendet, känslan och skickaåtgärden definierar vilken åtgärd som ska vidtas när ett adaptivt formulär skickas in. Du kan till exempel skicka insamlade data till en datakälla. Molntjänsten har stöd för två typer av mallar:

   * **Redigerbar mall**: Du kan [skapa en](template-editor.md) eller [importera en befintlig redigerbar mall](migrate-to-forms-as-a-cloud-service.md). Du kan också distribuera den [senaste arketypen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests.) för att få några exempel på redigerbara mallar.

   * **Statisk mall**: Dessa är äldre mallar och rekommenderas endast för kunder som migrerar från Adobe Managed Services (AMS) och lokala AEM Forms-installationer (AEM 6.5 Forms eller tidigare). På så sätt kan du fortsätta att använda dina befintliga investeringar i statiska mallar. När du skapar ett adaptivt formulär använder du en redigerbar mall.


## Skapa ett anpassat formulär {#create-an-adaptive-form-foundation-components}

1. Åtkomst till författarinstansen [!DNL Experience Manager Forms]. Det kan vara en molninstans eller en lokal utvecklingsinstans.

1. Ange dina inloggningsuppgifter på Experience Manager inloggningssida.

   När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** i det övre vänstra hörnet.

1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas.
1. På fliken Source väljer du en mall:

   * När du väljer en redigerbar mall markeras automatiskt ett tema och en skicka-åtgärd som anges i mallen och knappen **[!UICONTROL Create]** aktiveras. Du kan gå till flikarna **[!UICONTROL Style]** eller **[!UICONTROL Submission]** och välja ett annat tema eller skicka-åtgärd. Om den valda redigerbara mallen inte anger något tema är knappen Skapa inaktiverad. Du kan gå till fliken **[!UICONTROL Styles]** och välja ett tema manuellt.

     >[!NOTE]
     >
     > Du kan också skapa mallen [!UICONTROL Document of Record] med en adaptiv Forms-redigerare. Mer information finns i [Dokumentstöd i redigeraren för anpassade formulär](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * När du väljer en statisk mall är alternativen för data, format, sändning, leverans och förhandsgranskning inte tillgängliga. När du skapar ett adaptivt formulär bör du använda en redigerbar mall.

1. Välj ett tema på fliken **[!UICONTROL Style]**:

   * När den valda mallen anger ett tema väljs temat automatiskt i guiden. Du kan också välja ett annat tema på fliken Format.
   * Om den valda mallen inte anger något tema kan du använda fliken Format för att välja ett tema. Knappen **[!UICONTROL Create]** aktiveras först när ett tema har valts.

1. (Valfritt) Välj en datamodell på fliken **[!UICONTROL Data]**:

   * **Formulärdatamodell**: Med en [FDM (Form Data Model)](data-integration.md) kan du integrera entiteter och tjänster från olika datakällor i ett adaptivt formulär. Välj FDM (Form Data Model) om det adaptiva formulär du skapar inbegriper att hämta och skriva data från och till flera datakällor.

   * **JSON-schema**: [JSON-schema](adaptive-form-json-schema-form-model.md) representerar den struktur i vilken data produceras eller används av det bakomliggande systemet i din organisation. Du kan koppla schemat till ett adaptivt formulär och använda dess element för att lägga till dynamiskt innehåll i det adaptiva formuläret. Elementen i schemat är tillgängliga för användning på fliken Datamodellobjekt i innehållsläsaren när du redigerar Adaptiv Forms och alla fält läggs även till i det anpassade formuläret.

   Som standard markeras alla fält i datamodellen. När du skapar det adaptiva formuläret konverteras alla markerade datamodellfält till motsvarande adaptiva formulärkomponenter. Guiden innehåller kryssrutor som du kan använda för att markera endast de fält som ska ingå i det adaptiva formuläret.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. Välj en sändningsåtgärd på fliken **[!UICONTROL Submission]**:

   * När du väljer en mall markeras åtgärden Skicka som anges i mallen automatiskt. Du kan välja en annan skickaåtgärd på fliken Skicka. Fliken **[!UICONTROL  Submission]** visar alla tillgängliga skicka-åtgärder.

   * När den valda mallen inte anger någon skicka-åtgärd kan du använda fliken **[!UICONTROL Submission]** för att välja en skicka-åtgärd

1. (Valfritt) På fliken Leverans kan du ange ett publicerings- eller avpubliceringsdatum för ett adaptivt formulär.

1. Välj **[!UICONTROL Create]**. En dialogruta där du kan ange namn, namn och plats för att spara det adaptiva formuläret visas:

   * **[!UICONTROL Title]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i användargränssnittet för [!DNL Experience Manager Forms].
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.
   * **[!UICONTROL Path:]** Anger platsen där det adaptiva formuläret ska sparas. Du kan spara det adaptiva formuläret direkt på `/content/dam/formsanddocuments` eller skapa en mapp som `/content/dam/formsanddocuments/adaptiveforms` om du vill spara ett adaptivt formulär. Se till att du skapar mappen innan du använder den i sökvägen. Fältet **[!UICONTROL Path:]** skapar inte en mapp automatiskt.

1. Välj **[!UICONTROL Create]**. Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen. Här visas också sidlisten där du kan anpassa det skapade formuläret efter behov.

   Baserat på typen av anpassat formulär visas formulärelementen i det associerade <!--XFA form template, XML schema or --> JSON-schemat eller formulärdatamodellen (FDM) på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten. Du kan också dra och släppa dessa element för att skapa ett anpassat formulär.

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Select to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an adaptive form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, select on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Select **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and select Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model2). -->

## Redigera formulärmodellegenskaper för ett anpassat formulär {#edit-form-model-foundation-components}

Du kan ändra formulärmodellen för ett adaptivt formulär (JSON-baserat eller FDM (Form Data Model)). Du kan inte ändra från en formulärmodell till en annan.

1. Markera det adaptiva formuläret och välj ikonen **Egenskaper** .
1. Öppna fliken **[!UICONTROL Form Model]** och gör något av följande.

   * Om det adaptiva formuläret saknar en formulärmodell kan du välja en annan formulärmodell och därefter välja <!-- a form template, --> XML- eller JSON-schema eller formulärdatamodell (FDM).
   * Om det adaptiva formuläret är baserat på en formulärmodell kan du välja ett annat <!-- form template, --> XML- eller JSON-schema eller formulärdatamodell (FDM) för samma formulärmodell.

1. Välj **[!UICONTROL Save]** om du vill spara egenskaperna.

Du kan också ändra formulärmodellens egenskaper i verktyget Adaptiv formulärbyggare eller verktyget Adaptiv formulärmall.

1. Markera komponenten **[!UICONTROL Adaptive Form container (Root)]**.
1. Klicka på ikonen ![Konfigurera ikon](/help/forms/assets/configure-icon.svg) för att öppna behållaren **[!UICONTROL Properties]** för det adaptiva formuläret.
1. Välj fliken **[!UICONTROL Data Model]** och gör något av följande:

   * Om det adaptiva formuläret saknar en formulärmodell kan du välja en formulärmodell och därefter välja <!-- a form template, --> XML- eller JSON-schema eller formulärdatamodell (FDM).
   * Om det adaptiva formuläret är baserat på en formulärmodell kan du inte ändra formulärmodellen. Du kan välja ett annat <!-- form template, --> XML- eller JSON-schema eller formulärdatamodell (FDM) för samma formulärmodell.
1. Välj ![Spara](/help/forms/assets/check-button.png) om du vill spara egenskaperna.

![FDM-schema-support](/help/forms/assets/fdmsupport.png){width="100%" align="center"}

>[!NOTE]
>
> Du kan också spara ett anpassat formulär som en mall. Mer information finns i [Skapa en mall med ett adaptivt formulär](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).

>[!ENDTABS]


## Nästa steg

* [Använd Adobe Sign med Forms](working-with-adobe-sign.md)
* [Använd Google reCaptcha i med Forms](captcha-adaptive-forms.md)
* [Lägga till upprepningsbart avsnitt i ett formulär](create-forms-repeatable-sections.md)
* [Förifyll fält i ett formulär](prepopulate-adaptive-form-fields.md)

>[!MORELIKETHIS]
>
>* [Skapa ett anpassat formulär](/help/forms/creating-adaptive-form-core-components.md)

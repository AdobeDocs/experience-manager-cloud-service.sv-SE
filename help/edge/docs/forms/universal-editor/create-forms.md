---
title: Skapa fristående blanketter baserade på mallar från Core Component eller Edge Delivery Services och publicera dem på Edge Delivery Services
description: I den här artikeln beskrivs hur du skapar adaptiv Forms genom att välja en Core Component-baserad eller Edge Delivery Services-baserad mall i guiden Skapa formulär. Du kan även publicera formulären på AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: e2ea802856a2fbab90d4ddb1ecf7280ce789d59c
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---


# Från redigering till publicering: AEM Forms på Edge Delivery Services

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande med ditt GitHub-organisationsnamn och databasnamn från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>

Med Adobe Experience Manager (AEM) kan du skapa formulär som är engagerande, responsiva och dynamiska. Det innehåller flera redigeringsmetoder som passar olika krav och nivåer av användarexpertis. &#x200B;

I den här artikeln behandlas hur man skapar formulär i AEM-miljön och publicerar dem via Edge Delivery Services. Forms som byggts med Core Component-baserade mallar kan publiceras på både AEM och Edge Delivery Services, vilket ger flexibilitet vid driftsättningen. Formulär som skapats med Edge Delivery Services-baserade mallar kan däremot bara publiceras på Edge Delivery Services. &#x200B;

![Skapa och publicera anpassat formulär](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## Fördelar med att skapa formulär i AEM och publicera med Edge Delivery Services:

* **Bevara befintliga AEM-arbetsflöden**: Organisationer kan fortsätta använda sina etablerade AEM-arbetsflöden och styrningsstrukturer för att säkerställa konsekvens och kontroll när det gäller att skapa innehåll. &#x200B;

* **Förbättrade prestanda**: Om du publicerar via Edge Delivery Services kommer återgivningstiden att bli kortare, vilket förbättrar användarupplevelsen och minskar sidinläsningstiden. &#x200B;

* **Förbättrad SEO**: Edge Delivery Services har utformats för att leverera innehåll med höga Google Lighthuse-poäng, vilket kan leda till bättre sökmotoroptimering och ökad synlighet. &#x200B;

* **Flexibla distributionsalternativ**: Forms som byggts med kärnkomponenter kan publiceras på både AEM och Edge Delivery Services, vilket ger flexibilitet i distributionsstrategier. &#x200B;

## Innan du börjar

Innan du börjar skapa formulär i AEM och publicerar dem via Edge Delivery Services måste du kontrollera att följande krav är uppfyllda:

* Kontrollera att du har en Github-databas konfigurerad för Edge Delivery Services.
   * Om du inte har någon databas kan du [skapa ett nytt AEM-projekt som är förkonfigurerat med det adaptiva Forms-blocket](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block).
   * Om du har en databas lägger du till det adaptiva Forms-blocket i din befintliga databas. Detaljerade instruktioner finns i [Komma igång med Edge Delivery Services för AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project).
* Upprätta en anslutning mellan din AEM-miljö och GitHub-databasen. [Hur gör jag?](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

Ett beslutsflödesdiagram som vägleder installationen och publiceringen av Adaptive Forms:

![Github-databasarbetsflöde](/help/forms/assets/repo-workflow.png){width=auto}

## Skapa formulär i AEM och publicera dem i Edge Delivery Services

Följ de här stegen för att skapa formulär i AEM och publicera dem på Edge Delivery Services:

[1. Välj en mall och skapa formuläret](#choose-a-template-and-create-the-form)

[2. Skriv formuläret](#author-the-form)

[3. Publicera ett formulär](#publish-a-form)

### Välj en mall och skapa formuläret

Du kan skapa formulär på en AEM-instans för publicering till Edge Delivery Services med:

>[!BEGINTABS]

>[!TAB Edge Delivery Services-baserad mall]

Gör så här för att välja mallen och skapa formuläret:

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas.
1. På fliken **Source** väljer du en **Edge Delivery Services-baserad mall**:

   ![Skapa EDS Forms](/help/edge/assets/create-eds-forms.png)

   När du väljer en **Edge Delivery Services-baserad mall** aktiveras knappen **[!UICONTROL Create]** .
1. (Valfritt) På flikarna **[!UICONTROL Data Source]** eller **[!UICONTROL Submission]** kan du välja en datakälla eller skicka-åtgärd.
1. (Valfritt) På fliken **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett formulär.
1. Klicka på **[!UICONTROL Create]** så visas guiden **Skapa formulär**:

   1. Ange **Namn** och **Titel**.
   1. Ange **GitHub-URL**. Om din GitHub-databas till exempel har namnet `edsforms`, finns den under kontot `wkndforms`, är URL:en:

      `https://github.com/wkndforms/edsforms`

   ![Guiden Skapa formulär](/help/edge/assets/create-form-wizard.png)

   När du klickar på **[!UICONTROL Create]** öppnas formuläret i den universella redigeraren för redigering.

   ![författare till formuläret](/help/edge/assets/author-form.png)
1. Klicka på **[!UICONTROL Create]** för att skapa formuläret. Nu kan du [skapa formuläret med den universella redigeraren](#author-the-form).

>[!TAB Kärnkomponentbaserad mall]

Gör så här för att välja mallen och skapa formuläret:

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas.
1. På fliken **Source** väljer du en **Core Component-baserad mall** och ett **tema**. Knappen **[!UICONTROL Create]** aktiveras:

   ![Kärnkomponentbaserad mall](/help/forms/assets/core-component-based-template.png)

1. (Valfritt) På flikarna **[!UICONTROL Data Source]** eller **[!UICONTROL Submission]** kan du välja en datakälla eller skicka-åtgärd.
1. (Valfritt) På fliken **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett formulär.
1. Klicka på **[!UICONTROL Create]** så visas guiden **Skapa formulär** för:
   1. Ange **Namn** och **Titel**.
   1. Ange platsen i fältet **Sökväg** där det adaptiva formuläret ska sparas.

   ![Guiden Skapa formulär](/help/forms/assets/create-cc-form.png)

   När du klickar på **[!UICONTROL Create]** öppnas formuläret i den adaptiva formulärredigeraren för redigering.

   ![Adaptiv formulärredigerare](/help/forms/assets/af-editor-form.png)

1. Klicka på **[!UICONTROL Create]** för att skapa formuläret. Nu kan du [skapa formuläret med den adaptiva formulärredigeraren](#author-the-form).

>[!ENDTABS]

### Författare till formuläret

De formulär som skapas med den Edge Delivery Services-baserade mallen öppnas i [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) för redigering. Formulär som skapats med den Core Component-baserade mallen öppnas dock i den adaptiva formulärredigeraren för redigering.

Utför följande steg för att skapa formulär med den universella redigeraren för en Edge Delivery Services-baserad mall eller med den adaptiva formulärredigeraren för den kärnkomponentbaserade mallen:

>[!BEGINTABS]

>[!TAB Edge Delivery Services-baserad mall]


1. Öppna innehållsläsaren och navigera till komponenten **[!UICONTROL Adaptive Form]** i **innehållsträdet**.

   ![innehållsträd](/help/edge/assets/content-tree.png)

1. Klicka på ikonen **[!UICONTROL Add]** och lägg till de önskade komponenterna från listan **Adaptiva formulärkomponenter**.
   ![lägg till komponent](/help/edge/assets/add-component.png)

   På skärmbilden nedan visas `Registration Form` som har skapats i Universella redigerare:

   ![kontakta oss](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> [Klicka här](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) om du vill ha detaljerade anvisningar om hur du skapar ett adaptivt formulär med den universella redigeraren.

Nu kan du [konfigurera och anpassa Skicka-åtgärder för formulär](/help/edge/docs/forms/universal-editor/submit-action.md).

>[!TAB Kärnkomponentbaserad mall]

1. Klicka på **[!UICONTROL Insert component]** i avsnittet **Dra komponenter hit**.

   ![Dra komponenter hit](/help/forms/assets/drag-components-af-editor.png)

1. Lägg till önskade komponenter från listan **Adaptiva formulärkomponenter**.

   ![Lägg till komponenter](/help/forms/assets/add-component-af.png)

På skärmbilden nedan visas `Enrollment Form` som har skapats i redigeraren för anpassade formulär:

![Adaptiv formulärredigerare](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> [Klicka här](/help/forms/creating-adaptive-form-core-components.md) om du vill ha mer information om hur du skapar ett adaptivt formulär baserat på mallen för kärnkomponenten.

Nu kan du [konfigurera Skicka-åtgärder för formulär](/help/forms/configure-submit-actions-core-components.md).

>[!ENDTABS]

### Publicera formuläret

Om du vill publicera ett adaptivt formulär på Edge Delivery Services måste du [skapa en Edge Delivery Services-konfiguration på en AEM](#create-an-edge-delivery-services-configuration)-instans.

#### Skapa en Edge Delivery Services-konfiguration

Så här skapar du Edge Delivery Services-konfigurationen:

>[!BEGINTABS]
>[!TAB Edge Delivery Services-baserad mall]


Edge Delivery Services-konfigurationen för formulär som är baserade på den Edge Delivery Services-baserade mallen skapas automatiskt i formulärets konfigurationsbehållare.

![Edge Delivery Services-konfiguration](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Kärnkomponentbaserad mall]

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Edge Delivery Services Configuration]** på din AEM Forms as a Cloud Service-författarinstans.

   ![Välj Edge Delivery Services-konfiguration](/help/edge/assets/select-eds-conf.png)

2. Välj den mapp som matchar formulärets namn. Om ditt formulär till exempel heter `enrollment-form` väljer du mappen `forms/enrollment-form` och klickar på **[!UICONTROL Create]** > **[!UICONTROL Configuration]**:

   ![Edge Delivery Services-konfiguration](/help/forms/assets/create-eds-conf.png)

3. Klicka på **[!UICONTROL Edge Delivery Services Configuration]** och klicka på **[!UICONTROL Properties]** för att öppna egenskaperna:

   ![Automatiskt skapad konfiguration](/help/forms/assets/eds-conf.png)

   Edge Delivery Services Configuration visas.

4. Ange följande i Edge Delivery Services-konfigurationen:

   * **Organisation**: Ange ditt GitHub-organisationsnamn.

   * **Platsnamn**: Ange ditt GitHub-databasnamn.
   * **Förgrening**: Ange förgreningsnamnet. Lämna textrutan tom om du använder huvudgrenen.
   * **(Valfritt) Edge Host**: Låt alternativet Edge Host vara. Formuläret publiceras i både förhandsgransknings- (.page) och livemiljön (.live).
   * **(Valfritt) Webbplatsautentiseringstoken**: Använd webbplatsautentiseringstoken för att autentisera begäranden mellan din AEM-instans och Edge Delivery Services på ett säkert sätt.

5. Klicka på **[!UICONTROL Save and Close]**. Konfigurationen skapas.

>[!ENDTABS]

#### Få åtkomst till formuläret i Edge Delivery Services

För att få åtkomst till formuläret på Edge Delivery Services är det obligatoriskt att publicera formuläret. Utför följande steg för att publicera formuläret:

>[!BEGINTABS]
>[!TAB I Universal Editor]

1. Publicera formuläret genom att klicka på knappen **[!UICONTROL Publish]** i det övre högra hörnet av Universella redigerare.

![publicera formulär](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Läs artikeln [Publicera och distribuera](/help/edge/docs/forms/universal-editor/publish-forms.md) om du vill veta mer om hur du publicerar ett formulär till Edge Delivery Services.

>[!TAB I anpassad formulärredigerare]

1. I Experience Manager Forms-konsolen går du till den överordnade mappen och väljer ett formulär som du vill publicera.

1. Klicka på alternativet **[!UICONTROL Publish]** i verktygsfältet och ta en titt på alla referensresurser som skulle publiceras med formuläret.

![Publicera formulär i anpassad formulärredigerare](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Läs artikeln [Hantera publikation i Experience Manager Forms](/help/forms/manage-publication.md) om du vill veta hur du publicerar ett formulär i den adaptiva formulärredigeraren.

>[!ENDTABS]

* **Mellanlagrad version (för testning)**: Den mellanlagrade versionen visar den opublicerade, fungerande versionen av formuläret för testning. Använd följande URL-format för att förhandsgranska formuläret innan det publiceras:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **Live-version (publicerat formulär)**:   Den aktiva versionen visar den senast publicerade versionen av formuläret, som är tillgänglig för slutanvändarna. Använd följande URL-format för att komma åt den publicerade, aktiva versionen av formuläret:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  URL-strukturen är densamma för både testversioner och liveversioner. Innehållet som du ser skiljer sig dock åt beroende på sammanhanget.

I skärmbilderna nedan jämförs testformulärs- och Live-formulärs-URL:er och förhandsgranskningar av formulär som skapats med Edge Delivery Services-baserade och Core Component-baserade mallar:

>[!BEGINTABS]
>[!TAB Edge Delivery Services-baserad mall]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>Version</strong></th>
      <th style="width: 80%;"><strong>Bild</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>Mellanlagrad version</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="Mellanlagrad version av registreringsformulär" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Live-version</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="Live-version av registreringsformulär" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB Kärnkomponentbaserad mall]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>Version</strong></th>
      <th style="width: 80%;"><strong>Bild</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Mellanlagrad version</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="Mellanlagrad version av registreringsformulär" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Live-version</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="Live-version av anmälningsformulär" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## Felsökning

Har du problem med att läsa in formuläret? Här är några vanliga problem och hur du åtgärdar dem:

* **Formulär-URL**: Dubbelkontrollera att formulärets URL inte innehåller tillägget .html i slutet. Edge-tjänsten för leverans kräver inte det här tillägget.

* **AEM Author UR** L: Kontrollera att den URL för AEM Author som anges i `fstab.yaml` -filen är korrekt formaterad. Den ska innehålla följande uppgifter:

   * Rätt GitHub-ägare
   * Rätt databasnamn
   * Den specifika gren som du använder för Edge Delivery Services

## Börja skapa formulär

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->

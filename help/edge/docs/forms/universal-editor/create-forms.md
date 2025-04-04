---
title: Hur skapar man fristående blanketter som bygger på Edge Delivery Services-mallar med Universal Editor?
description: I den här artikeln beskrivs hur du använder den universella redigeraren för att skapa formulär genom att välja en Edge Delivery Services-baserad mall i guiden Skapa formulär. Du kan även publicera formulären på AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: b0cedf31a8759cdf403e1e7d6aadcab3bba03bab
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Skapa adaptiv Forms med Universal Editor

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande med ditt GitHub-organisationsnamn och databasnamn från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>

Universell redigerare är en mångsidig visuell redigerare som ger dig en upplevelse som heter What-you-see-is-what-you-get (WYSIWYG) när du redigerar formulär. Det gör det enklare att skapa responsiva och användarvänliga formulär med dra-och-släpp-funktionen, med hjälp av tillgängliga adaptiva Forms-komponenter som textrutor, alternativknappar och kryssrutor.

AEM har ett block, Adaptive Forms Block, som gör det enkelt att skapa Edge Delivery Services Forms för datainhämtning och datalagring med Universal Editor. Du kan [skapa ett nytt AEM-projekt förkonfigurerat med det adaptiva Forms-blocket](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) eller [lägga till det adaptiva Forms-blocket i ett befintligt AEM-webbplatsprojekt](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project).

![Github-databasarbetsflöde](/help/edge/assets/repo-workflow.png)

I den här artikeln får du hjälp med att skapa och redigera fristående formulär med den universella redigeraren genom att välja en Edge Delivery Services-baserad mall i guiden Skapa formulär.

## Krav

* [Konfigurera din GitHub-databas](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) för att upprätta en anslutning mellan din AEM-miljö och GitHub-databasen.
* Om du redan använder Edge Delivery Services lägger du till den senaste versionen av [Adaptive Forms-blocket](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) i din GitHub-databas.
* Instansen AEM Forms Author innehåller en mall baserad på Edge Delivery Services. Kontrollera att den [senaste versionen av Core Components](https://github.com/adobe/aem-core-forms-components) är installerad i din miljö.
* Ha URL:en till din AEM Forms as a Cloud Service-författarinstans och din GitHub-databas till hands.

## Arbeta med formulär i den universella redigeraren

Med den universella redigeraren kan du enkelt skapa responsiva och interaktiva fristående formulär. Du kan utföra följande åtgärder på formulär i Universell redigerare:
* [Skapa ett formulär](#create-a-form)
* [Skapa ett formulär](#author-a-form)
* [Publicera ett formulär](#publish-a-form)
* [Hantera ett formulär](#manage-a-form)

>[!NOTE]
>
> Du kan även [skapa ett formulär på AEM Site med Edge Delivery Services Site-mallen i Universal Editor och publicera det på Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project).


### Skapa ett formulär

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas.
1. På fliken **Source** väljer du en Edge Delivery Services-baserad formulärmall:

   ![Skapa EDS Forms](/help/edge/assets/create-eds-forms.png)


   När du väljer en Edge Delivery Services-baserad mall aktiveras knappen **[!UICONTROL Create]**.
1. (Valfritt) På flikarna **[!UICONTROL Data Source]** eller **[!UICONTROL Submission]** kan du välja en datakälla eller skicka-åtgärd.
1. (Valfritt) På fliken **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett formulär.

1. Klicka på **[!UICONTROL Create]** så visas guiden **Skapa formulär**.
1. Ange **Namn** och **Titel**.
1. Ange **GitHub-URL**. Om din GitHub-databas till exempel har namnet `edsforms`, finns den under kontot `wkndforms`, är URL:en:
   `https://github.com/wkndforms/edsforms`
1. Klicka på **[!UICONTROL Create]**.

   ![Guiden Skapa formulär](/help/edge/assets/create-form-wizard.png)

   När du klickar på **[!UICONTROL Create]** öppnas formuläret i Universell redigerare för redigering.

   ![författare till formuläret](/help/edge/assets/author-form.png)

   <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

   När du klickar på **[!UICONTROL Create]** öppnas formuläret i den universella redigeraren för redigering.

### Skapa ett formulär

1. Öppna innehållsläsaren och navigera till komponenten **[!UICONTROL Adaptive Form]** i **innehållsträdet**.

   ![innehållsträd](/help/edge/assets/content-tree.png)

1. Klicka på ikonen **[!UICONTROL Add]** och lägg till de önskade komponenterna från listan **Adaptiva formulärkomponenter**.

   ![lägg till komponent](/help/edge/assets/add-component.png)

1. Markera den tillagda adaptiva formulärkomponenten och uppdatera dess egenskaper med **[!UICONTROL Properties]**.

   ![öppna egenskaper](/help/edge/assets/component-properties.png)

   På skärmbilden nedan visas det enkla `Registration Form`-formuläret som har skapats i Universella redigerare:

   ![kontakta oss](/help/edge/assets/contact-us.png)

   Nu kan du [konfigurera och anpassa Skicka-åtgärder för formulär](/help/edge/docs/forms/universal-editor/submit-action.md).


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

### Publicera ett formulär

Publicera det fristående formuläret till Edge Delivery Services genom att klicka på knappen **[!UICONTROL Publish]** i det övre högra hörnet av Universell redigerare.

![publicera formulär](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Läs artikeln [Publicera och distribuera](/help/edge/docs/forms/universal-editor/publish-forms.md) om du vill veta mer om hur du publicerar ett formulär till Edge Delivery Services.

Så här kommer du åt formuläret på Edge Delivery Services:

* **Mellanlagrad version (för testning)**: Den mellanlagrade versionen visar den opublicerade, fungerande versionen av formuläret för testning. Använd följande URL-format för att förhandsgranska formuläret innan det publiceras:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Om projektdatabasen till exempel heter &quot;desforms&quot;, finns den under kontot &quot;wkndforms&quot;, och du använder huvudgrenen och formuläret som &quot;Registration Form&quot;, ser den mellanlagrade versions-URL:en ut så här:
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **Live-version (publicerat formulär)**:   Den aktiva versionen visar den senast publicerade versionen av formuläret, som är tillgänglig för slutanvändarna. Använd följande URL-format för att komma åt den publicerade, aktiva versionen av formuläret:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Om projektdatabasen till exempel heter &quot;desforms&quot;, finns den under kontot &quot;wkndforms&quot;, och du använder huvudgrenen och formuläret som &quot;Registration Form&quot;, ser den mellanlagrade versions-URL:en ut så här:
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

URL-strukturen är densamma för både testversioner och liveversioner. Innehållet som du ser skiljer sig dock åt beroende på sammanhanget:

![Visa publicerat formulär](/help/edge/assets/eds-view-publish-form.png)

### Hantera ett formulär

Du kan utföra flera åtgärder på formulär med AEM Forms användargränssnitt.

1. Logga in på din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Markera ett formulär så visas följande åtgärder som du kan utföra på det markerade formuläret i verktygsfältet.

<table>
 <tbody>
  <tr>
   <td><p><strong>Åtgärd</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
  </tr>
  <tr>
   <td><p>Redigera</p> </td>
   <td><p>Öppnar formuläret i redigeringsläge.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Egenskaper</p> </td>
   <td><p>Tillhandahåller alternativ för att ändra egenskaperna för formuläret.<br /> <br /> </p> </td>
  </tr>
  <td><p>Kopiera</p> </td>
   <td><p> Innehåller alternativ för att kopiera formuläret och klistra in det på önskad plats. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Förhandsgranska</p> </td>
   <td><p>Innehåller alternativ för att förhandsgranska formuläret som HTML eller utföra en anpassad förhandsgranskning genom att sammanfoga data från en XML-fil med formuläret. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Ladda ned</p> </td>
   <td><p>Hämtar det markerade formuläret.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Starta granskning/hantera granskning</p> </td>
   <td><p>Tillåter initiering och hantering av en granskning av det valda formuläret.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>-->
  <tr>
   <td><p>Publicera/avpublicera</p> </td>
   <td><p>Publicerar/avpublicerar det markerade formuläret.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Ta bort</p> </td>
   <td><p>Tar bort det markerade formuläret.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Jämför</p> </td>
   <td><p>Jämför två olika former för förhandsgranskning.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Felsökning

Har du problem med att läsa in formuläret? Här är några vanliga problem och hur du åtgärdar dem:

* **Formulär-URL**: Dubbelkontrollera att formulärets URL inte innehåller tillägget .html i slutet. Edge-tjänsten för leverans kräver inte det här tillägget.

* **AEM Author UR** L: Kontrollera att den URL för AEM Author som anges i `fstab.yaml` -filen är korrekt formaterad. Den ska innehålla följande uppgifter:

   * Rätt GitHub-ägare
   * Rätt databasnamn
   * Den specifika gren som du använder för Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Börja skapa formulär

{{universal-editor-see-also}}

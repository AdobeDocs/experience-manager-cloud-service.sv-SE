---
title: Integrering med Content Automation for Creative Cloud
description: Generera varianter av mediefiler med hjälp av Creative Cloud-integrering
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 1d8136b761528fe927b467320ebc7363de0d8a37
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# Generera variationer av resurser med hjälp av [!DNL Adobe Creative Cloud]-integrering {#content-automation}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Tillägget för innehållsautomatisering integrerar [!DNL Adobe Experience Manager Assets] som en [!DNL Cloud Service] - och [!DNL Adobe Creative Cloud]-API för att bearbeta dina resurser i stor skala. [!DNL Experience Manager] använder molnbaserade [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) för att använda [!DNL Adobe Creative Cloud]-funktionerna och automatisera skapandet av resurser och mediehanteringen.

Om du vill redigera resurser i [!DNL Adobe Photoshop] och [!DNL Adobe Lightroom] behöver du inte hämta resurser från [!DNL Experience Manager Assets], redigera och överföra dem igen. Du skapar och konfigurerar en bearbetningsprofil i [!DNL Experience Manager], tillämpar profilen på en mapp och överför resurserna till mappen. Dina överförda resurser bearbetas om baserat på bearbetningsprofilerna och du får variationer av dessa resurser. Den enhetliga och smidiga gruppbearbetningen sparar tid och ökar innehållets hastighet utan att man behöver ha superb kreativ kompetens. Utvecklarna och partnerna kan också utöka sina tillgångsmikrotjänster med direkt åtkomst till dessa API:er och inkludera anpassad logik.

Användare kan skapa bearbetningsprofiler för att automatisera följande kreativa åtgärder för sina resurser:

* **Automatisk ton**: Använder artificiell intelligens för att analysera innehållet i bilden och gör intelligent ljus- och färgkorrigeringar baserat på bildens unika attribut.

* **Automatisk upprätt**: Använder artificiell intelligens för att analysera innehållet i bilden och korrigera skevade perspektiv i bilder. Om du till exempel vill skapa nivåhorisonter.

  ![automatisk ton](/help/assets/assets/content-automation-autotone.png)

  *Bild: Automatisk toning och automatisk upprätning kan hjälpa till att förbättra skevade bilder.*

* **Lightroom-förinställningar**: Använder ett användardefinierat utseende på bilder för att få ett konsekvent utseende med anpassade förinställningar.

  ![Lightroom-förinställning](/help/assets/assets/content-automation-lrpresets.png)

  *Bild: Adobe Lightroom-förinställning förbättrar bildkvaliteten på ett konsekvent sätt för många bilder.*

* **Bildutstansning**: Använder artificiell intelligens för att skapa markering runt utjämnade objekt och ta bort bakgrund med ett enda kommando.

  ![Ta bort bakgrund och klippa ut en bild från ett foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Bildmask**: Använder artificiell intelligens för att skapa en mask runt salivobjekt med ett enda kommando.

  ![Maskera en bild med AI](/help/assets/assets/content-automation-mask.png)

* **Photoshop-åtgärder**: Tillämpar en serie [!DNL Adobe Photoshop] åtgärder på en fil eller en grupp med filer.

  ![Photoshop-åtgärder](/help/assets/assets/content-automation-psactions.png)

* **Smart objektersättning**: Utför personalisering i stor skala genom att låta dig växla bilder samtidigt som du behåller alla effekter och justeringar som används i en PSD-fil.

  ![Ersätt objekt smart](/help/assets/assets/content-automation-objectreplace.png)

## Aktivera Content Automation för AEM as a Cloud Service {#enable-content-automation}

Så här aktiverar du tillägget för innehållsautomatisering för AEM as a Cloud Service med Cloud Manager:

1. Kontakta din kontorepresentant för att licensiera tillägget för innehållsautomatisering.
1. Gå till Cloud Manager och byt till din organisation med hjälp av organisationsväljaren.
1. Klicka på **[!UICONTROL Add Program]** och ange ett programnamn.
1. Klicka på **[!UICONTROL Continue]**.
1. Expandera **[!UICONTROL Assets]** och välj **[!UICONTROL Content Automation]**.
1. Klicka på **[!UICONTROL Create]**.
1. Kör pipelinen för att [distribuera ändringarna till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Om du behöver lägga till tillägget för innehållsautomatisering i ett befintligt AEM as a Cloud Service-program i Cloud Manager:

1. Klicka på ... på programkortet.

1. Välj **[!UICONTROL Edit Program]** och sedan fliken **[!UICONTROL Solutions & Add-ons]**.

1. Expandera **[!UICONTROL Assets]** och välj **[!UICONTROL Content Automation]**.
1. Klicka på **[!UICONTROL Update]**.
1. Kör pipelinen för att [distribuera ändringarna till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Använd en bearbetningsprofil för att redigera flera kreativa resurser samtidigt {#process-assets}

Så här använder du bearbetningsprofiler för att automatiskt skapa variationer:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]**.

1. Välj **[!UICONTROL Create]** och ange **[!UICONTROL Name]**.

1. Välj fliken **[!UICONTROL Creative]**, ange utdatamapp och välj **[!UICONTROL Add New]** för att lägga till en kreativ konfiguration.

1. Ange **[!UICONTROL Rendition Name]** (eller utdatanamn), **[!UICONTROL Extension]** (eller filtyp), välj **[!UICONTROL Quality]** (eller utdataparametrar), välj **[!UICONTROL Includes]** och **[!UICONTROL Excludes]** MIME-typlistor (eller indataresursfilter) och välj önskad kreativ åtgärd.

   fliken ![[!UICONTROL Creative] i [!UICONTROL Processing Profile]](assets/creative-processing-profile.png)

1. Vissa åtgärder kräver extra parametrar (resurs). Ange vid behov värden för de här extra parametrarna.

1. Lägg till fler kreativa åtgärder som en del av samma bearbetningsprofil eller Spara profilen.

1. Använd bearbetningsprofilen på en mapp. På mappens **[!UICONTROL Properties]**-sida väljer du **[!UICONTROL Asset Processing]** och väljer den bearbetningsprofil som ska användas.

När du har tillämpat bearbetningsprofilen på en DAM-mapp kör alla resurser som har överförts eller uppdaterats i den här mappen de definierade åtgärderna förutom standardbearbetningen. Undermapparna ärver samma profiler som de överordnade mapparna. Användare kan åsidosätta detta arv.

Om du vill bearbeta befintliga resurser markerar du resurserna, väljer alternativet **[!UICONTROL Reprocess]** och väljer sedan önskad bearbetningsprofil.

## Tips och begränsningar {#limitations-best-practices}

* [!DNL Experience Manager] begränsar resursbearbetningen till 300 begäranden per minut och miljö och 700 begäranden per minut per organisation.
* Filstorleken är begränsad till 4 GB för [!DNL Adobe Photoshop] API-åtgärder och 1 GB för [!DNL Adobe Lightroom]-åtgärder.
* PDF-återgivningar av Microsoft Office-dokument (&quot;.docx&quot;, &quot;.doc&quot;, &quot;.ppt&quot;, &quot;.pptx&quot;, &quot;.xls&quot;, &quot;.xlsx&quot;) är begränsade till filer som är högst 100 MB.
* Videoomkodning är begränsad till indatafiler på 15 GB eller mindre.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Konfigurera och använda resursmikrotjänster via bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).
>* [Integrera [!DNL Experience Manager] med [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Tillgångsinmatning och bearbetning med tillgångsmikrotjänster: En översikt](/help/assets/asset-microservices-overview.md).

---
title: Integrera [!DNL AEM Assets] med [!DNL Figma].
description: Lär dig att integrera [!DNL AEM Assets] med [!DNL Figma] för att komma åt och använda organisationens resurser i ditt  [!DNL Figma] designarbetsflöde.
hide: false
role: User
source-git-commit: 25434ebc76096055940d8d85640b28ce4db36d3a
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Integrera [!DNL AEM Assets] med [!DNL Figma]{#integrate-aem-assets-with-figma}

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

[!DNL AEM Assets] kan integreras med [!DNL Figma], vilket gör att designers kan komma åt resurser som lagras i [!DNL AEM Assets] direkt från användargränssnittet i [!DNL Figma]. Du kan placera innehåll som hanteras i [!DNL AEM Assets] på arbetsytan [!DNL Figma] och sedan spara nytt eller redigerat innehåll i databasen [!DNL AEM Assets].

## Innan du börjar{#prerequisites-for-aem-assets-and-figma-integration}

* Den lägsta version av AEM som krävs är `19149`.

* Du måste ha giltiga [!DNL AEM Assets]- och [!DNL Figma]-licenser för att kunna integrera [!DNL AEM Assets] med [!DNL Figma].

## Åtkomst [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]{#access-aem-assets-connector}

Utför följande steg för att komma åt [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]:

1. På din [!DNL Figma]-hemsida klickar du på **[!UICONTROL Actions]** i verktygsfältet längst ned på arbetsytan och söker efter [!DNL Adobe Experience Manager (AEM) Assets Connector] i sökfältet som finns i dialogrutan.
1. Välj [!DNL Adobe Experience Manager (AEM) Assets Connector] om du vill visa panelen [!DNL Adobe Experience Manager (AEM) Assets Connector]. [Importera [!DNL AEM] resurser till din [!DNL Figma] arbetsyta](#import-aem-assets-into-figma-workflow) med den här panelen.
   ![åtgärder](/help/assets/assets/actions-on-figma.png)
Du kan även komma åt den [[!DNL Adobe Experience Manager (AEM) Assets Connector] ](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) som är tillgänglig i [!DNL Figma] användargruppen, klicka på **[!UICONTROL Open in...]** , välja en nyligen använd fil eller skapa en ny fil och klicka på **[!UICONTROL Run]** för att komma åt panelen [!DNL Adobe Experience Manager (AEM) Assets Connector] .
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [Kontakta Adobe Support](https://helpx.adobe.com/se/contact.html) om du behöver hjälp om du får ett **[!UICONTROL Network Error]**-meddelande efter att du loggat in i din [!DNL AEM]-miljö.

## Importera [!DNL AEM] resurser till arbetsytan i [!DNL Figma]{#import-aem-assets-into-figma-workflow}

[Öppna [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]-panelen](#access-aem-assets-connector) i designgränssnittet i [!DNL Figma] och gör följande:

1. Sök efter resurser på panelen [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]. Mer information finns i [Använda resursväljaren](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector).

1. Dra och släpp resursen på arbetsytan eller markera resursen och klicka på **[!UICONTROL Select]** för att lägga resursen på arbetsytan.

1. Klicka på ![tre punkter](/help/assets/assets/three-dots.svg) i mappsökvägen om du vill visa alla överordnade och underordnade mappar i den aktuella hierarkin. Välj en mapp att navigera till den platsen.
   ![tre punkter](/help/assets/assets/assets-folder-structure.png)

När din Figma-design är klar kan du [exportera resursen till AEM Assets-databasen](#export-figma-design-to-aem-assets-folder).

## Exportera resurser till [!DNL AEM Assets]-databasen{#export-figma-design-to-aem-assets-folder}

[Använd [!UICONTROL Adobe Experience Manager (AEM) Assets Connector] panel](#access-aem-assets-connector) i designgränssnittet i [!DNL Figma] och utför följande steg för att exportera din design till databasen [!DNL AEM Assets]:

1. Navigera till målmappen där du vill spara din [!DNL Figma]-design. Om du redan finns i en mapp klickar du på Fler alternativ (![tre punkter](/help/assets/assets/three-dots.svg)) i mappsökvägen för att välja en annan målmapp.
1. Valfritt: Gruppera resurser på arbetsytan för att välja dem som en enhet att överföra till din mapp.
1. Klicka på ![filöverföring](/help/assets/assets/upload-icon.svg) **[!UICONTROL Upload]** för att visa dialogrutan **[!UICONTROL Upload Asset]**.
1. Ange ett filnamn i dialogrutan, välj ett filformat, markera **[!UICONTROL Selected Item]** eller **[!UICONTROL Page]** och klicka på **[!UICONTROL Upload]** för att överföra den markerade resursen eller hela designen till målmappen.
   ![överför figma-design](/help/assets/assets/upload-figma-design.png)

## Viktiga punkter att notera{#Limitations-of-using-aem-assets-into-figma}

Den här integreringen har för närvarande följande begränsningar:

* För import av [!DNL AEM]-resurser till Figma är formaten **JPEG**, **PNG** som stöds.
* För export av designer från [!DNL Figma] till [!DNL AEM Assets] är formaten **PNG**, **PDF**, **JPG** och **SVG** som stöds.




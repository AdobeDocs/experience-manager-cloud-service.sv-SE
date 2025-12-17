---
title: Integrera [!DNL AEM Assets] med [!DNL Figma].
description: Lär dig att integrera [!DNL AEM Assets] med [!DNL Figma] för att komma åt och använda organisationens resurser i ditt  [!DNL Figma] designarbetsflöde.
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: a9c1f5472092b3b9fa7a5e5570feb92f32e9ef6c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---


# Integrera [!DNL AEM Assets] med [!DNL Figma]{#integrate-aem-assets-with-figma}

[!DNL AEM Assets] kan integreras med [!DNL Figma], vilket gör att designers kan komma åt resurser som lagras i [!DNL AEM Assets] direkt från användargränssnittet i [!DNL Figma]. Du kan placera innehåll som hanteras i [!DNL AEM Assets] på arbetsytan [!DNL Figma] och sedan spara nytt eller redigerat innehåll i databasen [!DNL AEM Assets].

## Innan du börjar{#prerequisites-for-aem-assets-and-figma-integration}

* Den lägsta version av AEM som krävs är `19149`.

* Du måste ha giltiga [!DNL AEM Assets]- och [!DNL Figma]-licenser för att kunna integrera [!DNL AEM Assets] med [!DNL Figma].

## Filformat som stöds {#supported-file-formats-integration-figma}


* För import av [!DNL AEM]-resurser till Figma är de format som stöds bildresurser (JPEG, PNG), videofiler (MP4, MOV, WebM), animerade filer (GIF) och vektorfiler (SVG).
* För export av designer från [!DNL Figma] till [!DNL AEM Assets] är formaten **PNG**, **PDF**, **JPG** och **SVG** som stöds.

## Åtkomst [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]{#access-aem-assets-connector}

Utför följande steg för att komma åt [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]:

1. På din [!DNL Figma]-hemsida klickar du på **[!UICONTROL Actions]** i verktygsfältet längst ned på arbetsytan och söker efter [!DNL Adobe Experience Manager (AEM) Assets Connector] i sökfältet som finns i dialogrutan.
1. Välj [!DNL Adobe Experience Manager (AEM) Assets Connector] om du vill visa panelen [!DNL Adobe Experience Manager (AEM) Assets Connector]. [Importera [!DNL AEM] resurser till din [!DNL Figma] arbetsyta](#import-aem-assets-into-figma-workflow) med den här panelen.
   ![åtgärder](/help/assets/assets/actions-on-figma.png)
Du kan även komma åt den [[!DNL Adobe Experience Manager (AEM) Assets Connector] ](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) som är tillgänglig i [!DNL Figma] användargruppen, klicka på **[!UICONTROL Open in...]** , välja en nyligen använd fil eller skapa en ny fil och klicka på **[!UICONTROL Run]** för att komma åt panelen [!DNL Adobe Experience Manager (AEM) Assets Connector] .
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [Kontakta Adobe Support](https://helpx.adobe.com/contact.html) om du behöver hjälp om du får ett **[!UICONTROL Network Error]**-meddelande efter att du loggat in i din [!DNL AEM]-miljö.

## Importera [!DNL AEM] resurser till arbetsytan i [!DNL Figma]{#import-aem-assets-into-figma-workflow}

[Öppna [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]-panelen](#access-aem-assets-connector) i designgränssnittet i [!DNL Figma] och gör följande:

1. Sök efter resurser på panelen [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]. Mer information finns i [Använda resursväljaren](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector).

1. Dra och släpp resursen på arbetsytan eller markera resursen och klicka på **[!UICONTROL Select]** för att lägga resursen på arbetsytan.

1. Klicka på ![tre punkter](/help/assets/assets/three-dots.svg) i mappsökvägen om du vill visa alla överordnade och underordnade mappar i den aktuella hierarkin. Välj en mapp att navigera till den platsen.
   ![tre punkter](/help/assets/assets/figma-v2-plugin.png)

1. [Valfritt] Klicka **[!UICONTROL Check for updates]**. De resurser som används i det aktuella Figma-dokumentet jämförs med de resurser som finns i AEM. Alla uppdateringar visas i ett separat fönster. Klicka på **[!UICONTROL Update]** om du vill hämta den uppdaterade resursen från AEM till ditt Figma-dokument.

När din Figma-design är klar kan du [exportera resursen till AEM Assets-databasen](#export-figma-design-to-aem-assets-folder).

## Exportera resurser till [!DNL AEM Assets]-databasen{#export-figma-design-to-aem-assets-folder}

[Använd [!UICONTROL Adobe Experience Manager (AEM) Assets Connector] panel](#access-aem-assets-connector) i designgränssnittet i [!DNL Figma] och utför följande steg för att exportera din design till databasen [!DNL AEM Assets]:

1. Navigera till målmappen där du vill spara din [!DNL Figma]-design. Om du redan finns i en mapp klickar du på Fler alternativ (![tre punkter](/help/assets/assets/three-dots.svg)) i mappsökvägen för att välja en annan målmapp.
1. Valfritt: Gruppera resurser på arbetsytan för att välja dem som en enhet att överföra till din mapp.
1. Klicka på ![filöverföring](/help/assets/assets/upload-icon.svg) **[!UICONTROL Upload]** för att visa dialogrutan **[!UICONTROL Upload Asset]**.
1. I dialogrutan väljer du antingen **[!UICONTROL Selected Item]** eller **[!UICONTROL Page]**, anger ett fil- eller sidnamn, definierar en exportkonfiguration och klickar på **[!UICONTROL Upload]** för att överföra den markerade resursen eller hela designen till målmappen.

   Exportkonfigurationen omfattar filformat, skala och kvalitet. Om du t.ex. väljer JPG som filformat kan du även definiera bildens skala och kvalitet. Om du väljer PNG som filformat kan du också definiera bildskalan.
   ![överför figma-design](/help/assets/assets/upload-figma-design.png)

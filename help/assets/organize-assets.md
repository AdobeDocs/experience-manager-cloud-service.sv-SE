---
title: Ordna dina digitala resurser
description: Organisera dina digitala resurser, bilder, filer, mappar och så vidare med Experience Manager.
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# Ordna dina digitala resurser {#organize-digital-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Alla digitala resurser, metadata och innehåll i Microsoft® Office- och PDF-dokument extraheras och blir sökbara. Sökning möjliggör avancerad filtrering av resurser och respekterar helt rätt behörigheter. Metadata beskrivs i detalj i Metadata i Digital Asset Management.

[!DNL Experience Manager Assets] har stöd för flera sätt att ordna innehåll. Du kan ordna dem hierarkiskt med hjälp av mappar eller ordna dem på ett oordnat sätt, t.ex. med taggar. Användare kan redigera taggar i DAM-redigeraren där delresurser, återgivningar och metadata visas.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them easier to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Ordna resurser i mappar {#organize-using-folders}

Det mest grundläggande sättet att ordna resurser är att spara resurserna i mappar. Det motsvarar att ordna filer i mappar i det lokala filsystemet. Mer information om hur du skapar och hanterar mappar finns i [Hantera resurser](manage-digital-assets.md). Hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar kan påverka hur dessa resurser bearbetas. Genom att använda enhetliga och lämpliga namngivningsstrategier för filer och mappar tillsammans med god metadatapraxis kan ni få ut det mesta av era digitala resurslager.

* Vanligtvis växer databasen med digitala resurser. Därför är det viktigt att formalisera metadataanvändning, mappstruktur och filnamngivning tidigt när du skapar innehåll.
* Använd endast mappar för att få en enhetlig lagringsstruktur för dina digitala resurser. Denna konsekvens hjälper er att arbeta och hantera ert material bättre. Resurser som placeras i följande typer av mappar kan till exempel hjälpa dig att dela upp dina resurser:

   * **Utvecklingsmappar**: innehåller digitala resurser som du för närvarande arbetar med.
   * **Klientmappar**: innehåller digitala resurser baserade på klienter eller projektnamn.
   * **Primära mappar**: innehåller digitala källresurser.
   * **Återgivningsmappar**: innehåller återgivningar och kopior av det ursprungliga digitala källmaterialet.
   * **Filstorleksmappar**: innehåller digitala resurser baserade på små, medelstora eller stora filstorlekar.
   * **Mellanlagringsmappar**: innehåller digitala resurser som är klara att publiceras live på din webbplats.
   * **MIME-typmappar**: innehåller digitala resurser som är specifika för MIME-typer, t.ex. bilder, dokument och multimedia.
   * **Arkivera mappar**: innehåller pensionerade digitala resurser.
   * **Datumbaserade mappar**: innehåller digitala resurser baserat på skapandedatum eller senaste ändringsdatum.

* Skapa en katalog med mappar som troligtvis inte ändras så att anpassningar och automatisering fortsätter att fungera. De tilldelade bearbetningsprofilerna fortsätter till exempel att fungera.
* Om en resurs redan har publicerats använder du [!DNL Experience Manager] om du vill flytta resursen till en annan mapp och publicera på nytt från den nya platsen. Den ursprungliga publicerade resursplatsen är fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock *vilse* till [!DNL Experience Manager] och kan inte avpubliceras. Därför bör du först avpublicera en resurs och sedan flytta den till en annan mapp.

## Ordna resurser med hjälp av taggar {#use-tags-to-organize-assets}

Om du lägger till taggar i resurser blir det enklare att hämta dem under en sökning, skapa samlingar med hjälp av sökresultaten, öka rankningen för vissa resurser och använda AI-algoritmer i Adobe Sensei för tillgångsidentifiering.

[!DNL Adobe Experience Manager Assets] använder en självlärande algoritm för att skapa mycket beskrivande taggar som gör att du kan hitta rätt resurs med bara några klick. Smart taggning använder Adobe Sensei, artificiell intelligens och maskininlärningsmiljö, som kan utbildas för att känna igen och använda både standard- och företagsspecifika taggar på bilder. Smarta taggar kan även identifiera innehåll, enskilda ord eller fraser och automatiskt använda beskrivande taggar på resurser.

Så här lägger du till taggar i en resurs:

1. Logga in på [!DNL Experience Manager Assets].
1. Klicka **[!UICONTROL Assets]** > **[!UICONTROL Files]**, markera resursen och klicka på **[!UICONTROL Properties]** för att öppna resursegenskaperna.
1. I **[!UICONTROL Basic]** klickar du på mappikonen i **[!UICONTROL Tags]** metadata. Ett popup-fönster öppnas.
1. Sök efter eller välj lämpliga taggar från de befintliga taggarna i `cq-tags`. Du kan tilldela flera taggar till resursen.

   Du kan sortera taggstrukturen i stigande eller fallande ordning baserat på **[!UICONTROL Name]** (i alfabetisk ordning), **[!UICONTROL Created]** datum, eller **[!UICONTROL Modified]** datum. I följande bild sorteras taggstrukturen i bokstavsordning baserat på **[!UICONTROL Name]**.

   ![add-tags](assets/add-tags-to-asset.png)

1. Klicka **Spara** om du vill uppdatera ändringar i metadata för resursen.

Mer information finns i följande artiklar:

* [Redigera metadata för resurser](meta-edit.md)
* [Smarta taggar i resurser](smart-tags.md)
* [Lägga till taggar och predikat i sökpanelen](/help/assets/search-facets.md/#adding-a-tags-predicate)

## Ordna som samlingar {#organize-as-collections}

Med resurssamlingar i [!DNL Experience Manager Assets]kan du effektivisera möjligheten att skapa, redigera och dela resurser mellan användare. Skapa flera typer av samlingar baserat på hur du använder dem, inklusive samlingar som innehåller en statisk referenslista över resurser, mappar och samlingar samt samlingar som hämtar resurser baserat på sökvillkor. Du kan skapa samlingar med resurser från olika platser och dela dem med flera användare med olika åtkomstnivåer, behörighet att visa och redigera.

Mer information finns i [hantera samlingar](manage-collections.md)


## Använd profiler för att ordna dina resurser {#organize-to-use-profiles}

En bearbetningsprofil innehåller [!DNL Assets] bearbetningskommandon som gäller för resurser som överförs till fördefinierade mappar. Profiler används för att automatisera bearbetningen av innehållet i en mapp eller nyligen överförda resurser. Du kan använda profiler för att ordna dina resurser bättre.

Genom att standardisera metadataanvändning, filnamngivning och mappstruktur säkerställer du att du kan tillämpa bearbetningsprofiler på mappar med större precision och enhetlighet när din pool med digitala resurser växer.

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Använda mikrotjänster och bearbetningsprofiler](asset-microservices-configure-and-use.md)
>* [Metadataprofiler](metadata-profiles.md)
>* [Videoprofiler](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Media bildprofiler](/help/assets/dynamic-media/image-profiles.md)

